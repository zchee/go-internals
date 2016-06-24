ast.Expr
========

All expression nodes implement the `Expr` interface.

```go
type Expr interface {
	Node
	// contains filtered or unexported methods
}
```

### Type Switch

-	`*ast.Expr`
	-	[*ast.BadExpr](./BadExpr.md)
	-	[*ast.Ident](./Ident.md)
	-	[*ast.Ellipsis](./Ellipsis.md)
	-	[*ast.BasicLit](./BasicLit.md)
	-	[*ast.FuncLit](./FuncLit.md)
	-	[*ast.CompositeLit](./CompositeLit.md)
	-	[*ast.ParenExpr](./ParenExpr.md)
	-	[*ast.SelectorExpr](./SelectorExpr.md)
	-	[*ast.IndexExpr](./IndexExpr.md)
	-	[*ast.SliceExpr](./SliceExpr.md)
	-	[*ast.TypeAssertExpr](./TypeAssertExpr.md)
	-	[*ast.CallExpr](./CallExpr.md)
	-	[*ast.StarExpr](./StarExpr.md)
	-	[*ast.UnaryExpr](./UnaryExpr.md)
	-	[*ast.BinaryExpr](./BinaryExpr.md)
	-	[*ast.KeyValueExpr](./KeyValueExpr.md)
	-	[*ast.ArrayType](./ArrayType.md)
	-	[*ast.StructType](./StructType.md)
	-	[*ast.FuncType](./FuncType.md)
	-	[*ast.InterfaceType](./InterfaceType.md)
	-	[*ast.MapType](./MapType.md)
	-	[*ast.ChanType](./ChanType.md)
