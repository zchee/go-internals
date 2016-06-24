ast.File
========

A `File` node represents a Go source file.

The Comments list contains all comments in the source file in order of appearance,  
including the comments that are pointed to from other nodes via Doc and Comment fields.

```go
type File struct {
	Doc        *ast.CommentGroup   // associated documentation; or nil
	Package    token.Pos           // position of "package" keyword
	Name       *ast.Ident          // package name
	Decls      []ast.Decl          // top-level declarations; or nil
	Scope      *ast.Scope          // package scope (this file only)
	Imports    []*ast.ImportSpec   // imports in this file
	Unresolved []*ast.Ident        // unresolved identifiers in this file
	Comments   []*ast.CommentGroup // list of all comments in the source file
}
```

| Method     | Type                                                                   |
|------------|------------------------------------------------------------------------|
| Doc        | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| Package    | [token.Pos (godoc.org)](https://godoc.org/go/token#Pos)                |
| Name       | [*ast.Ident](./Ident.md)                                               |
| Decls      | [[]*ast.Decl](./Decl.md)                                               |
| Scope      | [*ast.Scope](./Scope.md)                                               |
| Imports    | [[]*ast.ImportSpec](./ImportSpec.md)                                   |
| Unresolved | [[]*ast.Ident](./Ident.md)                                             |
| Comments   | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |

### Create

```go
fset := token.NewFileSet()
f, err := parser.ParseFile(fset, "hello.go", helloFile, parser.Mode(0))
if err != nil {
	log.Fatal(err)
}
// f is *ast.File
```

```go
func MergePackageFiles(pkg *Package, mode MergeMode) *File
```

MergePackageFiles creates a file AST by merging the ASTs of the files belonging to a package.  
The mode flags control merging behavior.

### Method

```go
func (x *File) End() token.Pos
```

```go
func (x *File) Pos() token.Pos
```

### `*ast.File`

type: `*ast.File`

The all of root.

### `*ast.File.Package`

type: `string`

```go
Package: ./cmd/lookup/lookup.go:1:1
```

Position(Location) of the package of declaration.

### `*ast.File.Name`

type: `*ast.Ident`

```go
Name: *ast.Ident {
  NamePos: ./main.go:1:9
  Name: "main"
}
```

Package name and position of the package name of declaration.  
If **not** main file(`build.Package.IsCommand() == false`), `Name` is package name.

### `*ast.File.Decls`

type: `[]ast.Decl`

The main abstract syntax information of file.

| Kind   | type            |
|--------|-----------------|
| import | `*ast.GenDecl`  |
| const  | `*ast.GenDecl`  |
| var    | `*ast.GenDecl`  |
| func   | `*ast.FuncDecl` |

### `*ast.File.Scope`

type: `*ast.Scope`

```go
Scope: *ast.Scope {
   Objects: map[string]*ast.Object (len = 2) {
      "hello": *(obj @ 89)
      "main": *(obj @ 112)
   }
}
```

Objects scope.

func, var and const types object information.

### `*ast.File.Imports`

type: `*ast.ImportSpec`

Imported package information.

### `*ast.File.Unresolved`

type: `[]*ast.Ident`

?
