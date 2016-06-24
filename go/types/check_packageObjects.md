check.packageObjects()
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
// packageObjects typechecks all package objects in objList, but not function bodies.
func (check *Checker) packageObjects(objList []Object) {
	// add new methods to already type-checked types (from a prior Checker.Files call)
	for _, obj := range objList {
		if obj, _ := obj.(*TypeName); obj != nil && obj.typ != nil {
			check.addMethodDecls(obj)
		}
	}

	// pre-allocate space for type declaration paths so that the underlying array is reused
	typePath := make([]*TypeName, 0, 8)

	for _, obj := range objList {
		check.objDecl(obj, nil, typePath)
	}

	// At this point we may have a non-empty check.methods map; this means that not all
	// entries were deleted at the end of typeDecl because the respective receiver base
	// types were not found. In that case, an error was reported when declaring those
	// methods. We can now safely discard this map.
	check.methods = nil
}
```

Prev: [check.resolveOrder()](./check_resolveOrder.md)

Next: [check.functionBodies()](./check_functionBodies.md)
