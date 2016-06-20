Type Switch
===========

Type switch syntax tree.

ast.Node
--------

-	[ast.Expr](#astexpr)
-	[ast.Decl](#astdecl)
-	[ast.Stmt](#aststmt)

ast.Expr
--------

-	[ast.Expr](./ast/Expr.md)
	-	[ast.BadExpr](./ast/BadExpr.md)
	-	[ast.BasicLit](./ast/BasicLit.md)
		-	Kind: [token.Token](https://godoc.org/go/token#Token)
			-	[token.INT](https://godoc.org/go/token#INT) // 12345
			-	[token.FLOAT](https://godoc.org/go/token#FLOAT) // 123.45
			-	[token.IMAG](https://godoc.org/go/token#IMAG) // 123.45i
			-	[token.CHAR](https://godoc.org/go/token#CHAR) // 'a'
			-	[token.STRING](https://godoc.org/go/token#STRING) // "abc"
	-	[ast.BinaryExpr](./ast/BinaryExpr.md)
		-	X: [ast.Expr](./ast/Expr.md) // left operand
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
		-	Y: [ast.Expr](./ast/Expr.md) // right operand
	-	[ast.CallExpr](./ast/CallExpr.md)
		-	Fun: [ast.Expr](./ast.Expr.md) // function expression
			-	[*ast.Ident](./ast/Ident.md)
			-	[*ast.SelectorExpr](./ast/SelectorExpr.md)
		-	Args: [\[ \]ast.Expr](./ast.Expr.md) // function arguments; or nil
			-	[*ast.BasicLit](./ast/BasicLit.md)
			-	[*ast.CallExpr](./ast/CallExpr.md)
			-	[*ast.Ident](./ast/Ident.md)
			-	[*ast.MapType](./ast/MapType.md)
	-	[ast.CompositeLit](./ast/CompositeLit.md)
	-	[ast.Ellipsis](./ast/Ellipsis.md)
		-	Elt: [ast.Expr](./ast/Expr.md) // ellipsis element type (parameter lists only); or nil
	-	[ast.FuncLit](./ast/FuncLit.md)
		-	Type: [*ast.FuncType](./ast/FuncType.md)
		-	Body: [*ast.BlockStmt](./ast/BlockStmt.md)
	-	[ast.Ident](./ast/Ident.md)
		-	Obj: [*ast.Object](./ast/Object.md) // denoted object; or nil
			-	Kind: [ast.ObjKind](./ast/ObjKind.md)
				-	[ast.Bad](./ast/ObjKind.md#Bad) // for error handling
				-	[ast.Pkg](./ast/ObjKind.md#Pkg) // package
				-	[ast.Con](./ast/ObjKind.md#Con) // constant
				-	[ast.Typ](./ast/ObjKind.md#Typ) // type
				-	[ast.Var](./ast/ObjKind.md#Var) // variable
				-	[ast.Fun](./ast/ObjKind.md#Fun) // function or method
				-	[ast.Lbl](./ast/ObjKind.md#Lbl) // label
			-	Decl: `interface{}`
				-	[ast.Field](./ast/Field.md)
					-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
					-	Names: [*ast.Ident](./ast/Ident.md) // field/method/parameter names; or nil if anonymous field
					-	Type: [*ast.Expr](./ast/Expr.md) // field/method/parameter type
					-	Tag: [*ast.BasicLit](./ast/CommentGroup.md) // field tag; or nil
					-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
				-	[ast.ImportSpec](./ast/ImportSpec.md)
					-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](./ast/Ident.md) // local package name (including "."); or nil
					-	Path: [*ast.BasicLit](./ast/CommentGroup.md) // import path
					-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
					-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
				-	[ast.TypeSpec](./ast/TypeSpec.md)
					-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](./ast/Ident.md) // type name
					-	Type: [ast.Expr](./ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
						-	[*ast.Ident](./ast/Ident.md)
						-	[*ast.ParenExpr](./ast/ParenExpr.md)
						-	[*ast.SelectorExpr](./ast/SelectorExpr.md)
						-	[*ast.StarExpr](./ast/StarExpr.md)
						-	[ast.ArrayType](./ast/ArrayType.md)
							-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
							-	Len: [ast.Expr](./ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
							-	Elt: [ast.Expr](./ast/Expr.md) // element type
						-	[ast.ChanType](./ast/ChanType.md)
							-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
							-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
							-	Dir: [ChanDir](./ast/ChanDir.md) // channel direction
							-	Value: [ast.Expr](./ast/Expr.md) // value type
						-	[ast.FuncType](./ast/FuncType.md)
							-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
							-	Params: [*ast.FieldList](./ast/FieldList.md) // (incoming) parameters; non-nil
							-	Results: [*ast.FieldList](./ast/FieldList.md) // (outgoing) results; or nil
						-	[ast.InterfaceType](./ast/InterfaceType.md)
							-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
							-	Methods: [*ast.FieldList](./ast/FieldList.md) // list of methods
						-	[ast.MapType](./ast/MapType.md)
							-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
							-	Key: [ast.Expr](./ast/Expr.md)
							-	Value: [ast.Expr](./ast/Expr.md)
						-	[ast.StructType](./ast/StructType.md)
							-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
							-	Fields: [*ast.FieldList](./ast/FieldList.md) // list of field declarations
					-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
				-	[ast.ValueSpec](./ast/ValueSpec.md)
					-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
					-	Name: [*ast.Ident](./ast/Ident.md) // value name (len(Names) > 0)
					-	Type: [ast.Expr](./ast/Expr.md) // value type; or nil
					-	Values: [\[\]ast.Expr](./ast/Expr.md) // initial value; or nil
					-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
				-	[ast.FuncDecl](./ast/FuncDecl.md)
					-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
					-	Recv: [*ast.FieldList](./ast/FieldList.md) // receiver (methods); or nil (functions)
					-	Name: [*ast.Ident](./ast/Ident.md) // function/method name
					-	Type: [*ast.FuncType](./ast/FuncType.md) // function signature: parameters, results, and position of "func" keyword
					-	Body: [*ast.BlockStmt](./ast/BlockStmt.md) // function body; or nil (forward declaration)
				-	[ast.LabeledStmt](./ast/LabeledStmt.md)
					-	Label: [*ast.Ident](./ast/Ident.md)
					-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
					-	Stmt: [ast.Stmt](./ast/Stmt.md)
				-	[ast.AssignStmt](./ast/AssignStmt.md)
					-	Lhs: [\[\]ast.Expr](./ast/Expr.md)
					-	TokPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Tok
					-	Tok: [token.Token](https://godoc.org/go/token#Token) // assignment token, DEFINE
					-	Rhs: [\[\]ast.Expr](./ast/Expr.md)
				-	[ast.Scope](./ast/Scope.md)
					-	Outer: [*ast.Scope](./ast/Scope.md)
					-	Objects: [map\[string\]*ast.Object](./ast/Object.md)
	-	[ast.IndexExpr](./ast/IndexExpr.md)
		-	X: [ast.Expr](./ast/Expr.md) // expression
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Index: [ast.Expr](./ast/Expr.md) // index expression
		-	Y: [ast.Expr](./ast/Expr.md) // position of "\]"
	-	[ast.KeyValueExpr](./ast/KeyValueExpr.md)
		-	Key: [ast.Expr](./ast/Expr.md)
		-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
		-	Value: [ast.Expr](./ast/Expr.md)
	-	[ast.ParenExpr](./ast/ParenExpr.md)
		-	Lparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
		-	X: [ast.Expr](./ast/Expr.md) // parenthesized expression
		-	Rparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
	-	[ast.SelectorExpr](./ast/SelectorExpr.md)
		-	X: [ast.Expr](./ast/Expr.md) // expression
		-	Sel: [*ast.Ident](./ast/Ident.md) // field selector
	-	[ast.SliceExpr](./ast/SliceExpr.md)
		-	X: [ast.Expr](./ast/Expr.md) // expression
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Low: [ast.Expr](./ast/Expr.md) // begin of slice range; or nil
		-	High: [ast.Expr](./ast/Expr.md) // end of slice range; or nil
		-	Max: [ast.Expr](./ast/Expr.md) // maximum capacity of slice; or nil
		-	Rbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\]"
	-	[ast.StarExpr](./ast/StarExpr.md)
		-	Star: [token.Pos](https://godoc.org/go/token#Pos) // position of "*"
		-	X: [ast.Expr](./ast/Expr.md) // operand
	-	[ast.TypeAssertExpr](./ast/TypeAssertExpr.md)
		-	X: [ast.Expr](./ast/Expr.md) // expression
		-	Lparen: [token.Pos](https://godoc.org/go/token#Pos) // position of "("
		-	Type: [ast.Expr](./ast/Expr.md) // asserted type; nil means type switch X.(type)
		-	Rparen: [token.Pos](https://godoc.org/go/token#Pos) // position of ")"
	-	[ast.UnaryExpr](./ast/UnaryExpr.md)
		-	OpPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Op
		-	Op: [token.Pos](https://godoc.org/go/token#Token) // operator
		-	X: [ast.Expr](./ast/Expr.md) // operand
	-	[ast.ArrayType](./ast/ArrayType.md)
		-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
		-	Len: [ast.Expr](./ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
		-	Elt: [ast.Expr](./ast/Expr.md) // element type
	-	[ast.ChanType](./ast/ChanType.md)
		-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
		-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
		-	Dir: [ChanDir](./ast/ChanDir.md) // channel direction
		-	Value: [ast.Expr](./ast/Expr.md) // value type
	-	[ast.FuncType](./ast/FuncType.md)
		-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
		-	Params: [*ast.FieldList](./ast/FieldList.md) // (incoming) parameters; non-nil
		-	Results: [*ast.FieldList](./ast/FieldList.md) // (outgoing) results; or nil
	-	[ast.InterfaceType](./ast/InterfaceType.md)
		-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
		-	Methods: [*ast.FieldList](./ast/FieldList.md) // list of methods
	-	[ast.MapType](./ast/MapType.md)
		-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
		-	Key: [ast.Expr](./ast/Expr.md)
		-	Value: [ast.Expr](./ast/Expr.md)
	-	[ast.StructType](./ast/StructType.md)
		-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
		-	Fields: [*ast.FieldList](./ast/FieldList.md) // list of field declarations

ast.Decl
--------

-	[ast.Decl](./ast/Decl.md)
	-	[ast.BadDecl](./ast/BadDecl.md)
	-	[ast.GenDecl](./ast/GenDecl.md)
		-	Token: [token.Token](https://godoc.org/go/token#Token)
			-	[token.IMPORT](https://godoc.org/go/token#IMPORT)
			-	[token.CONST](https://godoc.org/go/token#CONST)
			-	[token.TYPE](https://godoc.org/go/token#TYPE)
			-	[token.VAR](https://godoc.org/go/token#VAR)
		-	Specs: [\[ \]ast.Specs](./ast/Spec.md)
			-	[ast.ImportSpec](./ast/ImportSpec.md)
				-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](./ast/Ident.md) // local package name (including "."); or nil
				-	Path: [*ast.BasicLit](./ast/CommentGroup.md) // import path
				-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
				-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
			-	[ast.TypeSpec](./ast/TypeSpec.md)
				-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](./ast/Ident.md) // type name
				-	Type: [ast.Expr](./ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
					-	[*ast.Ident](./ast/Ident.md)
					-	[*ast.ParenExpr](./ast/ParenExpr.md)
					-	[*ast.SelectorExpr](./ast/SelectorExpr.md)
					-	[*ast.StarExpr](./ast/StarExpr.md)
					-	[ast.ArrayType](./ast/ArrayType.md)
						-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
						-	Len: [ast.Expr](./ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
						-	Elt: [ast.Expr](./ast/Expr.md) // element type
					-	[ast.ChanType](./ast/ChanType.md)
						-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
						-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
						-	Dir: [ChanDir](./ast/ChanDir.md) // channel direction
						-	Value: [ast.Expr](./ast/Expr.md) // value type
					-	[ast.FuncType](./ast/FuncType.md)
						-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
						-	Params: [*ast.FieldList](./ast/FieldList.md) // (incoming) parameters; non-nil
						-	Results: [*ast.FieldList](./ast/FieldList.md) // (outgoing) results; or nil
					-	[ast.InterfaceType](./ast/InterfaceType.md)
						-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
						-	Methods: [*ast.FieldList](./ast/FieldList.md) // list of methods
					-	[ast.MapType](./ast/MapType.md)
						-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
						-	Key: [ast.Expr](./ast/Expr.md)
						-	Value: [ast.Expr](./ast/Expr.md)
					-	[ast.StructType](./ast/StructType.md)
						-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
						-	Fields: [*ast.FieldList](./ast/FieldList.md) // list of field declarations
				-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
			-	[ast.ValueSpec](./ast/ValueSpec.md)
				-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
				-	Name: [*ast.Ident](./ast/Ident.md) // value name (len(Names) > 0)
				-	Type: [ast.Expr](./ast/Expr.md) // value type; or nil
				-	Values: [\[\]ast.Expr](./ast/Expr.md) // initial value; or nil
				-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
	-	[ast.FuncDecl](./ast/FuncDecl.md)
		-	Name: [ast.Ident](./ast/Ident.md)
			-	[ast.Object](./ast/Object.md)
				-	[ast.Decl](./ast/Decl.md)
					-	[ast.Field](./ast/Field.md)
						-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
						-	Names: [*ast.Ident](./ast/Ident.md) // field/method/parameter names; or nil if anonymous field
						-	Type: [*ast.Expr](./ast/Expr.md) // field/method/parameter type
						-	Tag: [*ast.BasicLit](./ast/CommentGroup.md) // field tag; or nil
						-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
					-	[ast.ImportSpec](./ast/ImportSpec.md)
						-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
						-	Name: [*ast.Ident](./ast/Ident.md) // local package name (including "."); or nil
						-	Path: [*ast.BasicLit](./ast/CommentGroup.md) // import path
						-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
						-	EndPos: [token.Pos](https://godoc.org/go/token#Pos) // end of spec (overrides Path.Pos if nonzero)
					-	[ast.TypeSpec](./ast/TypeSpec.md)
						-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
						-	Name: [*ast.Ident](./ast/Ident.md) // type name
						-	Type: [ast.Expr](./ast/Expr.md) // *Ident, *ParenExpr, *SelectorExpr, *StarExpr, or any of the *XxxTypes
							-	[*ast.Ident](./ast/Ident.md)
							-	[*ast.ParenExpr](./ast/ParenExpr.md)
							-	[*ast.SelectorExpr](./ast/SelectorExpr.md)
							-	[*ast.StarExpr](./ast/StarExpr.md)
							-	[ast.ArrayType](./ast/ArrayType.md)
								-	Lbrack: [token.Pos](https://godoc.org/go/token#Pos) // position of "\["
								-	Len: [ast.Expr](./ast/Expr.md) // Ellipsis node for \[...\]T array types, nil for slice types
								-	Elt: [ast.Expr](./ast/Expr.md) // element type
							-	[ast.ChanType](./ast/ChanType.md)
								-	Begin: [token.Pos](https://godoc.org/go/token#Pos) // position of "chan" keyword or "-" (whichever comes first)
								-	Arrow: [token.Pos](https://godoc.org/go/token#Pos) // position of "-" (token.NoPos if there is no "-")
								-	Dir: [ChanDir](./ast/ChanDir.md) // channel direction
								-	Value: [ast.Expr](./ast/Expr.md) // value type
							-	[ast.FuncType](./ast/FuncType.md)
								-	Func: [token.Pos](https://godoc.org/go/token#Pos) // position of "func" keyword (token.NoPos if there is no "func")
								-	Params: [*ast.FieldList](./ast/FieldList.md) // (incoming) parameters; non-nil
								-	Results: [*ast.FieldList](./ast/FieldList.md) // (outgoing) results; or nil
							-	[ast.InterfaceType](./ast/InterfaceType.md)
								-	Interface: [token.Pos](https://godoc.org/go/token#Pos) // position of "interface" keyword
								-	Methods: [*ast.FieldList](./ast/FieldList.md) // list of methods
							-	[ast.MapType](./ast/MapType.md)
								-	Map: [token.Pos](https://godoc.org/go/token#Pos) // position of "map" keyword
								-	Key: [ast.Expr](./ast/Expr.md)
								-	Value: [ast.Expr](./ast/Expr.md)
							-	[ast.StructType](./ast/StructType.md)
								-	Struct: [token.Pos](https://godoc.org/go/token#Pos) // position of "struct" keyword
								-	Fields: [*ast.FieldList](./ast/FieldList.md) // list of field declarations
						-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
					-	[ast.ValueSpec](./ast/ValueSpec.md)
						-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // associated documentation; or nil
						-	Name: [*ast.Ident](./ast/Ident.md) // value name (len(Names) > 0)
						-	Type: [ast.Expr](./ast/Expr.md) // value type; or nil
						-	Values: [\[\]ast.Expr](./ast/Expr.md) // initial value; or nil
						-	Comment: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
					-	[ast.FuncDecl](./ast/FuncDecl.md)
						-	Doc: [*ast.CommentGroup](./ast/CommentGroup.md) // line comments; or nil
						-	Recv: [*ast.FieldList](./ast/FieldList.md) // receiver (methods); or nil (functions)
						-	Name: [*ast.Ident](./ast/Ident.md) // function/method name
						-	Type: [*ast.FuncType](./ast/FuncType.md) // function signature: parameters, results, and position of "func" keyword
						-	Body: [*ast.BlockStmt](./ast/BlockStmt.md) // function body; or nil (forward declaration)
					-	[ast.LabeledStmt](./ast/LabeledStmt.md)
						-	Label: [*ast.Ident](./ast/Ident.md)
						-	Colon: [token.Pos](https://godoc.org/go/token#Pos) // position of ":"
						-	Stmt: [ast.Stmt](./ast/Stmt.md)
					-	[ast.AssignStmt](./ast/AssignStmt.md)
						-	Lhs: [\[\]ast.Expr](./ast/Expr.md)
						-	TokPos: [token.Pos](https://godoc.org/go/token#Pos) // position of Tok
						-	Tok: [token.Token](https://godoc.org/go/token#Token) // assignment token, DEFINE
						-	Rhs: [\[\]ast.Expr](./ast/Expr.md)
					-	[ast.Scope](./ast/Scope.md)
						-	Outer: [*ast.Scope](./ast/Scope.md)
						-	Objects: [map\[string\]*ast.Object](./ast/Object.md)

ast.Stmt
--------

-	[ast.Stmt](./ast/Stmt.md)
	-	[ast.BadStmt](./ast/BadStmt.md)
	-	[ast.DeclStmt](./ast/DeclStmt.md)
	-	[ast.EmptyStmt](./ast/EmptyStmt.md)
	-	[ast.LabeledStmt](./ast/LabeledStmt.md)
	-	[ast.ExprStmt](./ast/ExprStmt.md)
	-	[ast.SendStmt](./ast/SendStmt.md)
	-	[ast.IncDecStmt](./ast/IncDecStmt.md)
	-	[ast.AssignStmt](./ast/AssignStmt.md)
	-	[ast.GoStmt](./ast/GoStmt.md)
	-	[ast.DeferStmt](./ast/DeferStmt.md)
	-	[ast.ReturnStmt](./ast/ReturnStmt.md)
	-	[ast.BranchStmt](./ast/BranchStmt.md)
	-	[ast.BlockStmt](./ast/BlockStmt.md)
	-	[ast.IfStmt](./ast/IfStmt.md)
	-	[ast.CaseClause](./ast/CaseClause.md)
	-	[ast.SwitchStmt](./ast/SwitchStmt.md)
	-	[ast.TypeSwitchStmt](./ast/TypeSwitchStmt.md)
	-	[ast.CommClause](./ast/CommClause.md)
	-	[ast.SelectStmt](./ast/SelectStmt.md)
	-	[ast.ForStmt](./ast/ForStmt.md)
	-	[ast.RangeStmt](./ast/RangeStmt.md)