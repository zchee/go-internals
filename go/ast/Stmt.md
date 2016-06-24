ast.Stmt
========

All statement nodes implement the `Stmt` interface.

```go
type Stmt interface {
	Node
	// contains filtered or unexported methods
}
```

### Type Switch

-	`ast.Stmt`
	-	[*ast.BadStmt](./BadStmt.md)
	-	[*ast.DeclStmt](./DeclStmt.md)
	-	[*ast.EmptyStmt](./EmptyStmt.md)
	-	[*ast.LabeledStmt](./LabeledStmt.md)
	-	[*ast.ExprStmt](./ExprStmt.md)
	-	[*ast.SendStmt](./SendStmt.md)
	-	[*ast.IncDecStmt](./IncDecStmt.md)
	-	[*ast.AssignStmt](./AssignStmt.md)
	-	[*ast.GoStmt](./GoStmt.md)
	-	[*ast.DeferStmt](./DeferStmt.md)
	-	[*ast.ReturnStmt](./ReturnStmt.md)
	-	[*ast.BranchStmt](./BranchStmt.md)
	-	[*ast.BlockStmt](./BlockStmt.md)
	-	[*ast.IfStmt](./IfStmt.md)
	-	[*ast.CaseClause](./CaseClause.md)
	-	[*ast.SwitchStmt](./SwitchStmt.md)
	-	[*ast.TypeSwitchStmt](./TypeSwitchStmt.md)
	-	[*ast.CommClause](./CommClause.md)
	-	[*ast.SelectStmt](./SelectStmt.md)
	-	[*ast.ForStmt](./ForStmt.md)
	-	[*ast.RangeStmt](./RangeStmt.md)
