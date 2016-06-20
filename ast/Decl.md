ast.Decl
========

All declaration nodes implement the `Decl` interface.

```go
type Decl interface {
	Node
	// contains filtered or unexported methods
}
```

### Type Switch

-	`ast.Decl`
	-	[*ast.BadDecl](./BadDecl.md)
	-	[*ast.GenDecl](./GenDecl.md)
	-	[*ast.FuncDecl](./FuncDecl.md)
