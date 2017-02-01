ast.Spec
========

The `Spec` type stands for any of `*ast.ImportSpec`, `*ast.ValueSpec`, and `*ast.TypeSpec`.

```go
type Spec interface {
	ast.Node
	// contains filtered or unexported methods
}
```

ast.ImportSpec
--------------

An `ImportSpec` node represents a single package import.

```go
type ImportSpec struct {
	Doc     *ast.CommentGroup // associated documentation; or nil
	Name    *ast.Ident        // local package name (including "."); or nil
	Path    *ast.BasicLit     // import path
	Comment *ast.CommentGroup // line comments; or nil
	EndPos  token.Pos         // end of spec (overrides Path.Pos if nonzero)
}
```

| Method  | Type                                                                   |
|---------|------------------------------------------------------------------------|
| Doc     | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| Name    | [*ast.Ident](./Ident.md)                                               |
| Path    | [*ast.BasicLit](./BasicLit.md)                                         |
| Comment | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| EndPos  | [token.Pos (godoc.org)](https://godoc.org/go/token#Pos)                |

### Method

```go
func (x *ImportSpec) End() token.Pos
```

```go
func (x *ImportSpec) Pos() token.Pos
```

`Pos` and `End` implementations for spec nodes.

### Syntax Tree

-	`*ast.ImportSpec`
	-	Path: `*ast.BasicLit`
		-	ValuePos: string
		-	Kind: string
		-	Value: string
	-	EndPos: string

### Sample

```go
import (
	"fmt"
)
```

```go
0: *ast.ImportSpec {
.  Path: *ast.BasicLit {
.  .  ValuePos: ./cmd/lookup/lookup.go:4:2
.  .  Kind: STRING
.  .  Value: "\"fmt\""
.  }
.  EndPos: -
}
```

ast.ValueSpec
-------------

A `ValueSpec` node represents a constant or variable declaration (`ast.ConstSpec` or `ast.VarSpec` production).

```go
type ValueSpec struct {
	Doc     *ast.CommentGroup // associated documentation; or nil
	Names   []*ast.Ident      // value names (len(Names) > 0)
	Type    ast.Expr          // value type; or nil
	Values  []ast.Expr        // initial values; or nil
	Comment *ast.CommentGroup // line comments; or nil
}
```

| Method  | Type                                                                   |
|---------|------------------------------------------------------------------------|
| Doc     | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| Names   | [[]*ast.Ident](./Ident.md)                                             |
| Type    | [*ast.Expr](./Expr.md)                                                 |
| Value   | [[]*ast.Expr](./Expr.md)                                               |
| Comment | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |

### Method

```go
func (x *ValueSpec) End() token.Pos
```

```go
func (x *ValueSpec) Pos() token.Pos
```

### Syntax Tree

-	`*ast.ValueSpec`
	-	Names: `[]*ast.Ident`
		-	NamePos: string
		-	Name: string
		-	Obj: `*ast.Object`
	-	Values: `[]ast.Expr`
		-	ValuePos: string
		-	Kind: string
		-	Value: string

### Sample

`Const`

```go
const hello = `
package main

import "fmt"

// append
func main() {
        // fmt
        fmt.Println("Hello, world")
        // main
        main, x := 1, 2
        // main
        print(main, x)
        // x
}
// x
`
```

```go
0: *ast.ValueSpec {
.  Names: []*ast.Ident (len = 1) {
.  .  0: *ast.Ident {
.  .  .  NamePos: ./cmd/lookup/lookup.go:20:7
.  .  .  Name: "hello"
.  .  .  Obj: *ast.Object {
.  .  .  .  Kind: const
.  .  .  .  Name: "hello"
.  .  .  .  Decl: *(obj @ 186)
.  .  .  .  Data: 0
.  .  .  }
.  .  }
.  }
.  Values: []ast.Expr (len = 1) {
.  .  0: *ast.BasicLit {
.  .  .  ValuePos: ./cmd/lookup/lookup.go:20:15
.  .  .  Kind: STRING
.  .  .  Value: "`\npackage main\n\nimport..."
.  .  }
.  }
}
```

`Var`

```go
var helloFile = hello
```

```go
0: *ast.ValueSpec {
.  Names: []*ast.Ident (len = 1) {
.  .  0: *ast.Ident {
.  .  .  NamePos: ./cmd/lookup/lookup.go:38:5
.  .  .  Name: "helloFile"
.  .  .  Obj: *ast.Object {
.  .  .  .  Kind: var
.  .  .  .  Name: "helloFile"
.  .  .  .  Decl: *(obj @ 215)
.  .  .  .  Data: 0
.  .  .  }
.  .  }
.  }
.  Values: []ast.Expr (len = 1) {
.  .  0: *ast.Ident {
.  .  .  NamePos: ./cmd/lookup/lookup.go:38:17
.  .  .  Name: "hello"
.  .  .  Obj: *(obj @ 191)
.  .  }
.  }
}
```

ast.TypeSpec
------------

A `TypeSpec` node represents a type declaration (`ast.TypeSpec` production).

```go
type TypeSpec struct {
	Doc     *ast.CommentGroup // associated documentation; or nil
	Name    *ast.Ident        // type name
	Type    ast.Expr          // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
	Comment *ast.CommentGroup // line comments; or nil
}
```

| Method  | Type                                                                   |
|---------|------------------------------------------------------------------------|
| Doc     | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| Name    | [*ast.Ident](./Ident.md)                                               |
| Type    | [ast.Expr](./Expr.md)                                                 |
| Comment | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |

### Method

```go
func (x *TypeSpec) End() token.Pos
```

```go
func (x *TypeSpec) Pos() token.Pos
```

### Sample

```go
type Lookup struct {
	Target  string
	Types   map[string]types.Type
	comment *ast.CommentGroup
}
```

```go
0: *ast.TypeSpec {
.  Name: *ast.Ident {
.  .  NamePos: ./cmd/lookup/lookup.go:14:6
.  .  Name: "Lookup"
.  .  Obj: *ast.Object {
.  .  .  Kind: type
.  .  .  Name: "Lookup"
.  .  .  Decl: *(obj @ 84)
.  .  }
.  }
.  Type: *ast.StructType {
.  .  Struct: ./cmd/lookup/lookup.go:14:13
.  .  Fields: *ast.FieldList {
.  .  .  Opening: ./cmd/lookup/lookup.go:14:20
.  .  .  List: []*ast.Field (len = 3) {
.  .  .  .  0: *ast.Field {
.  .  .  .  .  Names: []*ast.Ident (len = 1) {
.  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:15:2
.  .  .  .  .  .  .  Name: "Target"
.  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  Name: "Target"
.  .  .  .  .  .  .  .  Decl: *(obj @ 99)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Type: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:15:10
.  .  .  .  .  .  Name: "string"
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  1: *ast.Field {
.  .  .  .  .  Names: []*ast.Ident (len = 1) {
.  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:2
.  .  .  .  .  .  .  Name: "Types"
.  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  Name: "Types"
.  .  .  .  .  .  .  .  Decl: *(obj @ 116)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Type: *ast.MapType {
.  .  .  .  .  .  Map: ./cmd/lookup/lookup.go:16:10
.  .  .  .  .  .  Key: *ast.Ident {
.  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:14
.  .  .  .  .  .  .  Name: "string"
.  .  .  .  .  .  }
.  .  .  .  .  .  Value: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:21
.  .  .  .  .  .  .  .  Name: "types"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:27
.  .  .  .  .  .  .  .  Name: "Type"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  2: *ast.Field {
.  .  .  .  .  Names: []*ast.Ident (len = 1) {
.  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:2
.  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  .  Decl: *(obj @ 146)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Type: *ast.StarExpr {
.  .  .  .  .  .  Star: ./cmd/lookup/lookup.go:17:10
.  .  .  .  .  .  X: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:11
.  .  .  .  .  .  .  .  Name: "ast"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:15
.  .  .  .  .  .  .  .  Name: "CommentGroup"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  }
.  .  .  Closing: ./cmd/lookup/lookup.go:18:1
.  .  }
.  .  Incomplete: false
.  }
}
```
