ast.FuncDecl
============

A `FuncDecl` node represents a function declaration.

```go
type FuncDecl struct {
	Doc  *ast.CommentGroup // associated documentation; or nil
	Recv *ast.FieldList    // receiver (methods); or nil (functions)
	Name *ast.Ident        // function/method name
	Type *ast.FuncType     // function signature: parameters, results, and position of "func" keyword
	Body *ast.BlockStmt    // function body; or nil (forward declaration)
}
```

| Method | Type                                                                   |
|--------|------------------------------------------------------------------------|
| Doc    | [*ast.CommentGroup (godoc.org)](https://godoc.org/go/ast#CommentGroup) |
| Recv   | [*ast.FieldList](./FieldList.md)                                       |
| Name   | [*ast.Ident](./Ident.md)                                               |
| Type   | [*ast.FuncType](./FuncType.md)                                         |
| Body   | [*ast.BlockStmt](./BlockStmt.md)                                       |

### Method

```go
func (x *FuncDecl) End() token.Pos
```

```go
func (x *FuncDecl) Pos() token.Pos
```

### Sample

```go
func main() {
	fset := token.NewFileSet()
	f, err := parser.ParseFile(fset, "hello.go", helloFile, parser.ParseComments)
	if err != nil {
		log.Fatal(err) // parse error
	}

	conf := types.Config{Importer: importer.Default()}
	pkg, err := conf.Check("cmd/hello", fset, []*ast.File{f}, nil)
	if err != nil {
		log.Fatal(err) // type error
	}

	// Each comment contains a name.
	// Look up that name in the innermost scope enclosing the comment.
	for _, comment := range f.Comments {
		pos := comment.Pos()
		name := strings.TrimSpace(comment.Text())
		fmt.Printf("At %s,\t%q = ", fset.Position(pos), name)
		inner := pkg.Scope().Innermost(pos)
		if _, obj := inner.LookupParent(name, pos); obj != nil {
			fmt.Println(obj)
		} else {
			fmt.Println("not found")
		}
	}
}
```

```go
4: *ast.FuncDecl {
.  Name: *ast.Ident {
.  .  NamePos: ./cmd/lookup/lookup.go:40:6
.  .  Name: "main"
.  .  Obj: *ast.Object {
.  .  .  Kind: func
.  .  .  Name: "main"
.  .  .  Decl: *(obj @ 239)
.  .  }
.  }
.  Type: *ast.FuncType {
.  .  Func: ./cmd/lookup/lookup.go:40:1
.  .  Params: *ast.FieldList {
.  .  .  Opening: ./cmd/lookup/lookup.go:40:10
.  .  .  Closing: ./cmd/lookup/lookup.go:40:11
.  .  }
.  }
.  Body: *ast.BlockStmt {
.  .  Lbrace: ./cmd/lookup/lookup.go:40:13
.  .  List: []ast.Stmt (len = 7) {
.  .  .  0: *ast.AssignStmt {
.  .  .  .  Lhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:2
.  .  .  .  .  .  Name: "fset"
.  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  Name: "fset"
.  .  .  .  .  .  .  Decl: *(obj @ 259)
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  TokPos: ./cmd/lookup/lookup.go:41:7
.  .  .  .  Tok: :=
.  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:10
.  .  .  .  .  .  .  .  Name: "token"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:16
.  .  .  .  .  .  .  .  Name: "NewFileSet"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:41:26
.  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:41:27
.  .  .  .  .  }
.  .  .  .  }
.  .  .  }
.  .  .  1: *ast.AssignStmt {
.  .  .  .  Lhs: []ast.Expr (len = 2) {
.  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:2
.  .  .  .  .  .  Name: "f"
.  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  Name: "f"
.  .  .  .  .  .  .  Decl: *(obj @ 291)
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:5
.  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  .  Decl: *(obj @ 291)
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  TokPos: ./cmd/lookup/lookup.go:42:9
.  .  .  .  Tok: :=
.  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:12
.  .  .  .  .  .  .  .  Name: "parser"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:19
.  .  .  .  .  .  .  .  Name: "ParseFile"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:42:28
.  .  .  .  .  .  Args: []ast.Expr (len = 4) {
.  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:29
.  .  .  .  .  .  .  .  Name: "fset"
.  .  .  .  .  .  .  .  Obj: *(obj @ 264)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  1: *ast.BasicLit {
.  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:42:35
.  .  .  .  .  .  .  .  Kind: STRING
.  .  .  .  .  .  .  .  Value: "\"hello.go\""
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  2: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:47
.  .  .  .  .  .  .  .  Name: "helloFile"
.  .  .  .  .  .  .  .  Obj: *(obj @ 220)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  3: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:58
.  .  .  .  .  .  .  .  .  Name: "parser"
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:65
.  .  .  .  .  .  .  .  .  Name: "ParseComments"
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:42:78
.  .  .  .  .  }
.  .  .  .  }
.  .  .  }
.  .  .  2: *ast.IfStmt {
.  .  .  .  If: ./cmd/lookup/lookup.go:43:2
.  .  .  .  Cond: *ast.BinaryExpr {
.  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:43:5
.  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  Obj: *(obj @ 305)
.  .  .  .  .  }
.  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:43:9
.  .  .  .  .  Op: !=
.  .  .  .  .  Y: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:43:12
.  .  .  .  .  .  Name: "nil"
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  Body: *ast.BlockStmt {
.  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:43:16
.  .  .  .  .  List: []ast.Stmt (len = 1) {
.  .  .  .  .  .  0: *ast.ExprStmt {
.  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:3
.  .  .  .  .  .  .  .  .  .  Name: "log"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:7
.  .  .  .  .  .  .  .  .  .  Name: "Fatal"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:44:12
.  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:13
.  .  .  .  .  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:44:16
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:45:2
.  .  .  .  }
.  .  .  }
.  .  .  3: *ast.AssignStmt {
.  .  .  .  Lhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:2
.  .  .  .  .  .  Name: "conf"
.  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  Name: "conf"
.  .  .  .  .  .  .  Decl: *(obj @ 405)
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  TokPos: ./cmd/lookup/lookup.go:47:7
.  .  .  .  Tok: :=
.  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.CompositeLit {
.  .  .  .  .  .  Type: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:10
.  .  .  .  .  .  .  .  Name: "types"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:16
.  .  .  .  .  .  .  .  Name: "Config"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:47:22
.  .  .  .  .  .  Elts: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  0: *ast.KeyValueExpr {
.  .  .  .  .  .  .  .  Key: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:23
.  .  .  .  .  .  .  .  .  Name: "Importer"
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Colon: ./cmd/lookup/lookup.go:47:31
.  .  .  .  .  .  .  .  Value: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:33
.  .  .  .  .  .  .  .  .  .  .  Name: "importer"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:42
.  .  .  .  .  .  .  .  .  .  .  Name: "Default"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:47:49
.  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:47:50
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:47:51
.  .  .  .  .  }
.  .  .  .  }
.  .  .  }
.  .  .  4: *ast.AssignStmt {
.  .  .  .  Lhs: []ast.Expr (len = 2) {
.  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:2
.  .  .  .  .  .  Name: "pkg"
.  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  Name: "pkg"
.  .  .  .  .  .  .  Decl: *(obj @ 460)
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:7
.  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  Obj: *(obj @ 305)
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  TokPos: ./cmd/lookup/lookup.go:48:11
.  .  .  .  Tok: :=
.  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:14
.  .  .  .  .  .  .  .  Name: "conf"
.  .  .  .  .  .  .  .  Obj: *(obj @ 410)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:19
.  .  .  .  .  .  .  .  Name: "Check"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:48:24
.  .  .  .  .  .  Args: []ast.Expr (len = 4) {
.  .  .  .  .  .  .  0: *ast.BasicLit {
.  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:48:25
.  .  .  .  .  .  .  .  Kind: STRING
.  .  .  .  .  .  .  .  Value: "\"cmd/hello\""
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:38
.  .  .  .  .  .  .  .  Name: "fset"
.  .  .  .  .  .  .  .  Obj: *(obj @ 264)
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  2: *ast.CompositeLit {
.  .  .  .  .  .  .  .  Type: *ast.ArrayType {
.  .  .  .  .  .  .  .  .  Lbrack: ./cmd/lookup/lookup.go:48:44
.  .  .  .  .  .  .  .  .  Elt: *ast.StarExpr {
.  .  .  .  .  .  .  .  .  .  Star: ./cmd/lookup/lookup.go:48:46
.  .  .  .  .  .  .  .  .  .  X: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:47
.  .  .  .  .  .  .  .  .  .  .  .  Name: "ast"
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:51
.  .  .  .  .  .  .  .  .  .  .  .  Name: "File"
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:48:55
.  .  .  .  .  .  .  .  Elts: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:56
.  .  .  .  .  .  .  .  .  .  Name: "f"
.  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 296)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:48:57
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  3: *ast.Ident {
.  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:60
.  .  .  .  .  .  .  .  Name: "nil"
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:48:63
.  .  .  .  .  }
.  .  .  .  }
.  .  .  }
.  .  .  5: *ast.IfStmt {
.  .  .  .  If: ./cmd/lookup/lookup.go:49:2
.  .  .  .  Cond: *ast.BinaryExpr {
.  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:49:5
.  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  Obj: *(obj @ 305)
.  .  .  .  .  }
.  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:49:9
.  .  .  .  .  Op: !=
.  .  .  .  .  Y: *ast.Ident {
.  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:49:12
.  .  .  .  .  .  Name: "nil"
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  Body: *ast.BlockStmt {
.  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:49:16
.  .  .  .  .  List: []ast.Stmt (len = 1) {
.  .  .  .  .  .  0: *ast.ExprStmt {
.  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:3
.  .  .  .  .  .  .  .  .  .  Name: "log"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:7
.  .  .  .  .  .  .  .  .  .  Name: "Fatal"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:50:12
.  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:13
.  .  .  .  .  .  .  .  .  .  Name: "err"
.  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:50:16
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:51:2
.  .  .  .  }
.  .  .  }
.  .  .  6: *ast.RangeStmt {
.  .  .  .  For: ./cmd/lookup/lookup.go:55:2
.  .  .  .  Key: *ast.Ident {
.  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:6
.  .  .  .  .  Name: "_"
.  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  Kind: var
.  .  .  .  .  .  Name: "_"
.  .  .  .  .  .  Decl: *ast.AssignStmt {
.  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
.  .  .  .  .  .  .  .  0: *(obj @ 589)
.  .  .  .  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:9
.  .  .  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 595)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:55:17
.  .  .  .  .  .  .  Tok: :=
.  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.UnaryExpr {
.  .  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:55:20
.  .  .  .  .  .  .  .  .  Op: range
.  .  .  .  .  .  .  .  .  X: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:26
.  .  .  .  .  .  .  .  .  .  .  Name: "f"
.  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 296)
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:28
.  .  .  .  .  .  .  .  .  .  .  Name: "Comments"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  }
.  .  .  .  Value: *(obj @ 598)
.  .  .  .  TokPos: ./cmd/lookup/lookup.go:55:17
.  .  .  .  Tok: :=
.  .  .  .  X: *(obj @ 614)
.  .  .  .  Body: *ast.BlockStmt {
.  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:55:37
.  .  .  .  .  List: []ast.Stmt (len = 5) {
.  .  .  .  .  .  0: *ast.AssignStmt {
.  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:3
.  .  .  .  .  .  .  .  .  Name: "pos"
.  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  Name: "pos"
.  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 637)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:56:7
.  .  .  .  .  .  .  Tok: :=
.  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:10
.  .  .  .  .  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 601)
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:18
.  .  .  .  .  .  .  .  .  .  .  Name: "Pos"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:56:21
.  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:56:22
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  1: *ast.AssignStmt {
.  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:3
.  .  .  .  .  .  .  .  .  Name: "name"
.  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  Name: "name"
.  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 670)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:57:8
.  .  .  .  .  .  .  Tok: :=
.  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:11
.  .  .  .  .  .  .  .  .  .  .  Name: "strings"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:19
.  .  .  .  .  .  .  .  .  .  .  Name: "TrimSpace"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:57:28
.  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:29
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
.  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 601)
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:37
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Text"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:57:41
.  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:57:42
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:57:43
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  2: *ast.ExprStmt {
.  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:3
.  .  .  .  .  .  .  .  .  .  Name: "fmt"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:7
.  .  .  .  .  .  .  .  .  .  Name: "Printf"
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:58:13
.  .  .  .  .  .  .  .  Args: []ast.Expr (len = 3) {
.  .  .  .  .  .  .  .  .  0: *ast.BasicLit {
.  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:58:14
.  .  .  .  .  .  .  .  .  .  Kind: STRING
.  .  .  .  .  .  .  .  .  .  Value: "\"At %s,\\t%q = \""
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  1: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:31
.  .  .  .  .  .  .  .  .  .  .  .  Name: "fset"
.  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 264)
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:36
.  .  .  .  .  .  .  .  .  .  .  .  Name: "Position"
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:58:44
.  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:45
.  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
.  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:58:48
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  2: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:51
.  .  .  .  .  .  .  .  .  .  Name: "name"
.  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 675)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:58:55
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  3: *ast.AssignStmt {
.  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:3
.  .  .  .  .  .  .  .  .  Name: "inner"
.  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  Name: "inner"
.  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 772)
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:59:9
.  .  .  .  .  .  .  Tok: :=
.  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:12
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pkg"
.  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 465)
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:16
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Scope"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:59:21
.  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:59:22
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:24
.  .  .  .  .  .  .  .  .  .  .  Name: "Innermost"
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:59:33
.  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:34
.  .  .  .  .  .  .  .  .  .  .  Name: "pos"
.  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:59:37
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  .  4: *ast.IfStmt {
.  .  .  .  .  .  .  If: ./cmd/lookup/lookup.go:60:3
.  .  .  .  .  .  .  Init: *ast.AssignStmt {
.  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
.  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:6
.  .  .  .  .  .  .  .  .  .  Name: "_"
.  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  .  Name: "_"
.  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 825)
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:9
.  .  .  .  .  .  .  .  .  .  Name: "obj"
.  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
.  .  .  .  .  .  .  .  .  .  .  Kind: var
.  .  .  .  .  .  .  .  .  .  .  Name: "obj"
.  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 825)
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:60:13
.  .  .  .  .  .  .  .  Tok: :=
.  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:16
.  .  .  .  .  .  .  .  .  .  .  .  Name: "inner"
.  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 777)
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:22
.  .  .  .  .  .  .  .  .  .  .  .  Name: "LookupParent"
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:60:34
.  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 2) {
.  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:35
.  .  .  .  .  .  .  .  .  .  .  .  Name: "name"
.  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 675)
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  1: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:41
.  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
.  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:60:44
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Cond: *ast.BinaryExpr {
.  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:47
.  .  .  .  .  .  .  .  .  Name: "obj"
.  .  .  .  .  .  .  .  .  Obj: *(obj @ 839)
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:60:51
.  .  .  .  .  .  .  .  Op: !=
.  .  .  .  .  .  .  .  Y: *ast.Ident {
.  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:54
.  .  .  .  .  .  .  .  .  Name: "nil"
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Body: *ast.BlockStmt {
.  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:60:58
.  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
.  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:4
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fmt"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:8
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Println"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:61:15
.  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:16
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "obj"
.  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 839)
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:61:19
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:62:3
.  .  .  .  .  .  .  }
.  .  .  .  .  .  .  Else: *ast.BlockStmt {
.  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:62:10
.  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
.  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
.  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
.  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
.  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:63:4
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fmt"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
.  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:63:8
.  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Println"
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:63:15
.  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
.  .  .  .  .  .  .  .  .  .  .  .  0: *ast.BasicLit {
.  .  .  .  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:63:16
.  .  .  .  .  .  .  .  .  .  .  .  .  Kind: STRING
.  .  .  .  .  .  .  .  .  .  .  .  .  Value: "\"not found\""
.  .  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
.  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:63:27
.  .  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  }
.  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:64:3
.  .  .  .  .  .  .  }
.  .  .  .  .  .  }
.  .  .  .  .  }
.  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:65:2
.  .  .  .  }
.  .  .  }
.  .  }
.  .  Rbrace: ./cmd/lookup/lookup.go:66:1
.  }
}
```
