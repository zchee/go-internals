ast.Object
==========

An `Object` describes a named language entity such as a  
`package`, `constant`, `type`, `variable`, `function` (incl. `methods`), or `label`.

```go
type Object struct {
	Kind ast.ObjKind
	Name string      // declared name
	Decl interface{} // corresponding Field, XxxSpec, FuncDecl, LabeledStmt, AssignStmt, Scope; or nil
	Data interface{} // object-specific data; or nil
	Type interface{} // placeholder for type information; may be nil
}
```

| Method | Type                         |
|--------|------------------------------|
| Kind   | [*ast.ObjKind](./ObjKind.md) |
| Name   | `string`                     |
| Decl   | `interface{}`                |
| Data   | `interface{}`                |
| Type   | `interface{}`                |

### Type Switch

-	`ast.Object.Decl`
	-	[`ast.Field`](./Field.md)
	-	[`ast.ImportSpec`](./ImportSpec.md)
	-	[`ast.TypeSpec`](./TypeSpec.md)
	-	[`ast.ValueSpec`](./ValueSpec.md)
	-	[`ast.FuncDecl`](./FuncDecl.md)
	-	[`ast.LabeledStmt`](./LabeledStmt.md)
	-	[`ast.AssignStmt`](./AssignStmt.md)
	-	[`ast.Scope`](./Scope.md)

### Create

```go
func NewObj(kind ObjKind, name string) *Object
```

`NewObj` creates a new object of a given kind and name.

### Method

```go
func (obj *Object) Pos() token.Pos
```

`Pos` computes the source position of the declaration of an object name.  
The result may be an invalid position if it cannot be computed (`obj.Decl` may be `nil` or not correct).
