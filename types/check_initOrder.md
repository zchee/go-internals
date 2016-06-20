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
// initOrder computes the Info.InitOrder for package variables.
func (check *Checker) initOrder() {
	// An InitOrder may already have been computed if a package is
	// built from several calls to (*Checker).Files. Clear it.
	check.Info.InitOrder = check.Info.InitOrder[:0]

	// Compute the transposed object dependency graph and initialize
	// a priority queue with the list of graph nodes.
	pq := nodeQueue(dependencyGraph(check.objMap))
	heap.Init(&pq)

	const debug = false
	if debug {
		fmt.Printf("Computing initialization order for %s\n\n", check.pkg)
		fmt.Println("Object dependency graph:")
		for obj, d := range check.objMap {
			if len(d.deps) > 0 {
				fmt.Printf("\t%s depends on\n", obj.Name())
				for dep := range d.deps {
					fmt.Printf("\t\t%s\n", dep.Name())
				}
			} else {
				fmt.Printf("\t%s has no dependencies\n", obj.Name())
			}
		}
		fmt.Println()

		fmt.Println("Transposed object dependency graph:")
		for _, n := range pq {
			fmt.Printf("\t%s depends on %d nodes\n", n.obj.Name(), n.in)
			for _, out := range n.out {
				fmt.Printf("\t\t%s is dependent\n", out.obj.Name())
			}
		}
		fmt.Println()

		fmt.Println("Processing nodes:")
	}

	// Determine initialization order by removing the highest priority node
	// (the one with the fewest dependencies) and its edges from the graph,
	// repeatedly, until there are no nodes left.
	// In a valid Go program, those nodes always have zero dependencies (after
	// removing all incoming dependencies), otherwise there are initialization
	// cycles.
	mark := 0
	emitted := make(map[*declInfo]bool)
	for len(pq) > 0 {
		// get the next node
		n := heap.Pop(&pq).(*objNode)

		if debug {
			fmt.Printf("\t%s (src pos %d) depends on %d nodes now\n",
				n.obj.Name(), n.obj.order(), n.in)
		}

		// if n still depends on other nodes, we have a cycle
		if n.in > 0 {
			mark++ // mark nodes using a different value each time
			cycle := findPath(n, n, mark)
			if i := valIndex(cycle); i >= 0 {
				check.reportCycle(cycle, i)
			}
			// ok to continue, but the variable initialization order
			// will be incorrect at this point since it assumes no
			// cycle errors
		}

		// reduce dependency count of all dependent nodes
		// and update priority queue
		for _, out := range n.out {
			out.in--
			heap.Fix(&pq, out.index)
		}

		// record the init order for variables with initializers only
		v, _ := n.obj.(*Var)
		info := check.objMap[v]
		if v == nil || !info.hasInitializer() {
			continue
		}

		// n:1 variable declarations such as: a, b = f()
		// introduce a node for each lhs variable (here: a, b);
		// but they all have the same initializer - emit only
		// one, for the first variable seen
		if emitted[info] {
			continue // initializer already emitted, if any
		}
		emitted[info] = true

		infoLhs := info.lhs // possibly nil (see declInfo.lhs field comment)
		if infoLhs == nil {
			infoLhs = []*Var{v}
		}
		init := &Initializer{infoLhs, info.init}
		check.Info.InitOrder = append(check.Info.InitOrder, init)
	}

	if debug {
		fmt.Println()
		fmt.Println("Initialization order:")
		for _, init := range check.Info.InitOrder {
			fmt.Printf("\t%s\n", init)
		}
		fmt.Println()
	}
}
```

Prev: [check.functionBodies()](./check_functionBodies.md)

Next: [check.unusedImports()](./check_unusedImports.md)
