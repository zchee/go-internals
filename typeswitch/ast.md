go/ast Type Switch
==================

Type switch syntax tree.

ast.Node
--------

<details>
 <summary>type list</summary>
 ```go
 // All expression nodes implement the Expr interface.
 type Expr interface {
 	Node
 	exprNode()
 }

 // All statement nodes implement the Stmt interface.
 type Stmt interface {
 	Node
 	stmtNode()
 }

 // All declaration nodes implement the Decl interface.
 type Decl interface {
 	Node
 	declNode()
 }
 ```
</details>

-	[ast.Expr](#astexpr)
-	[ast.Decl](#astdecl)
-	[ast.Stmt](#aststmt)

ast.Expr
--------

<details>
 <summary>type list</summary>
 ```go
 type (
 	// A BadExpr node is a placeholder for expressions containing
 	// syntax errors for which no correct expression nodes can be
 	// created.
 	//
 	BadExpr struct {
 	 From, To token.Pos // position range of bad expression
 	}

 	// An Ident node represents an identifier.
 	Ident struct {
 	 NamePos token.Pos // identifier position
 	 Name    string    // identifier name
 	 Obj     *Object   // denoted object; or nil
 	}

 	// An Ellipsis node stands for the "..." type in a
 	// parameter list or the "..." length in an array type.
 	//
 	Ellipsis struct {
 	 Ellipsis token.Pos // position of "..."
 	 Elt      Expr      // ellipsis element type (parameter lists only); or nil
 	}

 	// A BasicLit node represents a literal of basic type.
 	BasicLit struct {
 	 ValuePos token.Pos   // literal position
 	 Kind     token.Token // token.INT, token.FLOAT, token.IMAG, token.CHAR, or token.STRING
 	 Value    string      // literal string; e.g. 42, 0x7f, 3.14, 1e-9, 2.4i, 'a', '\x7f', "foo" or `\m\n\o`
 	}

 	// A FuncLit node represents a function literal.
 	FuncLit struct {
 	 Type *FuncType  // function type
 	 Body *BlockStmt // function body
 	}

 	// A CompositeLit node represents a composite literal.
 	CompositeLit struct {
 	 Type   Expr      // literal type; or nil
 	 Lbrace token.Pos // position of "{"
 	 Elts   []Expr    // list of composite elements; or nil
 	 Rbrace token.Pos // position of "}"
 	}

 	// A ParenExpr node represents a parenthesized expression.
 	ParenExpr struct {
 	 Lparen token.Pos // position of "("
 	 X      Expr      // parenthesized expression
 	 Rparen token.Pos // position of ")"
 	}

 	// A SelectorExpr node represents an expression followed by a selector.
 	SelectorExpr struct {
 	 X   Expr   // expression
 	 Sel *Ident // field selector
 	}

 	// An IndexExpr node represents an expression followed by an index.
 	IndexExpr struct {
 	 X      Expr      // expression
 	 Lbrack token.Pos // position of "["
 	 Index  Expr      // index expression
 	 Rbrack token.Pos // position of "]"
 	}

 	// An SliceExpr node represents an expression followed by slice indices.
 	SliceExpr struct {
 	 X      Expr      // expression
 	 Lbrack token.Pos // position of "["
 	 Low    Expr      // begin of slice range; or nil
 	 High   Expr      // end of slice range; or nil
 	 Max    Expr      // maximum capacity of slice; or nil
 	 Slice3 bool      // true if 3-index slice (2 colons present)
 	 Rbrack token.Pos // position of "]"
 	}

 	// A TypeAssertExpr node represents an expression followed by a
 	// type assertion.
 	//
 	TypeAssertExpr struct {
 	 X      Expr      // expression
 	 Lparen token.Pos // position of "("
 	 Type   Expr      // asserted type; nil means type switch X.(type)
 	 Rparen token.Pos // position of ")"
 	}

 	// A CallExpr node represents an expression followed by an argument list.
 	CallExpr struct {
 	 Fun      Expr      // function expression
 	 Lparen   token.Pos // position of "("
 	 Args     []Expr    // function arguments; or nil
 	 Ellipsis token.Pos // position of "...", if any
 	 Rparen   token.Pos // position of ")"
 	}

 	// A StarExpr node represents an expression of the form "*" Expression.
 	// Semantically it could be a unary "*" expression, or a pointer type.
 	//
 	StarExpr struct {
 	 Star token.Pos // position of "*"
 	 X    Expr      // operand
 	}

 	// A UnaryExpr node represents a unary expression.
 	// Unary "*" expressions are represented via StarExpr nodes.
 	//
 	UnaryExpr struct {
 	 OpPos token.Pos   // position of Op
 	 Op    token.Token // operator
 	 X     Expr        // operand
 	}

 	// A BinaryExpr node represents a binary expression.
 	BinaryExpr struct {
 	 X     Expr        // left operand
 	 OpPos token.Pos   // position of Op
 	 Op    token.Token // operator
 	 Y     Expr        // right operand
 	}

 	// A KeyValueExpr node represents (key : value) pairs
 	// in composite literals.
 	//
 	KeyValueExpr struct {
 	 Key   Expr
 	 Colon token.Pos // position of ":"
 	 Value Expr
 	}

 	// An ArrayType node represents an array or slice type.
 	ArrayType struct {
 	 Lbrack token.Pos // position of "["
 	 Len    Expr      // Ellipsis node for [...]T array types, nil for slice types
 	 Elt    Expr      // element type
 	}

 	// A StructType node represents a struct type.
 	StructType struct {
 	 Struct     token.Pos  // position of "struct" keyword
 	 Fields     *FieldList // list of field declarations
 	 Incomplete bool       // true if (source) fields are missing in the Fields list
 	}

 	// Pointer types are represented via StarExpr nodes.

 	// A FuncType node represents a function type.
 	FuncType struct {
 	 Func    token.Pos  // position of "func" keyword (token.NoPos if there is no "func")
 	 Params  *FieldList // (incoming) parameters; non-nil
 	 Results *FieldList // (outgoing) results; or nil
 	}

 	// An InterfaceType node represents an interface type.
 	InterfaceType struct {
 	 Interface  token.Pos  // position of "interface" keyword
 	 Methods    *FieldList // list of methods
 	 Incomplete bool       // true if (source) methods are missing in the Methods list
 	}

 	// A MapType node represents a map type.
 	MapType struct {
 	 Map   token.Pos // position of "map" keyword
 	 Key   Expr
 	 Value Expr
 	}

 	// A ChanType node represents a channel type.
 	ChanType struct {
 	 Begin token.Pos // position of "chan" keyword or "<-" (whichever comes first)
 	 Arrow token.Pos // position of "<-" (token.NoPos if there is no "<-")
 	 Dir   ChanDir   // channel direction
 	 Value Expr      // value type
 	}
 )
 ```
</details>

-	[ast.Expr](../go/ast/Expr.md)
	-	[*ast.BadExpr](../go/ast/BadExpr.md)
	-	[*ast.BasicLit](../go/ast/BasicLit.md)
		-	Kind: [token.Token](https://godoc.org/go/token#Token)
			-	[token.INT](https://godoc.org/go/token#INT) // 12345
			-	[token.FLOAT](https://godoc.org/go/token#FLOAT) // 123.45
			-	[token.IMAG](https://godoc.org/go/token#IMAG) // 123.45i
			-	[token.CHAR](https://godoc.org/go/token#CHAR) // 'a'
			-	[token.STRING](https://godoc.org/go/token#STRING) // "abc"
	-	[*ast.BinaryExpr](../go/ast/BinaryExpr.md)
		-	X: [ast.Expr](../go/ast/Expr.md) // left operand
		-	OpPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Op
		-	Op: [token.Token](https://godoc.org/go/token#Token) // operator
			-	`ast.ADD` +
			-	`ast.SUB` -
			-	`ast.MUL` \*
			-	`ast.QUO` /
			-	`ast.REM` %
			-	`ast.AND` &
			-	`ast.OR` |
			-	`ast.XOR` ^
			-	`ast.SHL` \<\<
			-	`ast.SHR` >>
			-	`ast.AND_NOT` &^
			-	`ast.ADD_ASSIGN` +=
			-	`ast.SUB_ASSIGN` -=
			-	`ast.MUL_ASSIGN` *=
			-	`ast.QUO_ASSIGN` /=
			-	`ast.REM_ASSIGN` %=
			-	`ast.AND_ASSIGN` &=
			-	`ast.OR_ASSIGN` |=
			-	`ast.XOR_ASSIGN` ^=
			-	`ast.SHL_ASSIGN` \<<=
			-	`ast.SHR_ASSIGN` >>=
			-	`ast.AND_NOT_ASSIGN` &^=
			-	`ast.LAND` &&
			-	`ast.LOR` ||
			-	`ast.ARROW` <-
			-	`ast.INC` ++
			-	`ast.DEC` --
			-	`ast.EQL` ==
			-	`ast.LSS` \<
			-	`ast.GTR` >
			-	`ast.ASSIGN` =
			-	`ast.NOT` !
			-	`ast.NEQ` !=
			-	`ast.LEQ` <=
			-	`ast.GEQ` >=
			-	`ast.DEFINE` :=
			-	`ast.ELLIPSIS` ...
			-	`ast.LPAREN` (
			-	`ast.LBRACK` \[
			-	`ast.LBRACE` {
			-	`ast.COMMA` ,
			-	`ast.PERIOD` .
			-	`ast.RPAREN` )
			-	`ast.RBRACK` ]
			-	`ast.RBRACE` }
			-	`ast.SEMICOLON` ;
			-	`ast.COLON` :
		-	Y: [ast.Expr](../go/ast/Expr.md) // right operand
	-	[*ast.CallExpr](../go/ast/CallExpr.md)
		-	Fun: [ast.Expr](../go/ast.Expr.md) // function expression
			-	[*ast.Ident](../go/ast/Ident.md)
			-	[*ast.SelectorExpr](../go/ast/SelectorExpr.md)
		-	Args: [\[ \]ast.Expr](../go/ast.Expr.md) // function arguments; or nil
			-	[*ast.BasicLit](../go/ast/BasicLit.md)
			-	[*ast.CallExpr](../go/ast/CallExpr.md)
			-	[*ast.Ident](../go/ast/Ident.md)
			-	[*ast.MapType](../go/ast/MapType.md)
	-	[*ast.CompositeLit](../go/ast/CompositeLit.md)
		-	Type: [ast.Expr](../go/ast.Expr.md) // literal type; or nil
			-	[*ast.ArrayType](../go/ast/ArrayType.md)
			-	[*ast.MapType](../go/ast/MapType.md)
			-	[*ast.StructType](../go/ast/StructType.md)
			-	[*ast.Ident](../go/ast/Ident.md)
		-	Lbrace: [token.Pos](https://godoc.org/go/token#Pos) // position of "{"
		-	Elts [\[\]ast.Expr](../go/ast.Expr.md) // list of composite elements; or nil
			-	[*ast.KeyValueExpr](../go/ast/KeyValueExpr.md)
			-	[*ast.CompositeLit](../go/ast/CompositeLit.md)
			-	[*ast.StarExpr](../go/ast/StarExpr.md)
		-	Rbrace: [token.Pos](https://godoc.org/go/token#Pos) // position of "}"
	-	[*ast.Ellipsis](../go/ast/Ellipsis.md)
		-	Elt: [ast.Expr](../go/ast/Expr.md) // ellipsis element type (parameter lists only); or nil
	-	[*ast.FuncLit](../go/ast/FuncLit.md)
		-	Type: [*ast.FuncType](../go/ast/FuncType.md)
		-	Body: [*ast.BlockStmt](../go/ast/BlockStmt.md)
	-	[*ast.Ident](../go/ast/Ident.md)
		-	Obj: [*ast.Object](../go/ast/Object.md) // denoted object; or nil
			-	Kind: [ast.ObjKind](../go/ast/ObjKind.md)
				-	[ast.Bad](../go/ast/ObjKind.md#Bad) // for error handling
				-	[ast.Pkg](../go/ast/ObjKind.md#Pkg) // package
				-	[ast.Con](../go/ast/ObjKind.md#Con) // constant
				-	[ast.Typ](../go/ast/ObjKind.md#Typ) // type
				-	[ast.Var](../go/ast/ObjKind.md#Var) // variable
				-	[ast.Fun](../go/ast/ObjKind.md#Fun) // function or method
				-	[ast.Lbl](../go/ast/ObjKind.md#Lbl) // label
			-	Decl: `interface{}`
				-	[ast.Field](../go/ast/Field.md)
					-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
					-	Names: [*ast.Ident](../go/ast/Ident.md) // field/method/parameter names; or nil if anonymous field
					-	Type: [*ast.Expr](../go/ast/Expr.md) // field/method/parameter type
					-	Tag: [*ast.BasicLit](../go/ast/CommentGroup.md) // field tag; or nil
					-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
				-	[ast.ImportSpec](../go/ast/ImportSpec.md)
					-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](../go/ast/Ident.md) // local package name (including "."); or nil
					-	Path: [*ast.BasicLit](../go/ast/CommentGroup.md) // import path
					-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
					-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
				-	[ast.TypeSpec](../go/ast/TypeSpec.md)
					-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](../go/ast/Ident.md) // type name
					-	Type: [ast.Expr](../go/ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
						-	[*ast.Ident](../go/ast/Ident.md)
						-	[*ast.ParenExpr](../go/ast/ParenExpr.md)
						-	[*ast.SelectorExpr](../go/ast/SelectorExpr.md)
						-	[*ast.StarExpr](../go/ast/StarExpr.md)
						-	[*ast.ArrayType](../go/ast/ArrayType.md)
							-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
							-	Len: [ast.Expr](../go/ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
							-	Elt: [ast.Expr](../go/ast/Expr.md) // element type
						-	[*ast.ChanType](../go/ast/ChanType.md)
							-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
							-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
							-	Dir: [ChanDir](../go/ast/ChanDir.md) // channel direction
							-	Value: [ast.Expr](../go/ast/Expr.md) // value type
						-	[*ast.FuncType](../go/ast/FuncType.md)
							-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
							-	Params: [*ast.FieldList](../go/ast/FieldList.md) // (incoming) parameters; non-nil
							-	Results: [*ast.FieldList](../go/ast/FieldList.md) // (outgoing) results; or nil
						-	[*ast.InterfaceType](../go/ast/InterfaceType.md)
							-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
							-	Methods: [*ast.FieldList](../go/ast/FieldList.md) // list of methods
						-	[*ast.MapType](../go/ast/MapType.md)
							-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
							-	Key: [ast.Expr](../go/ast/Expr.md)
							-	Value: [ast.Expr](../go/ast/Expr.md)
						-	[*ast.StructType](../go/ast/StructType.md)
							-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
							-	Fields: [*ast.FieldList](../go/ast/FieldList.md) // list of field declarations
					-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
				-	[ast.ValueSpec](../go/ast/ValueSpec.md)
					-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](../go/ast/Ident.md) // value name (len(Names) > 0)
					-	Type: [ast.Expr](../go/ast/Expr.md) // value type; or nil
					-	Values: [\[\]ast.Expr](../go/ast/Expr.md) // initial value; or nil
					-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
				-	[ast.FuncDecl](../go/ast/FuncDecl.md)
					-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
					-	Recv: [*ast.FieldList](../go/ast/FieldList.md) // receiver (methods); or nil (functions)
					-	Name: [*ast.Ident](../go/ast/Ident.md) // function/method name
					-	Type: [*ast.FuncType](../go/ast/FuncType.md) // function signature: parameters, results, and position of "func" keyword
					-	Body: [*ast.BlockStmt](../go/ast/BlockStmt.md) // function body; or nil (forward declaration)
				-	[ast.LabeledStmt](../go/ast/LabeledStmt.md)
					-	Label: [*ast.Ident](../go/ast/Ident.md)
					-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
					-	Stmt: [ast.Stmt](../go/ast/Stmt.md)
				-	[ast.AssignStmt](../go/ast/AssignStmt.md)
					-	Lhs: [\[\]ast.Expr](../go/ast/Expr.md)
					-	TokPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Tok
					-	Tok: [token.Token](https://godoc.org/go/token#Token) // assignment token, DEFINE
					-	Rhs: [\[\]ast.Expr](../go/ast/Expr.md)
				-	[ast.Scope](../go/ast/Scope.md)
					-	Outer: [*ast.Scope](../go/ast/Scope.md)
					-	Objects: [map\[string\]*ast.Object](../go/ast/Object.md)
	-	[*ast.IndexExpr](../go/ast/IndexExpr.md)
		-	X: [ast.Expr](../go/ast/Expr.md) // expression
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Index: [ast.Expr](../go/ast/Expr.md) // index expression
		-	Y: [ast.Expr](../go/ast/Expr.md) // position of "\]"
	-	[*ast.KeyValueExpr](../go/ast/KeyValueExpr.md)
		-	Key: [ast.Expr](../go/ast/Expr.md)
		-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
		-	Value: [ast.Expr](../go/ast/Expr.md)
	-	[*ast.ParenExpr](../go/ast/ParenExpr.md)
		-	Lparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
		-	X: [ast.Expr](../go/ast/Expr.md) // parenthesized expression
		-	Rparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
	-	[*ast.SelectorExpr](../go/ast/SelectorExpr.md)
		-	X: [ast.Expr](../go/ast/Expr.md) // expression
		-	Sel: [*ast.Ident](../go/ast/Ident.md) // field selector
	-	[*ast.SliceExpr](../go/ast/SliceExpr.md)
		-	X: [ast.Expr](../go/ast/Expr.md) // expression
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Low: [ast.Expr](../go/ast/Expr.md) // begin of slice range; or nil
		-	High: [ast.Expr](../go/ast/Expr.md) // end of slice range; or nil
		-	Max: [ast.Expr](../go/ast/Expr.md) // maximum capacity of slice; or nil
		-	Rbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\]"
	-	[*ast.StarExpr](../go/ast/StarExpr.md)
		-	Star: [token.Pos](https://godoc.org/go/token#Pos) // position of "*"
		-	X: [ast.Expr](../go/ast/Expr.md) // operand
	-	[*ast.TypeAssertExpr](../go/ast/TypeAssertExpr.md)
		-	X: [ast.Expr](../go/ast/Expr.md) // expression
		-	Lparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
		-	Type: [ast.Expr](../go/ast/Expr.md) // asserted type; nil means type switch X.(type)
		-	Rparen: [token.Pos](https://godoc.org/go/token#Pos) // position of ")"
	-	[*ast.UnaryExpr](../go/ast/UnaryExpr.md)
		-	OpPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Op
		-	Op: [token.Pos](https://godoc.org/go/token#Token) // operator
		-	X: [ast.Expr](../go/ast/Expr.md) // operand
	-	[*ast.ArrayType](../go/ast/ArrayType.md)
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Len: [ast.Expr](../go/ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
		-	Elt: [ast.Expr](../go/ast/Expr.md) // element type
	-	[*ast.ChanType](../go/ast/ChanType.md)
		-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
		-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
		-	Dir: [ChanDir](../go/ast/ChanDir.md) // channel direction
		-	Value: [ast.Expr](../go/ast/Expr.md) // value type
	-	[*ast.FuncType](../go/ast/FuncType.md)
		-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
		-	Params: [*ast.FieldList](../go/ast/FieldList.md) // (incoming) parameters; non-nil
		-	Results: [*ast.FieldList](../go/ast/FieldList.md) // (outgoing) results; or nil
	-	[*ast.InterfaceType](../go/ast/InterfaceType.md)
		-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
		-	Methods: [*ast.FieldList](../go/ast/FieldList.md) // list of methods
	-	[*ast.MapType](../go/ast/MapType.md)
		-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
		-	Key: [ast.Expr](../go/ast/Expr.md)
		-	Value: [ast.Expr](../go/ast/Expr.md)
	-	[*ast.StructType](../go/ast/StructType.md)
		-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
		-	Fields: [*ast.FieldList](../go/ast/FieldList.md) // list of field declarations

ast.Decl
--------

<details>
 <summary>type list</summary>
 ```go
 type (
 	// A BadDecl node is a placeholder for declarations containing
 	// syntax errors for which no correct declaration nodes can be
 	// created.
 	//
 	BadDecl struct {
 	 From, To token.Pos // position range of bad declaration
 	}

 	// A GenDecl node (generic declaration node) represents an import,
 	// constant, type or variable declaration. A valid Lparen position
 	// (Lparen.Line > 0) indicates a parenthesized declaration.
 	//
 	// Relationship between Tok value and Specs element type:
 	//
 	//	token.IMPORT  *ImportSpec
 	//	token.CONST   *ValueSpec
 	//	token.TYPE    *TypeSpec
 	//	token.VAR     *ValueSpec
 	//
 	GenDecl struct {
 	 Doc    *CommentGroup // associated documentation; or nil
 	 TokPos token.Pos     // position of Tok
 	 Tok    token.Token   // IMPORT, CONST, TYPE, VAR
 	 Lparen token.Pos     // position of '(', if any
 	 Specs  []Spec
 	 Rparen token.Pos // position of ')', if any
 	}

 	// A FuncDecl node represents a function declaration.
 	FuncDecl struct {
 	 Doc  *CommentGroup // associated documentation; or nil
 	 Recv *FieldList    // receiver (methods); or nil (functions)
 	 Name *Ident        // function/method name
 	 Type *FuncType     // function signature: parameters, results, and position of "func" keyword
 	 Body *BlockStmt    // function body; or nil (forward declaration)
 	}
 )
 ```
</details>

-	[ast.Decl](../go/ast/Decl.md)
	-	[*ast.BadDecl](../go/ast/BadDecl.md)
	-	[*ast.GenDecl](../go/ast/GenDecl.md)
		-	Token: [token.Token](https://godoc.org/go/token#Token)
			-	[token.IMPORT](https://godoc.org/go/token#IMPORT)
			-	[token.CONST](https://godoc.org/go/token#CONST)
			-	[token.TYPE](https://godoc.org/go/token#TYPE)
			-	[token.VAR](https://godoc.org/go/token#VAR)
		-	Specs: [\[ \]ast.Specs](../go/ast/Spec.md)
			-	[ast.ImportSpec](../go/ast/ImportSpec.md)
				-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](../go/ast/Ident.md) // local package name (including "."); or nil
				-	Path: [*ast.BasicLit](../go/ast/CommentGroup.md) // import path
				-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
				-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
			-	[ast.TypeSpec](../go/ast/TypeSpec.md)
				-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](../go/ast/Ident.md) // type name
				-	Type: [ast.Expr](../go/ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
					-	[*ast.Ident](../go/ast/Ident.md)
					-	[*ast.ParenExpr](../go/ast/ParenExpr.md)
					-	[*ast.SelectorExpr](../go/ast/SelectorExpr.md)
					-	[*ast.StarExpr](../go/ast/StarExpr.md)
					-	[ast.ArrayType](../go/ast/ArrayType.md)
						-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
						-	Len: [ast.Expr](../go/ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
						-	Elt: [ast.Expr](../go/ast/Expr.md) // element type
					-	[ast.ChanType](../go/ast/ChanType.md)
						-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
						-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
						-	Dir: [ChanDir](../go/ast/ChanDir.md) // channel direction
						-	Value: [ast.Expr](../go/ast/Expr.md) // value type
					-	[ast.FuncType](../go/ast/FuncType.md)
						-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
						-	Params: [*ast.FieldList](../go/ast/FieldList.md) // (incoming) parameters; non-nil
						-	Results: [*ast.FieldList](../go/ast/FieldList.md) // (outgoing) results; or nil
					-	[ast.InterfaceType](../go/ast/InterfaceType.md)
						-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
						-	Methods: [*ast.FieldList](../go/ast/FieldList.md) // list of methods
					-	[ast.MapType](../go/ast/MapType.md)
						-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
						-	Key: [ast.Expr](../go/ast/Expr.md)
						-	Value: [ast.Expr](../go/ast/Expr.md)
					-	[ast.StructType](../go/ast/StructType.md)
						-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
						-	Fields: [*ast.FieldList](../go/ast/FieldList.md) // list of field declarations
				-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
			-	[ast.ValueSpec](../go/ast/ValueSpec.md)
				-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](../go/ast/Ident.md) // value name (len(Names) > 0)
				-	Type: [ast.Expr](../go/ast/Expr.md) // value type; or nil
				-	Values: [\[\]ast.Expr](../go/ast/Expr.md) // initial value; or nil
				-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
	-	[*ast.FuncDecl](../go/ast/FuncDecl.md)
		-	Recv: [*ast.FieldList](../go/ast/FieldList.md) // receiver (methods); or nil (functions)
			-	List: [\[\]*ast.Field](../go/ast/Field.md) // field list; or nil
				-	Names: [\[\]*ast.Ident](../go/ast/Ident.md) // field/method/parameter names; or nil if anonymous field
				-	Type: [*ast.Expr](../go/ast/Expr.md) // field/method/parameter type
				-	Tag:[*ast.BasicLit](../go/ast/BasicLit.md) // field tag; or nil
		-	Name: [ast.Ident](../go/ast/Ident.md) // function/method name
			-	Obj: [ast.Object](../go/ast/Object.md)
				-	Decl: [ast.Decl](../go/ast/Decl.md)
					-	[ast.Field](../go/ast/Field.md)
						-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
						-	Names: [*ast.Ident](../go/ast/Ident.md) // field/method/parameter names; or nil if anonymous field
						-	Type: [*ast.Expr](../go/ast/Expr.md) // field/method/parameter type
						-	Tag: [*ast.BasicLit](../go/ast/CommentGroup.md) // field tag; or nil
						-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
					-	[ast.ImportSpec](../go/ast/ImportSpec.md)
						-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
						-	Name: [*ast.Ident](../go/ast/Ident.md) // local package name (including "."); or nil
						-	Path: [*ast.BasicLit](../go/ast/CommentGroup.md) // import path
						-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
						-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
					-	[ast.TypeSpec](../go/ast/TypeSpec.md)
						-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
						-	Name: [*ast.Ident](../go/ast/Ident.md) // type name
						-	Type: [ast.Expr](../go/ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
							-	[*ast.Ident](../go/ast/Ident.md)
							-	[*ast.ParenExpr](../go/ast/ParenExpr.md)
							-	[*ast.SelectorExpr](../go/ast/SelectorExpr.md)
							-	[*ast.StarExpr](../go/ast/StarExpr.md)
							-	[ast.ArrayType](../go/ast/ArrayType.md)
								-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
								-	Len: [ast.Expr](../go/ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
								-	Elt: [ast.Expr](../go/ast/Expr.md) // element type
							-	[ast.ChanType](../go/ast/ChanType.md)
								-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
								-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
								-	Dir: [ChanDir](../go/ast/ChanDir.md) // channel direction
								-	Value: [ast.Expr](../go/ast/Expr.md) // value type
							-	[ast.FuncType](../go/ast/FuncType.md)
								-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
								-	Params: [*ast.FieldList](../go/ast/FieldList.md) // (incoming) parameters; non-nil
								-	Results: [*ast.FieldList](../go/ast/FieldList.md) // (outgoing) results; or nil
							-	[ast.InterfaceType](../go/ast/InterfaceType.md)
								-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
								-	Methods: [*ast.FieldList](../go/ast/FieldList.md) // list of methods
							-	[ast.MapType](../go/ast/MapType.md)
								-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
								-	Key: [ast.Expr](../go/ast/Expr.md)
								-	Value: [ast.Expr](../go/ast/Expr.md)
							-	[ast.StructType](../go/ast/StructType.md)
								-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
								-	Fields: [*ast.FieldList](../go/ast/FieldList.md) // list of field declarations
						-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
					-	[ast.ValueSpec](../go/ast/ValueSpec.md)
						-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // associated documentation; or nil
						-	Names: [\[\]*ast.Ident](../go/ast/Ident.md) // value name (len(Names) > 0)
						-	Type: [ast.Expr](../go/ast/Expr.md) // value type; or nil
						-	Values: [\[\]ast.Expr](../go/ast/Expr.md) // initial value; or nil
						-	Comment: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
					-	[ast.FuncDecl](../go/ast/FuncDecl.md)
						-	Doc: [*ast.CommentGroup](../go/ast/CommentGroup.md) // line comments; or nil
						-	Recv: [*ast.FieldList](../go/ast/FieldList.md) // receiver (methods); or nil (functions)
						-	Name: [*ast.Ident](../go/ast/Ident.md) // function/method name
						-	Type: [*ast.FuncType](../go/ast/FuncType.md) // function signature: parameters, results, and position of "func" keyword
						-	Body: [*ast.BlockStmt](../go/ast/BlockStmt.md) // function body; or nil (forward declaration)
					-	[ast.LabeledStmt](../go/ast/LabeledStmt.md)
						-	Label: [*ast.Ident](../go/ast/Ident.md)
						-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
						-	Stmt: [ast.Stmt](../go/ast/Stmt.md)
					-	[ast.AssignStmt](../go/ast/AssignStmt.md)
						-	Lhs: [\[\]ast.Expr](../go/ast/Expr.md)
						-	TokPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Tok
						-	Tok: [token.Token](https://godoc.org/go/token#Token) // assignment token, DEFINE
						-	Rhs: [\[\]ast.Expr](../go/ast/Expr.md)
					-	[ast.Scope](../go/ast/Scope.md)
						-	Outer: [*ast.Scope](../go/ast/Scope.md)
						-	Objects: [map\[string\]*ast.Object](../go/ast/Object.md)
		-	Type: [*ast.FuncType](../go/ast/FuncType.md) // function signature: parameters, results, and position of "func" keyword
			-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
			-	Params: [*ast.FieldList](../go/ast/FieldList.md) // (incoming) parameters; non-nil
			-	Results: [*ast.FieldList](../go/ast/FieldList.md) // (outgoing) results; or nil
		-	Body: [*ast.BlockStmt](../go/ast/BlockStmt.md) // function body; or nil (forward declaration)
			-	List: [\[\]ast.Stmt](../go/ast/Stmt.md)

ast.Stmt
--------

<details>
 <summary>type list</summary>
 ```go
 type (
 	// A BadStmt node is a placeholder for statements containing
 	// syntax errors for which no correct statement nodes can be
 	// created.
 	//
 	BadStmt struct {
 		From, To token.Pos // position range of bad statement
 	}

 	// A DeclStmt node represents a declaration in a statement list.
 	DeclStmt struct {
 		Decl Decl // *GenDecl with CONST, TYPE, or VAR token
 	}

 	// An EmptyStmt node represents an empty statement.
 	// The "position" of the empty statement is the position
 	// of the immediately following (explicit or implicit) semicolon.
 	//
 	EmptyStmt struct {
 		Semicolon token.Pos // position of following ";"
 		Implicit  bool      // if set, ";" was omitted in the source
 	}

 	// A LabeledStmt node represents a labeled statement.
 	LabeledStmt struct {
 		Label *Ident
 		Colon token.Pos // position of ":"
 		Stmt  Stmt
 	}

 	// An ExprStmt node represents a (stand-alone) expression
 	// in a statement list.
 	//
 	ExprStmt struct {
 		X Expr // expression
 	}

 	// A SendStmt node represents a send statement.
 	SendStmt struct {
 		Chan  Expr
 		Arrow token.Pos // position of "<-"
 		Value Expr
 	}

 	// An IncDecStmt node represents an increment or decrement statement.
 	IncDecStmt struct {
 		X      Expr
 		TokPos token.Pos   // position of Tok
 		Tok    token.Token // INC or DEC
 	}

 	// An AssignStmt node represents an assignment or
 	// a short variable declaration.
 	//
 	AssignStmt struct {
 		Lhs    []Expr
 		TokPos token.Pos   // position of Tok
 		Tok    token.Token // assignment token, DEFINE
 		Rhs    []Expr
 	}

 	// A GoStmt node represents a go statement.
 	GoStmt struct {
 		Go   token.Pos // position of "go" keyword
 		Call *CallExpr
 	}

 	// A DeferStmt node represents a defer statement.
 	DeferStmt struct {
 		Defer token.Pos // position of "defer" keyword
 		Call  *CallExpr
 	}

 	// A ReturnStmt node represents a return statement.
 	ReturnStmt struct {
 		Return  token.Pos // position of "return" keyword
 		Results []Expr    // result expressions; or nil
 	}

 	// A BranchStmt node represents a break, continue, goto,
 	// or fallthrough statement.
 	//
 	BranchStmt struct {
 		TokPos token.Pos   // position of Tok
 		Tok    token.Token // keyword token (BREAK, CONTINUE, GOTO, FALLTHROUGH)
 		Label  *Ident      // label name; or nil
 	}

 	// A BlockStmt node represents a braced statement list.
 	BlockStmt struct {
 		Lbrace token.Pos // position of "{"
 		List   []Stmt
 		Rbrace token.Pos // position of "}"
 	}

 	// An IfStmt node represents an if statement.
 	IfStmt struct {
 		If   token.Pos // position of "if" keyword
 		Init Stmt      // initialization statement; or nil
 		Cond Expr      // condition
 		Body *BlockStmt
 		Else Stmt // else branch; or nil
 	}

 	// A CaseClause represents a case of an expression or type switch statement.
 	CaseClause struct {
 		Case  token.Pos // position of "case" or "default" keyword
 		List  []Expr    // list of expressions or types; nil means default case
 		Colon token.Pos // position of ":"
 		Body  []Stmt    // statement list; or nil
 	}

 	// A SwitchStmt node represents an expression switch statement.
 	SwitchStmt struct {
 		Switch token.Pos  // position of "switch" keyword
 		Init   Stmt       // initialization statement; or nil
 		Tag    Expr       // tag expression; or nil
 		Body   *BlockStmt // CaseClauses only
 	}

 	// An TypeSwitchStmt node represents a type switch statement.
 	TypeSwitchStmt struct {
 		Switch token.Pos  // position of "switch" keyword
 		Init   Stmt       // initialization statement; or nil
 		Assign Stmt       // x := y.(type) or y.(type)
 		Body   *BlockStmt // CaseClauses only
 	}

 	// A CommClause node represents a case of a select statement.
 	CommClause struct {
 		Case  token.Pos // position of "case" or "default" keyword
 		Comm  Stmt      // send or receive statement; nil means default case
 		Colon token.Pos // position of ":"
 		Body  []Stmt    // statement list; or nil
 	}

 	// An SelectStmt node represents a select statement.
 	SelectStmt struct {
 		Select token.Pos  // position of "select" keyword
 		Body   *BlockStmt // CommClauses only
 	}

 	// A ForStmt represents a for statement.
 	ForStmt struct {
 		For  token.Pos // position of "for" keyword
 		Init Stmt      // initialization statement; or nil
 		Cond Expr      // condition; or nil
 		Post Stmt      // post iteration statement; or nil
 		Body *BlockStmt
 	}

 	// A RangeStmt represents a for statement with a range clause.
 	RangeStmt struct {
 		For        token.Pos   // position of "for" keyword
 		Key, Value Expr        // Key, Value may be nil
 		TokPos     token.Pos   // position of Tok; invalid if Key == nil
 		Tok        token.Token // ILLEGAL if Key == nil, ASSIGN, DEFINE
 		X          Expr        // value to range over
 		Body       *BlockStmt
 	}
 )
 ```
</details>

-	[ast.Stmt](../go/ast/Stmt.md)
	-	[*ast.BadStmt](../go/ast/BadStmt.md)
	-	[*ast.DeclStmt](../go/ast/DeclStmt.md)
	-	[*ast.EmptyStmt](../go/ast/EmptyStmt.md)
	-	[*ast.LabeledStmt](../go/ast/LabeledStmt.md)
	-	[*ast.ExprStmt](../go/ast/ExprStmt.md)
	-	[*ast.SendStmt](../go/ast/SendStmt.md)
	-	[*ast.IncDecStmt](../go/ast/IncDecStmt.md)
	-	[*ast.AssignStmt](../go/ast/AssignStmt.md)
	-	[*ast.GoStmt](../go/ast/GoStmt.md)
	-	[*ast.DeferStmt](../go/ast/DeferStmt.md)
	-	[*ast.ReturnStmt](../go/ast/ReturnStmt.md)
	-	[*ast.BranchStmt](../go/ast/BranchStmt.md)
	-	[*ast.BlockStmt](../go/ast/BlockStmt.md)
	-	[*ast.IfStmt](../go/ast/IfStmt.md)
	-	[*ast.CaseClause](../go/ast/CaseClause.md)
	-	[*ast.SwitchStmt](../go/ast/SwitchStmt.md)
	-	[*ast.TypeSwitchStmt](../go/ast/TypeSwitchStmt.md)
	-	[*ast.CommClause](../go/ast/CommClause.md)
	-	[*ast.SelectStmt](../go/ast/SelectStmt.md)
	-	[*ast.ForStmt](../go/ast/ForStmt.md)
	-	[*ast.RangeStmt](../go/ast/RangeStmt.md)
