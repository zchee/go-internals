check.collectObjects()
======================

```go
// A Checker maintains the state of the type checker.
// It must be created with NewChecker.
type Checker struct {
	// package information
	// (initialized by NewChecker, valid for the life-time of checker)
	conf *Config
	fset *token.FileSet
	pkg  *Package
	*Info
	objMap map[Object]*declInfo // maps package-level object to declaration info

	// information collected during type-checking of a set of package files
	// (initialized by Files, valid only for the duration of check.Files;
	// maps and lists are allocated on demand)
	files            []*ast.File                       // package files
	unusedDotImports map[*Scope]map[*Package]token.Pos // positions of unused dot-imported packages for each file scope

	firstErr error                 // first error encountered
	methods  map[string][]*Func    // maps type names to associated methods
	untyped  map[ast.Expr]exprInfo // map of expressions without final type
	funcs    []funcInfo            // list of functions to type-check
	delayed  []func()              // delayed checks requiring fully setup types

	// context within which the current object is type-checked
	// (valid only for the duration of type-checking a specific object)
	context
	pos token.Pos // if valid, identifiers are looked up as if at position pos (used by Eval)

	// debugging
	indent int // indentation for tracing
}
```

```go
// collectObjects collects all file and package objects and inserts them
// into their respective scopes. It also performs imports and associates
// methods with receiver base type names.
func (check *Checker) collectObjects() {
	pkg := check.pkg

	// pkgImports is the set of packages already imported by any package file seen
	// so far. Used to avoid duplicate entries in pkg.imports. Allocate and populate
	// it (pkg.imports may not be empty if we are checking test files incrementally).
	var pkgImports = make(map[*Package]bool)
	for _, imp := range pkg.imports {
		pkgImports[imp] = true
	}

	// srcDir is the directory used by the Importer to look up packages.
	// The typechecker itself doesn't need this information so it is not
	// explicitly provided. Instead, we extract it from position info of
	// the source files as needed.
	// This is the only place where the type-checker (just the importer)
	// needs to know the actual source location of a file.
	// TODO(gri) can we come up with a better API instead?
	var srcDir string
	if len(check.files) > 0 {
		// FileName may be "" (typically for tests) in which case
		// we get "." as the srcDir which is what we would want.
		srcDir = dir(check.fset.Position(check.files[0].Name.Pos()).Filename)
	}

	for fileNo, file := range check.files {
		// The package identifier denotes the current package,
		// but there is no corresponding package object.
		check.recordDef(file.Name, nil)

		// Use the actual source file extent rather than *ast.File extent since the
		// latter doesn't include comments which appear at the start or end of the file.
		// Be conservative and use the *ast.File extent if we don't have a *token.File.
		pos, end := file.Pos(), file.End()
		if f := check.fset.File(file.Pos()); f != nil {
			pos, end = token.Pos(f.Base()), token.Pos(f.Base()+f.Size())
		}
		fileScope := NewScope(check.pkg.scope, pos, end, check.filename(fileNo))
		check.recordScope(file, fileScope)

		for _, decl := range file.Decls {
			switch d := decl.(type) {
			case *ast.BadDecl:
				// ignore

			case *ast.GenDecl:
				var last *ast.ValueSpec // last ValueSpec with type or init exprs seen
				for iota, spec := range d.Specs {
					switch s := spec.(type) {
					case *ast.ImportSpec:
						// import package
						var imp *Package
						path, err := validatedImportPath(s.Path.Value)
						if err != nil {
							check.errorf(s.Path.Pos(), "invalid import path (%s)", err)
							continue
						}
						if path == "C" && check.conf.FakeImportC {
							// TODO(gri) shouldn't create a new one each time
							imp = NewPackage("C", "C")
							imp.fake = true
						} else {
							// ordinary import
							if importer := check.conf.Importer; importer == nil {
								err = fmt.Errorf("Config.Importer not installed")
							} else if importerFrom, ok := importer.(ImporterFrom); ok {
								imp, err = importerFrom.ImportFrom(path, srcDir, 0)
								if imp == nil && err == nil {
									err = fmt.Errorf("Config.Importer.ImportFrom(%s, %s, 0) returned nil but no error", path, pkg.path)
								}
							} else {
								imp, err = importer.Import(path)
								if imp == nil && err == nil {
									err = fmt.Errorf("Config.Importer.Import(%s) returned nil but no error", path)
								}
							}
							if err != nil {
								check.errorf(s.Path.Pos(), "could not import %s (%s)", path, err)
								continue
							}
						}

						// add package to list of explicit imports
						// (this functionality is provided as a convenience
						// for clients; it is not needed for type-checking)
						if !pkgImports[imp] {
							pkgImports[imp] = true
							if imp != Unsafe {
								pkg.imports = append(pkg.imports, imp)
							}
						}

						// local name overrides imported package name
						name := imp.name
						if s.Name != nil {
							name = s.Name.Name
							if path == "C" {
								// match cmd/compile (not prescribed by spec)
								check.errorf(s.Name.Pos(), `cannot rename import "C"`)
								continue
							}
							if name == "init" {
								check.errorf(s.Name.Pos(), "cannot declare init - must be func")
								continue
							}
						}

						obj := NewPkgName(s.Pos(), pkg, name, imp)
						if s.Name != nil {
							// in a dot-import, the dot represents the package
							check.recordDef(s.Name, obj)
						} else {
							check.recordImplicit(s, obj)
						}

						if path == "C" {
							// match cmd/compile (not prescribed by spec)
							obj.used = true
						}

						// add import to file scope
						if name == "." {
							// merge imported scope with file scope
							for _, obj := range imp.scope.elems {
								// A package scope may contain non-exported objects,
								// do not import them!
								if obj.Exported() {
									// TODO(gri) When we import a package, we create
									// a new local package object. We should do the
									// same for each dot-imported object. That way
									// they can have correct position information.
									// (We must not modify their existing position
									// information because the same package - found
									// via Config.Packages - may be dot-imported in
									// another package!)
									check.declare(fileScope, nil, obj, token.NoPos)
									check.recordImplicit(s, obj)
								}
							}
							// add position to set of dot-import positions for this file
							// (this is only needed for "imported but not used" errors)
							check.addUnusedDotImport(fileScope, imp, s.Pos())
						} else {
							// declare imported package object in file scope
							check.declare(fileScope, nil, obj, token.NoPos)
						}

					case *ast.ValueSpec:
						switch d.Tok {
						case token.CONST:
							// determine which initialization expressions to use
							switch {
							case s.Type != nil || len(s.Values) > 0:
								last = s
							case last == nil:
								last = new(ast.ValueSpec) // make sure last exists
							}

							// declare all constants
							for i, name := range s.Names {
								obj := NewConst(name.Pos(), pkg, name.Name, nil, constant.MakeInt64(int64(iota)))

								var init ast.Expr
								if i < len(last.Values) {
									init = last.Values[i]
								}

								d := &declInfo{file: fileScope, typ: last.Type, init: init}
								check.declarePkgObj(name, obj, d)
							}

							check.arityMatch(s, last)

						case token.VAR:
							lhs := make([]*Var, len(s.Names))
							// If there's exactly one rhs initializer, use
							// the same declInfo d1 for all lhs variables
							// so that each lhs variable depends on the same
							// rhs initializer (n:1 var declaration).
							var d1 *declInfo
							if len(s.Values) == 1 {
								// The lhs elements are only set up after the for loop below,
								// but that's ok because declareVar only collects the declInfo
								// for a later phase.
								d1 = &declInfo{file: fileScope, lhs: lhs, typ: s.Type, init: s.Values[0]}
							}

							// declare all variables
							for i, name := range s.Names {
								obj := NewVar(name.Pos(), pkg, name.Name, nil)
								lhs[i] = obj

								d := d1
								if d == nil {
									// individual assignments
									var init ast.Expr
									if i < len(s.Values) {
										init = s.Values[i]
									}
									d = &declInfo{file: fileScope, typ: s.Type, init: init}
								}

								check.declarePkgObj(name, obj, d)
							}

							check.arityMatch(s, nil)

						default:
							check.invalidAST(s.Pos(), "invalid token %s", d.Tok)
						}

					case *ast.TypeSpec:
						obj := NewTypeName(s.Name.Pos(), pkg, s.Name.Name, nil)
						check.declarePkgObj(s.Name, obj, &declInfo{file: fileScope, typ: s.Type})

					default:
						check.invalidAST(s.Pos(), "unknown ast.Spec node %T", s)
					}
				}

			case *ast.FuncDecl:
				name := d.Name.Name
				obj := NewFunc(d.Name.Pos(), pkg, name, nil)
				if d.Recv == nil {
					// regular function
					if name == "init" {
						// don't declare init functions in the package scope - they are invisible
						obj.parent = pkg.scope
						check.recordDef(d.Name, obj)
						// init functions must have a body
						if d.Body == nil {
							check.softErrorf(obj.pos, "missing function body")
						}
					} else {
						check.declare(pkg.scope, d.Name, obj, token.NoPos)
					}
				} else {
					// method
					check.recordDef(d.Name, obj)
					// Associate method with receiver base type name, if possible.
					// Ignore methods that have an invalid receiver, or a blank _
					// receiver name. They will be type-checked later, with regular
					// functions.
					if list := d.Recv.List; len(list) > 0 {
						typ := list[0].Type
						if ptr, _ := typ.(*ast.StarExpr); ptr != nil {
							typ = ptr.X
						}
						if base, _ := typ.(*ast.Ident); base != nil && base.Name != "_" {
							check.assocMethod(base.Name, obj)
						}
					}
				}
				info := &declInfo{file: fileScope, fdecl: d}
				check.objMap[obj] = info
				obj.setOrder(uint32(len(check.objMap)))

			default:
				check.invalidAST(d.Pos(), "unknown ast.Decl node %T", d)
			}
		}
	}

	// verify that objects in package and file scopes have different names
	for _, scope := range check.pkg.scope.children /* file scopes */ {
		for _, obj := range scope.elems {
			if alt := pkg.scope.Lookup(obj.Name()); alt != nil {
				if pkg, ok := obj.(*PkgName); ok {
					check.errorf(alt.Pos(), "%s already declared through import of %s", alt.Name(), pkg.Imported())
					check.reportAltDecl(pkg)
				} else {
					check.errorf(alt.Pos(), "%s already declared through dot-import of %s", alt.Name(), obj.Pkg())
					// TODO(gri) dot-imported objects don't have a position; reportAltDecl won't print anything
					check.reportAltDecl(obj)
				}
			}
		}
	}
}
```

Prev: [check.initFiles(files)](./check_initFiles.md)

Next: [check.resolveOrder()](./check_resolveOrder.md)
