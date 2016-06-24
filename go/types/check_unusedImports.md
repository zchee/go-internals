types.Check()
=============

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
// perform delayed checks
for _, f := range check.delayed {
	f()
}
```

```go
// unusedImports checks for unused imports.
func (check *Checker) unusedImports() {
	// if function bodies are not checked, packages' uses are likely missing - don't check
	if check.conf.IgnoreFuncBodies {
		return
	}

	// spec: "It is illegal (...) to directly import a package without referring to
	// any of its exported identifiers. To import a package solely for its side-effects
	// (initialization), use the blank identifier as explicit package name."

	// check use of regular imported packages
	for _, scope := range check.pkg.scope.children /* file scopes */ {
		for _, obj := range scope.elems {
			if obj, ok := obj.(*PkgName); ok {
				// Unused "blank imports" are automatically ignored
				// since _ identifiers are not entered into scopes.
				if !obj.used {
					path := obj.imported.path
					base := pkgName(path)
					if obj.name == base {
						check.softErrorf(obj.pos, "%q imported but not used", path)
					} else {
						check.softErrorf(obj.pos, "%q imported but not used as %s", path, obj.name)
					}
				}
			}
		}
	}

	// check use of dot-imported packages
	for _, unusedDotImports := range check.unusedDotImports {
		for pkg, pos := range unusedDotImports {
			check.softErrorf(pos, "%q imported but not used", pkg.path)
		}
	}
}
```

Prev: [check.initOrder()](./check_initOrder.md)

Next: [check.recordUntyped()](./check_recordUntyped.md)
