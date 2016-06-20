ast.GenDecl
===========

A `GenDecl` node (generic declaration node) represents an import, constant, type or variable declaration.  
A valid `Lparen` position (`Lparen.Line` > 0) indicates a parenthesized declaration.

Relationship between `Tok` value and Specs element type:

| Tok            | spec                                 |
|----------------|--------------------------------------|
| `token.IMPORT` | [`*ast.ImportSpec`](./ImportSpec.md) |
| `token.CONST`  | [`*ast.ValueSpec`](./ValueSpec.md)   |
| `token.TYPE`   | [`*ast.TypeSpec`](./TypeSpec.md)     |
| `token.VAR`    | [`*ast.ValueSpec`](./ValueSpec.md)   |

```go
type GenDecl struct {
	Doc    *ast.CommentGroup // associated documentation; or nil
	TokPos token.Pos         // position of Tok
	Tok    token.Token       // IMPORT, CONST, TYPE, VAR
	Lparen token.Pos         // position of '(', if any
	Specs  []ast.Spec
	Rparen token.Pos // position of ')', if any
}
```

| Method | Type                                                                   |
|--------|------------------------------------------------------------------------|
| Doc    | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| TokPos | [token.Pos (godoc.org)](https://godoc.org/go/token#Pos)                |
| Tok    | [token.Token (godoc.org)](https://godoc.org/go/token#Token)            |
| Lparen | [token.Pos (godoc.org)](https://godoc.org/go/token#Pos)                |
| Specs  | [[]*ast.Spec](./Spec.md)                                               |
| Rparen | [token.Pos (godoc.org)](https://godoc.org/go/token#Pos)                |

### Method

```go
func (x *GenDecl) End() token.Pos
```

```go
func (x *GenDecl) Pos() token.Pos
```
