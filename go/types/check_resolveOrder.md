check.resolveOrder()
====================

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
// resolveOrder computes the order in which package-level objects
// must be type-checked.
//
// Interface types appear first in the list, sorted topologically
// by dependencies on embedded interfaces that are also declared
// in this package, followed by all other objects sorted in source
// order.
//
// TODO(gri) Consider sorting all types by dependencies here, and
// in the process check _and_ report type cycles. This may simplify
// the full type-checking phase.
//
func (check *Checker) resolveOrder() []Object {
	var ifaces, others []Object

	// collect interface types with their dependencies, and all other objects
	for obj := range check.objMap {
		if ityp := check.interfaceFor(obj); ityp != nil {
			ifaces = append(ifaces, obj)
			// determine dependencies on embedded interfaces
			for _, f := range ityp.Methods.List {
				if len(f.Names) == 0 {
					// Embedded interface: The type must be a (possibly
					// qualified) identifier denoting another interface.
					// Imported interfaces are already fully resolved,
					// so we can ignore qualified identifiers.
					if ident, _ := f.Type.(*ast.Ident); ident != nil {
						embedded := check.pkg.scope.Lookup(ident.Name)
						if check.interfaceFor(embedded) != nil {
							check.objMap[obj].addDep(embedded)
						}
					}
				}
			}
		} else {
			others = append(others, obj)
		}
	}

	// final object order
	var order []Object

	// sort interface types topologically by dependencies,
	// and in source order if there are no dependencies
	sort.Sort(inSourceOrder(ifaces))
	if debug {
		for _, obj := range ifaces {
			assert(check.objMap[obj].mark == 0)
		}
	}
	for _, obj := range ifaces {
		check.appendInPostOrder(&order, obj)
	}

	// sort everything else in source order
	sort.Sort(inSourceOrder(others))

	return append(order, others...)
}
```

Prev: [check.collectObjects()](./check_collectObjects.md)

Next: [check.packageObjects(check.resolveOrder())](./check_collectObjects.md)
