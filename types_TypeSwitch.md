go/types Type Switch
====================

Type switch syntax tree.

types.Type
----------

-	[types.Type](./types/Type.md)
	-	[types.Basic](./types/Basic.md)
	-	[types.Array](./types/Array.md)
	-	[types.Slice](./types/Slice.md)
	-	[types.Struct](./types/Structt.md)
	-	[types.Pointer](./types/Pointer.md)
	-	[types.Tuple](./types/Tuple.md)
	-	[types.Signature](./types/Signature.md)
		-	\(*Signature) Params: [types.Tuple](./types/Tuple.md)
		-	\(*Signature) Recv: [types.Var](./types/Var.md)
		-	\(*Signature) Results: [types.Tuple](./types/Tuple.md)
		-	\(*Signature) Strnig: string
		-	\(*Signature) Underlynig: [types.Type](./types/Type.md)
		-	\(*Signature) Variadic: bool
	-	[types.Interface](./types/interface.md)
	-	[types.Map](./types/Map.md)
	-	[types.Chan](./types/Chan.md)
	-	[types.Named](./types/Named.md)

types.Object
------------

-	[types.Object](./types/Object.md)
	-	[types.Func](./types.Func.md)
	-	[types.TypeName](./types.TypeName.md)
