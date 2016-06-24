check.checkFiles()
==================

```go
func (conf *Config) Check(path string, fset *token.FileSet, files []*ast.File, info *Info) (*Package, error) {
	pkg := NewPackage(path, "")
	return pkg, NewChecker(conf, fset, pkg, info).Files(files)
}
```

```go
// NewPackage returns a new Package for the given package path and name;
// the name must not be the blank identifier.
// The package is not complete and contains no explicit imports.
func NewPackage(path, name string) *Package {
	if name == "_" {
		panic("invalid package name _")
	}
	scope := NewScope(Universe, token.NoPos, token.NoPos, fmt.Sprintf("package %q", path))
	return &Package{path: path, name: name, scope: scope}
}
```

```go
// NewChecker returns a new Checker instance for a given package.
// Package files may be added incrementally via checker.Files.
func NewChecker(conf *Config, fset *token.FileSet, pkg *Package, info *Info) *Checker {
	// make sure we have a configuration
	if conf == nil {
		conf = new(Config)
	}

	// make sure we have an info struct
	if info == nil {
		info = new(Info)
	}

	return &Checker{
		conf:   conf,
		fset:   fset,
		pkg:    pkg,
		Info:   info,
		objMap: make(map[Object]*declInfo),
	}
}
```

```go
// Files checks the provided files as part of the checker's package.
func (check *Checker) Files(files []*ast.File) error { return check.checkFiles(files) }
```

```go
func (check *Checker) checkFiles(files []*ast.File) (err error) {
	defer check.handleBailout(&err)

	check.initFiles(files)

	check.collectObjects()

	check.packageObjects(check.resolveOrder())

	check.functionBodies()

	check.initOrder()

	if !check.conf.DisableUnusedImportCheck {
		check.unusedImports()
	}

	// perform delayed checks
	for _, f := range check.delayed {
		f()
	}

	check.recordUntyped()

	check.pkg.complete = true
	return
}
```

Next: [check.initFiles(files)](./check_initFiles.md)
