```go
   0  *ast.File {
   1  .  Package: ./cmd/lookup/lookup.go:1:1
   2  .  Name: *ast.Ident {
   3  .  .  NamePos: ./cmd/lookup/lookup.go:1:9
   4  .  .  Name: "main"
   5  .  }
   6  .  Decls: []ast.Decl (len = 5) {
   7  .  .  0: *ast.GenDecl {
   8  .  .  .  TokPos: ./cmd/lookup/lookup.go:3:1
   9  .  .  .  Tok: import
  10  .  .  .  Lparen: ./cmd/lookup/lookup.go:3:8
  11  .  .  .  Specs: []ast.Spec (len = 8) {
  12  .  .  .  .  0: *ast.ImportSpec {
  13  .  .  .  .  .  Path: *ast.BasicLit {
  14  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:4:2
  15  .  .  .  .  .  .  Kind: STRING
  16  .  .  .  .  .  .  Value: "\"fmt\""
  17  .  .  .  .  .  }
  18  .  .  .  .  .  EndPos: -
  19  .  .  .  .  }
  20  .  .  .  .  1: *ast.ImportSpec {
  21  .  .  .  .  .  Path: *ast.BasicLit {
  22  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:5:2
  23  .  .  .  .  .  .  Kind: STRING
  24  .  .  .  .  .  .  Value: "\"go/ast\""
  25  .  .  .  .  .  }
  26  .  .  .  .  .  EndPos: -
  27  .  .  .  .  }
  28  .  .  .  .  2: *ast.ImportSpec {
  29  .  .  .  .  .  Path: *ast.BasicLit {
  30  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:6:2
  31  .  .  .  .  .  .  Kind: STRING
  32  .  .  .  .  .  .  Value: "\"go/importer\""
  33  .  .  .  .  .  }
  34  .  .  .  .  .  EndPos: -
  35  .  .  .  .  }
  36  .  .  .  .  3: *ast.ImportSpec {
  37  .  .  .  .  .  Path: *ast.BasicLit {
  38  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:7:2
  39  .  .  .  .  .  .  Kind: STRING
  40  .  .  .  .  .  .  Value: "\"go/parser\""
  41  .  .  .  .  .  }
  42  .  .  .  .  .  EndPos: -
  43  .  .  .  .  }
  44  .  .  .  .  4: *ast.ImportSpec {
  45  .  .  .  .  .  Path: *ast.BasicLit {
  46  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:8:2
  47  .  .  .  .  .  .  Kind: STRING
  48  .  .  .  .  .  .  Value: "\"go/token\""
  49  .  .  .  .  .  }
  50  .  .  .  .  .  EndPos: -
  51  .  .  .  .  }
  52  .  .  .  .  5: *ast.ImportSpec {
  53  .  .  .  .  .  Path: *ast.BasicLit {
  54  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:9:2
  55  .  .  .  .  .  .  Kind: STRING
  56  .  .  .  .  .  .  Value: "\"go/types\""
  57  .  .  .  .  .  }
  58  .  .  .  .  .  EndPos: -
  59  .  .  .  .  }
  60  .  .  .  .  6: *ast.ImportSpec {
  61  .  .  .  .  .  Path: *ast.BasicLit {
  62  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:10:2
  63  .  .  .  .  .  .  Kind: STRING
  64  .  .  .  .  .  .  Value: "\"log\""
  65  .  .  .  .  .  }
  66  .  .  .  .  .  EndPos: -
  67  .  .  .  .  }
  68  .  .  .  .  7: *ast.ImportSpec {
  69  .  .  .  .  .  Path: *ast.BasicLit {
  70  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:11:2
  71  .  .  .  .  .  .  Kind: STRING
  72  .  .  .  .  .  .  Value: "\"strings\""
  73  .  .  .  .  .  }
  74  .  .  .  .  .  EndPos: -
  75  .  .  .  .  }
  76  .  .  .  }
  77  .  .  .  Rparen: ./cmd/lookup/lookup.go:12:1
  78  .  .  }
  79  .  .  1: *ast.GenDecl {
  80  .  .  .  TokPos: ./cmd/lookup/lookup.go:14:1
  81  .  .  .  Tok: type
  82  .  .  .  Lparen: -
  83  .  .  .  Specs: []ast.Spec (len = 1) {
  84  .  .  .  .  0: *ast.TypeSpec {
  85  .  .  .  .  .  Name: *ast.Ident {
  86  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:14:6
  87  .  .  .  .  .  .  Name: "Lookup"
  88  .  .  .  .  .  .  Obj: *ast.Object {
  89  .  .  .  .  .  .  .  Kind: type
  90  .  .  .  .  .  .  .  Name: "Lookup"
  91  .  .  .  .  .  .  .  Decl: *(obj @ 84)
  92  .  .  .  .  .  .  }
  93  .  .  .  .  .  }
  94  .  .  .  .  .  Type: *ast.StructType {
  95  .  .  .  .  .  .  Struct: ./cmd/lookup/lookup.go:14:13
  96  .  .  .  .  .  .  Fields: *ast.FieldList {
  97  .  .  .  .  .  .  .  Opening: ./cmd/lookup/lookup.go:14:20
  98  .  .  .  .  .  .  .  List: []*ast.Field (len = 3) {
  99  .  .  .  .  .  .  .  .  0: *ast.Field {
 100  .  .  .  .  .  .  .  .  .  Names: []*ast.Ident (len = 1) {
 101  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 102  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:15:2
 103  .  .  .  .  .  .  .  .  .  .  .  Name: "Target"
 104  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 105  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 106  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Target"
 107  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 99)
 108  .  .  .  .  .  .  .  .  .  .  .  }
 109  .  .  .  .  .  .  .  .  .  .  }
 110  .  .  .  .  .  .  .  .  .  }
 111  .  .  .  .  .  .  .  .  .  Type: *ast.Ident {
 112  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:15:10
 113  .  .  .  .  .  .  .  .  .  .  Name: "string"
 114  .  .  .  .  .  .  .  .  .  }
 115  .  .  .  .  .  .  .  .  }
 116  .  .  .  .  .  .  .  .  1: *ast.Field {
 117  .  .  .  .  .  .  .  .  .  Names: []*ast.Ident (len = 1) {
 118  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 119  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:2
 120  .  .  .  .  .  .  .  .  .  .  .  Name: "Types"
 121  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 122  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 123  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Types"
 124  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 116)
 125  .  .  .  .  .  .  .  .  .  .  .  }
 126  .  .  .  .  .  .  .  .  .  .  }
 127  .  .  .  .  .  .  .  .  .  }
 128  .  .  .  .  .  .  .  .  .  Type: *ast.MapType {
 129  .  .  .  .  .  .  .  .  .  .  Map: ./cmd/lookup/lookup.go:16:10
 130  .  .  .  .  .  .  .  .  .  .  Key: *ast.Ident {
 131  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:14
 132  .  .  .  .  .  .  .  .  .  .  .  Name: "string"
 133  .  .  .  .  .  .  .  .  .  .  }
 134  .  .  .  .  .  .  .  .  .  .  Value: *ast.SelectorExpr {
 135  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 136  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:21
 137  .  .  .  .  .  .  .  .  .  .  .  .  Name: "types"
 138  .  .  .  .  .  .  .  .  .  .  .  }
 139  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 140  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:16:27
 141  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Type"
 142  .  .  .  .  .  .  .  .  .  .  .  }
 143  .  .  .  .  .  .  .  .  .  .  }
 144  .  .  .  .  .  .  .  .  .  }
 145  .  .  .  .  .  .  .  .  }
 146  .  .  .  .  .  .  .  .  2: *ast.Field {
 147  .  .  .  .  .  .  .  .  .  Names: []*ast.Ident (len = 1) {
 148  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 149  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:2
 150  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 151  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 152  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 153  .  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 154  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 146)
 155  .  .  .  .  .  .  .  .  .  .  .  }
 156  .  .  .  .  .  .  .  .  .  .  }
 157  .  .  .  .  .  .  .  .  .  }
 158  .  .  .  .  .  .  .  .  .  Type: *ast.StarExpr {
 159  .  .  .  .  .  .  .  .  .  .  Star: ./cmd/lookup/lookup.go:17:10
 160  .  .  .  .  .  .  .  .  .  .  X: *ast.SelectorExpr {
 161  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 162  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:11
 163  .  .  .  .  .  .  .  .  .  .  .  .  Name: "ast"
 164  .  .  .  .  .  .  .  .  .  .  .  }
 165  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 166  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:17:15
 167  .  .  .  .  .  .  .  .  .  .  .  .  Name: "CommentGroup"
 168  .  .  .  .  .  .  .  .  .  .  .  }
 169  .  .  .  .  .  .  .  .  .  .  }
 170  .  .  .  .  .  .  .  .  .  }
 171  .  .  .  .  .  .  .  .  }
 172  .  .  .  .  .  .  .  }
 173  .  .  .  .  .  .  .  Closing: ./cmd/lookup/lookup.go:18:1
 174  .  .  .  .  .  .  }
 175  .  .  .  .  .  .  Incomplete: false
 176  .  .  .  .  .  }
 177  .  .  .  .  }
 178  .  .  .  }
 179  .  .  .  Rparen: -
 180  .  .  }
 181  .  .  2: *ast.GenDecl {
 182  .  .  .  TokPos: ./cmd/lookup/lookup.go:20:1
 183  .  .  .  Tok: const
 184  .  .  .  Lparen: -
 185  .  .  .  Specs: []ast.Spec (len = 1) {
 186  .  .  .  .  0: *ast.ValueSpec {
 187  .  .  .  .  .  Names: []*ast.Ident (len = 1) {
 188  .  .  .  .  .  .  0: *ast.Ident {
 189  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:20:7
 190  .  .  .  .  .  .  .  Name: "hello"
 191  .  .  .  .  .  .  .  Obj: *ast.Object {
 192  .  .  .  .  .  .  .  .  Kind: const
 193  .  .  .  .  .  .  .  .  Name: "hello"
 194  .  .  .  .  .  .  .  .  Decl: *(obj @ 186)
 195  .  .  .  .  .  .  .  .  Data: 0
 196  .  .  .  .  .  .  .  }
 197  .  .  .  .  .  .  }
 198  .  .  .  .  .  }
 199  .  .  .  .  .  Values: []ast.Expr (len = 1) {
 200  .  .  .  .  .  .  0: *ast.BasicLit {
 201  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:20:15
 202  .  .  .  .  .  .  .  Kind: STRING
 203  .  .  .  .  .  .  .  Value: "`\npackage main\n\nimport \"fmt\"\n\n// append\nfunc main() {\n        // fmt\n        fmt.Println(\"Hello, world\")\n        // main\n        main, x := 1, 2\n        // main\n        print(main, x)\n        // x\n}\n// x\n`"
 204  .  .  .  .  .  .  }
 205  .  .  .  .  .  }
 206  .  .  .  .  }
 207  .  .  .  }
 208  .  .  .  Rparen: -
 209  .  .  }
 210  .  .  3: *ast.GenDecl {
 211  .  .  .  TokPos: ./cmd/lookup/lookup.go:38:1
 212  .  .  .  Tok: var
 213  .  .  .  Lparen: -
 214  .  .  .  Specs: []ast.Spec (len = 1) {
 215  .  .  .  .  0: *ast.ValueSpec {
 216  .  .  .  .  .  Names: []*ast.Ident (len = 1) {
 217  .  .  .  .  .  .  0: *ast.Ident {
 218  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:38:5
 219  .  .  .  .  .  .  .  Name: "helloFile"
 220  .  .  .  .  .  .  .  Obj: *ast.Object {
 221  .  .  .  .  .  .  .  .  Kind: var
 222  .  .  .  .  .  .  .  .  Name: "helloFile"
 223  .  .  .  .  .  .  .  .  Decl: *(obj @ 215)
 224  .  .  .  .  .  .  .  .  Data: 0
 225  .  .  .  .  .  .  .  }
 226  .  .  .  .  .  .  }
 227  .  .  .  .  .  }
 228  .  .  .  .  .  Values: []ast.Expr (len = 1) {
 229  .  .  .  .  .  .  0: *ast.Ident {
 230  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:38:17
 231  .  .  .  .  .  .  .  Name: "hello"
 232  .  .  .  .  .  .  .  Obj: *(obj @ 191)
 233  .  .  .  .  .  .  }
 234  .  .  .  .  .  }
 235  .  .  .  .  }
 236  .  .  .  }
 237  .  .  .  Rparen: -
 238  .  .  }
 239  .  .  4: *ast.FuncDecl {
 240  .  .  .  Name: *ast.Ident {
 241  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:40:6
 242  .  .  .  .  Name: "main"
 243  .  .  .  .  Obj: *ast.Object {
 244  .  .  .  .  .  Kind: func
 245  .  .  .  .  .  Name: "main"
 246  .  .  .  .  .  Decl: *(obj @ 239)
 247  .  .  .  .  }
 248  .  .  .  }
 249  .  .  .  Type: *ast.FuncType {
 250  .  .  .  .  Func: ./cmd/lookup/lookup.go:40:1
 251  .  .  .  .  Params: *ast.FieldList {
 252  .  .  .  .  .  Opening: ./cmd/lookup/lookup.go:40:10
 253  .  .  .  .  .  Closing: ./cmd/lookup/lookup.go:40:11
 254  .  .  .  .  }
 255  .  .  .  }
 256  .  .  .  Body: *ast.BlockStmt {
 257  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:40:13
 258  .  .  .  .  List: []ast.Stmt (len = 7) {
 259  .  .  .  .  .  0: *ast.AssignStmt {
 260  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
 261  .  .  .  .  .  .  .  0: *ast.Ident {
 262  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:2
 263  .  .  .  .  .  .  .  .  Name: "fset"
 264  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 265  .  .  .  .  .  .  .  .  .  Kind: var
 266  .  .  .  .  .  .  .  .  .  Name: "fset"
 267  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 259)
 268  .  .  .  .  .  .  .  .  }
 269  .  .  .  .  .  .  .  }
 270  .  .  .  .  .  .  }
 271  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:41:7
 272  .  .  .  .  .  .  Tok: :=
 273  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 274  .  .  .  .  .  .  .  0: *ast.CallExpr {
 275  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 276  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 277  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:10
 278  .  .  .  .  .  .  .  .  .  .  Name: "token"
 279  .  .  .  .  .  .  .  .  .  }
 280  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 281  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:41:16
 282  .  .  .  .  .  .  .  .  .  .  Name: "NewFileSet"
 283  .  .  .  .  .  .  .  .  .  }
 284  .  .  .  .  .  .  .  .  }
 285  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:41:26
 286  .  .  .  .  .  .  .  .  Ellipsis: -
 287  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:41:27
 288  .  .  .  .  .  .  .  }
 289  .  .  .  .  .  .  }
 290  .  .  .  .  .  }
 291  .  .  .  .  .  1: *ast.AssignStmt {
 292  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
 293  .  .  .  .  .  .  .  0: *ast.Ident {
 294  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:2
 295  .  .  .  .  .  .  .  .  Name: "f"
 296  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 297  .  .  .  .  .  .  .  .  .  Kind: var
 298  .  .  .  .  .  .  .  .  .  Name: "f"
 299  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 291)
 300  .  .  .  .  .  .  .  .  }
 301  .  .  .  .  .  .  .  }
 302  .  .  .  .  .  .  .  1: *ast.Ident {
 303  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:5
 304  .  .  .  .  .  .  .  .  Name: "err"
 305  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 306  .  .  .  .  .  .  .  .  .  Kind: var
 307  .  .  .  .  .  .  .  .  .  Name: "err"
 308  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 291)
 309  .  .  .  .  .  .  .  .  }
 310  .  .  .  .  .  .  .  }
 311  .  .  .  .  .  .  }
 312  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:42:9
 313  .  .  .  .  .  .  Tok: :=
 314  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 315  .  .  .  .  .  .  .  0: *ast.CallExpr {
 316  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 317  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 318  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:12
 319  .  .  .  .  .  .  .  .  .  .  Name: "parser"
 320  .  .  .  .  .  .  .  .  .  }
 321  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 322  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:19
 323  .  .  .  .  .  .  .  .  .  .  Name: "ParseFile"
 324  .  .  .  .  .  .  .  .  .  }
 325  .  .  .  .  .  .  .  .  }
 326  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:42:28
 327  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 4) {
 328  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 329  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:29
 330  .  .  .  .  .  .  .  .  .  .  Name: "fset"
 331  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 264)
 332  .  .  .  .  .  .  .  .  .  }
 333  .  .  .  .  .  .  .  .  .  1: *ast.BasicLit {
 334  .  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:42:35
 335  .  .  .  .  .  .  .  .  .  .  Kind: STRING
 336  .  .  .  .  .  .  .  .  .  .  Value: "\"hello.go\""
 337  .  .  .  .  .  .  .  .  .  }
 338  .  .  .  .  .  .  .  .  .  2: *ast.Ident {
 339  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:47
 340  .  .  .  .  .  .  .  .  .  .  Name: "helloFile"
 341  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 220)
 342  .  .  .  .  .  .  .  .  .  }
 343  .  .  .  .  .  .  .  .  .  3: *ast.SelectorExpr {
 344  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 345  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:58
 346  .  .  .  .  .  .  .  .  .  .  .  Name: "parser"
 347  .  .  .  .  .  .  .  .  .  .  }
 348  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 349  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:42:65
 350  .  .  .  .  .  .  .  .  .  .  .  Name: "ParseComments"
 351  .  .  .  .  .  .  .  .  .  .  }
 352  .  .  .  .  .  .  .  .  .  }
 353  .  .  .  .  .  .  .  .  }
 354  .  .  .  .  .  .  .  .  Ellipsis: -
 355  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:42:78
 356  .  .  .  .  .  .  .  }
 357  .  .  .  .  .  .  }
 358  .  .  .  .  .  }
 359  .  .  .  .  .  2: *ast.IfStmt {
 360  .  .  .  .  .  .  If: ./cmd/lookup/lookup.go:43:2
 361  .  .  .  .  .  .  Cond: *ast.BinaryExpr {
 362  .  .  .  .  .  .  .  X: *ast.Ident {
 363  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:43:5
 364  .  .  .  .  .  .  .  .  Name: "err"
 365  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
 366  .  .  .  .  .  .  .  }
 367  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:43:9
 368  .  .  .  .  .  .  .  Op: !=
 369  .  .  .  .  .  .  .  Y: *ast.Ident {
 370  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:43:12
 371  .  .  .  .  .  .  .  .  Name: "nil"
 372  .  .  .  .  .  .  .  }
 373  .  .  .  .  .  .  }
 374  .  .  .  .  .  .  Body: *ast.BlockStmt {
 375  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:43:16
 376  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
 377  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
 378  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 379  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 380  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 381  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:3
 382  .  .  .  .  .  .  .  .  .  .  .  .  Name: "log"
 383  .  .  .  .  .  .  .  .  .  .  .  }
 384  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 385  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:7
 386  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Fatal"
 387  .  .  .  .  .  .  .  .  .  .  .  }
 388  .  .  .  .  .  .  .  .  .  .  }
 389  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:44:12
 390  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 391  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 392  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:44:13
 393  .  .  .  .  .  .  .  .  .  .  .  .  Name: "err"
 394  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
 395  .  .  .  .  .  .  .  .  .  .  .  }
 396  .  .  .  .  .  .  .  .  .  .  }
 397  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 398  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:44:16
 399  .  .  .  .  .  .  .  .  .  }
 400  .  .  .  .  .  .  .  .  }
 401  .  .  .  .  .  .  .  }
 402  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:45:2
 403  .  .  .  .  .  .  }
 404  .  .  .  .  .  }
 405  .  .  .  .  .  3: *ast.AssignStmt {
 406  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
 407  .  .  .  .  .  .  .  0: *ast.Ident {
 408  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:2
 409  .  .  .  .  .  .  .  .  Name: "conf"
 410  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 411  .  .  .  .  .  .  .  .  .  Kind: var
 412  .  .  .  .  .  .  .  .  .  Name: "conf"
 413  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 405)
 414  .  .  .  .  .  .  .  .  }
 415  .  .  .  .  .  .  .  }
 416  .  .  .  .  .  .  }
 417  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:47:7
 418  .  .  .  .  .  .  Tok: :=
 419  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 420  .  .  .  .  .  .  .  0: *ast.CompositeLit {
 421  .  .  .  .  .  .  .  .  Type: *ast.SelectorExpr {
 422  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 423  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:10
 424  .  .  .  .  .  .  .  .  .  .  Name: "types"
 425  .  .  .  .  .  .  .  .  .  }
 426  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 427  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:16
 428  .  .  .  .  .  .  .  .  .  .  Name: "Config"
 429  .  .  .  .  .  .  .  .  .  }
 430  .  .  .  .  .  .  .  .  }
 431  .  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:47:22
 432  .  .  .  .  .  .  .  .  Elts: []ast.Expr (len = 1) {
 433  .  .  .  .  .  .  .  .  .  0: *ast.KeyValueExpr {
 434  .  .  .  .  .  .  .  .  .  .  Key: *ast.Ident {
 435  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:23
 436  .  .  .  .  .  .  .  .  .  .  .  Name: "Importer"
 437  .  .  .  .  .  .  .  .  .  .  }
 438  .  .  .  .  .  .  .  .  .  .  Colon: ./cmd/lookup/lookup.go:47:31
 439  .  .  .  .  .  .  .  .  .  .  Value: *ast.CallExpr {
 440  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 441  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 442  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:33
 443  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "importer"
 444  .  .  .  .  .  .  .  .  .  .  .  .  }
 445  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 446  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:47:42
 447  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Default"
 448  .  .  .  .  .  .  .  .  .  .  .  .  }
 449  .  .  .  .  .  .  .  .  .  .  .  }
 450  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:47:49
 451  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 452  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:47:50
 453  .  .  .  .  .  .  .  .  .  .  }
 454  .  .  .  .  .  .  .  .  .  }
 455  .  .  .  .  .  .  .  .  }
 456  .  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:47:51
 457  .  .  .  .  .  .  .  }
 458  .  .  .  .  .  .  }
 459  .  .  .  .  .  }
 460  .  .  .  .  .  4: *ast.AssignStmt {
 461  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
 462  .  .  .  .  .  .  .  0: *ast.Ident {
 463  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:2
 464  .  .  .  .  .  .  .  .  Name: "pkg"
 465  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 466  .  .  .  .  .  .  .  .  .  Kind: var
 467  .  .  .  .  .  .  .  .  .  Name: "pkg"
 468  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 460)
 469  .  .  .  .  .  .  .  .  }
 470  .  .  .  .  .  .  .  }
 471  .  .  .  .  .  .  .  1: *ast.Ident {
 472  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:7
 473  .  .  .  .  .  .  .  .  Name: "err"
 474  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
 475  .  .  .  .  .  .  .  }
 476  .  .  .  .  .  .  }
 477  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:48:11
 478  .  .  .  .  .  .  Tok: :=
 479  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 480  .  .  .  .  .  .  .  0: *ast.CallExpr {
 481  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 482  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 483  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:14
 484  .  .  .  .  .  .  .  .  .  .  Name: "conf"
 485  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 410)
 486  .  .  .  .  .  .  .  .  .  }
 487  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 488  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:19
 489  .  .  .  .  .  .  .  .  .  .  Name: "Check"
 490  .  .  .  .  .  .  .  .  .  }
 491  .  .  .  .  .  .  .  .  }
 492  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:48:24
 493  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 4) {
 494  .  .  .  .  .  .  .  .  .  0: *ast.BasicLit {
 495  .  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:48:25
 496  .  .  .  .  .  .  .  .  .  .  Kind: STRING
 497  .  .  .  .  .  .  .  .  .  .  Value: "\"cmd/hello\""
 498  .  .  .  .  .  .  .  .  .  }
 499  .  .  .  .  .  .  .  .  .  1: *ast.Ident {
 500  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:38
 501  .  .  .  .  .  .  .  .  .  .  Name: "fset"
 502  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 264)
 503  .  .  .  .  .  .  .  .  .  }
 504  .  .  .  .  .  .  .  .  .  2: *ast.CompositeLit {
 505  .  .  .  .  .  .  .  .  .  .  Type: *ast.ArrayType {
 506  .  .  .  .  .  .  .  .  .  .  .  Lbrack: ./cmd/lookup/lookup.go:48:44
 507  .  .  .  .  .  .  .  .  .  .  .  Elt: *ast.StarExpr {
 508  .  .  .  .  .  .  .  .  .  .  .  .  Star: ./cmd/lookup/lookup.go:48:46
 509  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.SelectorExpr {
 510  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 511  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:47
 512  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "ast"
 513  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 514  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 515  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:51
 516  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "File"
 517  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 518  .  .  .  .  .  .  .  .  .  .  .  .  }
 519  .  .  .  .  .  .  .  .  .  .  .  }
 520  .  .  .  .  .  .  .  .  .  .  }
 521  .  .  .  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:48:55
 522  .  .  .  .  .  .  .  .  .  .  Elts: []ast.Expr (len = 1) {
 523  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 524  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:56
 525  .  .  .  .  .  .  .  .  .  .  .  .  Name: "f"
 526  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 296)
 527  .  .  .  .  .  .  .  .  .  .  .  }
 528  .  .  .  .  .  .  .  .  .  .  }
 529  .  .  .  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:48:57
 530  .  .  .  .  .  .  .  .  .  }
 531  .  .  .  .  .  .  .  .  .  3: *ast.Ident {
 532  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:48:60
 533  .  .  .  .  .  .  .  .  .  .  Name: "nil"
 534  .  .  .  .  .  .  .  .  .  }
 535  .  .  .  .  .  .  .  .  }
 536  .  .  .  .  .  .  .  .  Ellipsis: -
 537  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:48:63
 538  .  .  .  .  .  .  .  }
 539  .  .  .  .  .  .  }
 540  .  .  .  .  .  }
 541  .  .  .  .  .  5: *ast.IfStmt {
 542  .  .  .  .  .  .  If: ./cmd/lookup/lookup.go:49:2
 543  .  .  .  .  .  .  Cond: *ast.BinaryExpr {
 544  .  .  .  .  .  .  .  X: *ast.Ident {
 545  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:49:5
 546  .  .  .  .  .  .  .  .  Name: "err"
 547  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
 548  .  .  .  .  .  .  .  }
 549  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:49:9
 550  .  .  .  .  .  .  .  Op: !=
 551  .  .  .  .  .  .  .  Y: *ast.Ident {
 552  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:49:12
 553  .  .  .  .  .  .  .  .  Name: "nil"
 554  .  .  .  .  .  .  .  }
 555  .  .  .  .  .  .  }
 556  .  .  .  .  .  .  Body: *ast.BlockStmt {
 557  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:49:16
 558  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
 559  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
 560  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 561  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 562  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 563  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:3
 564  .  .  .  .  .  .  .  .  .  .  .  .  Name: "log"
 565  .  .  .  .  .  .  .  .  .  .  .  }
 566  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 567  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:7
 568  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Fatal"
 569  .  .  .  .  .  .  .  .  .  .  .  }
 570  .  .  .  .  .  .  .  .  .  .  }
 571  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:50:12
 572  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 573  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 574  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:50:13
 575  .  .  .  .  .  .  .  .  .  .  .  .  Name: "err"
 576  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 305)
 577  .  .  .  .  .  .  .  .  .  .  .  }
 578  .  .  .  .  .  .  .  .  .  .  }
 579  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 580  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:50:16
 581  .  .  .  .  .  .  .  .  .  }
 582  .  .  .  .  .  .  .  .  }
 583  .  .  .  .  .  .  .  }
 584  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:51:2
 585  .  .  .  .  .  .  }
 586  .  .  .  .  .  }
 587  .  .  .  .  .  6: *ast.RangeStmt {
 588  .  .  .  .  .  .  For: ./cmd/lookup/lookup.go:55:2
 589  .  .  .  .  .  .  Key: *ast.Ident {
 590  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:6
 591  .  .  .  .  .  .  .  Name: "_"
 592  .  .  .  .  .  .  .  Obj: *ast.Object {
 593  .  .  .  .  .  .  .  .  Kind: var
 594  .  .  .  .  .  .  .  .  Name: "_"
 595  .  .  .  .  .  .  .  .  Decl: *ast.AssignStmt {
 596  .  .  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
 597  .  .  .  .  .  .  .  .  .  .  0: *(obj @ 589)
 598  .  .  .  .  .  .  .  .  .  .  1: *ast.Ident {
 599  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:9
 600  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 601  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 602  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 603  .  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 604  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 595)
 605  .  .  .  .  .  .  .  .  .  .  .  }
 606  .  .  .  .  .  .  .  .  .  .  }
 607  .  .  .  .  .  .  .  .  .  }
 608  .  .  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:55:17
 609  .  .  .  .  .  .  .  .  .  Tok: :=
 610  .  .  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 611  .  .  .  .  .  .  .  .  .  .  0: *ast.UnaryExpr {
 612  .  .  .  .  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:55:20
 613  .  .  .  .  .  .  .  .  .  .  .  Op: range
 614  .  .  .  .  .  .  .  .  .  .  .  X: *ast.SelectorExpr {
 615  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 616  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:26
 617  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "f"
 618  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 296)
 619  .  .  .  .  .  .  .  .  .  .  .  .  }
 620  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 621  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:55:28
 622  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Comments"
 623  .  .  .  .  .  .  .  .  .  .  .  .  }
 624  .  .  .  .  .  .  .  .  .  .  .  }
 625  .  .  .  .  .  .  .  .  .  .  }
 626  .  .  .  .  .  .  .  .  .  }
 627  .  .  .  .  .  .  .  .  }
 628  .  .  .  .  .  .  .  }
 629  .  .  .  .  .  .  }
 630  .  .  .  .  .  .  Value: *(obj @ 598)
 631  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:55:17
 632  .  .  .  .  .  .  Tok: :=
 633  .  .  .  .  .  .  X: *(obj @ 614)
 634  .  .  .  .  .  .  Body: *ast.BlockStmt {
 635  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:55:37
 636  .  .  .  .  .  .  .  List: []ast.Stmt (len = 5) {
 637  .  .  .  .  .  .  .  .  0: *ast.AssignStmt {
 638  .  .  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
 639  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 640  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:3
 641  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
 642  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 643  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 644  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
 645  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 637)
 646  .  .  .  .  .  .  .  .  .  .  .  }
 647  .  .  .  .  .  .  .  .  .  .  }
 648  .  .  .  .  .  .  .  .  .  }
 649  .  .  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:56:7
 650  .  .  .  .  .  .  .  .  .  Tok: :=
 651  .  .  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 652  .  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
 653  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 654  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 655  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:10
 656  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 657  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 601)
 658  .  .  .  .  .  .  .  .  .  .  .  .  }
 659  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 660  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:56:18
 661  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Pos"
 662  .  .  .  .  .  .  .  .  .  .  .  .  }
 663  .  .  .  .  .  .  .  .  .  .  .  }
 664  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:56:21
 665  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 666  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:56:22
 667  .  .  .  .  .  .  .  .  .  .  }
 668  .  .  .  .  .  .  .  .  .  }
 669  .  .  .  .  .  .  .  .  }
 670  .  .  .  .  .  .  .  .  1: *ast.AssignStmt {
 671  .  .  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
 672  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 673  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:3
 674  .  .  .  .  .  .  .  .  .  .  .  Name: "name"
 675  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 676  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 677  .  .  .  .  .  .  .  .  .  .  .  .  Name: "name"
 678  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 670)
 679  .  .  .  .  .  .  .  .  .  .  .  }
 680  .  .  .  .  .  .  .  .  .  .  }
 681  .  .  .  .  .  .  .  .  .  }
 682  .  .  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:57:8
 683  .  .  .  .  .  .  .  .  .  Tok: :=
 684  .  .  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 685  .  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
 686  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 687  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 688  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:11
 689  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "strings"
 690  .  .  .  .  .  .  .  .  .  .  .  .  }
 691  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 692  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:19
 693  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "TrimSpace"
 694  .  .  .  .  .  .  .  .  .  .  .  .  }
 695  .  .  .  .  .  .  .  .  .  .  .  }
 696  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:57:28
 697  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 698  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
 699  .  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 700  .  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 701  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:29
 702  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "comment"
 703  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 601)
 704  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 705  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 706  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:57:37
 707  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Text"
 708  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 709  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 710  .  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:57:41
 711  .  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 712  .  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:57:42
 713  .  .  .  .  .  .  .  .  .  .  .  .  }
 714  .  .  .  .  .  .  .  .  .  .  .  }
 715  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 716  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:57:43
 717  .  .  .  .  .  .  .  .  .  .  }
 718  .  .  .  .  .  .  .  .  .  }
 719  .  .  .  .  .  .  .  .  }
 720  .  .  .  .  .  .  .  .  2: *ast.ExprStmt {
 721  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 722  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 723  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 724  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:3
 725  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fmt"
 726  .  .  .  .  .  .  .  .  .  .  .  }
 727  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 728  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:7
 729  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Printf"
 730  .  .  .  .  .  .  .  .  .  .  .  }
 731  .  .  .  .  .  .  .  .  .  .  }
 732  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:58:13
 733  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 3) {
 734  .  .  .  .  .  .  .  .  .  .  .  0: *ast.BasicLit {
 735  .  .  .  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:58:14
 736  .  .  .  .  .  .  .  .  .  .  .  .  Kind: STRING
 737  .  .  .  .  .  .  .  .  .  .  .  .  Value: "\"At %s,\\t%q = \""
 738  .  .  .  .  .  .  .  .  .  .  .  }
 739  .  .  .  .  .  .  .  .  .  .  .  1: *ast.CallExpr {
 740  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 741  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 742  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:31
 743  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fset"
 744  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 264)
 745  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 746  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 747  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:36
 748  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Position"
 749  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 750  .  .  .  .  .  .  .  .  .  .  .  .  }
 751  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:58:44
 752  .  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 753  .  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 754  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:45
 755  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
 756  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
 757  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 758  .  .  .  .  .  .  .  .  .  .  .  .  }
 759  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 760  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:58:48
 761  .  .  .  .  .  .  .  .  .  .  .  }
 762  .  .  .  .  .  .  .  .  .  .  .  2: *ast.Ident {
 763  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:58:51
 764  .  .  .  .  .  .  .  .  .  .  .  .  Name: "name"
 765  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 675)
 766  .  .  .  .  .  .  .  .  .  .  .  }
 767  .  .  .  .  .  .  .  .  .  .  }
 768  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 769  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:58:55
 770  .  .  .  .  .  .  .  .  .  }
 771  .  .  .  .  .  .  .  .  }
 772  .  .  .  .  .  .  .  .  3: *ast.AssignStmt {
 773  .  .  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 1) {
 774  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 775  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:3
 776  .  .  .  .  .  .  .  .  .  .  .  Name: "inner"
 777  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 778  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 779  .  .  .  .  .  .  .  .  .  .  .  .  Name: "inner"
 780  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 772)
 781  .  .  .  .  .  .  .  .  .  .  .  }
 782  .  .  .  .  .  .  .  .  .  .  }
 783  .  .  .  .  .  .  .  .  .  }
 784  .  .  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:59:9
 785  .  .  .  .  .  .  .  .  .  Tok: :=
 786  .  .  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 787  .  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
 788  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 789  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 790  .  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 791  .  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 792  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:12
 793  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pkg"
 794  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 465)
 795  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 796  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 797  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:16
 798  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Scope"
 799  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 800  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 801  .  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:59:21
 802  .  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 803  .  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:59:22
 804  .  .  .  .  .  .  .  .  .  .  .  .  }
 805  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 806  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:24
 807  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Innermost"
 808  .  .  .  .  .  .  .  .  .  .  .  .  }
 809  .  .  .  .  .  .  .  .  .  .  .  }
 810  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:59:33
 811  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 812  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 813  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:59:34
 814  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
 815  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
 816  .  .  .  .  .  .  .  .  .  .  .  .  }
 817  .  .  .  .  .  .  .  .  .  .  .  }
 818  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 819  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:59:37
 820  .  .  .  .  .  .  .  .  .  .  }
 821  .  .  .  .  .  .  .  .  .  }
 822  .  .  .  .  .  .  .  .  }
 823  .  .  .  .  .  .  .  .  4: *ast.IfStmt {
 824  .  .  .  .  .  .  .  .  .  If: ./cmd/lookup/lookup.go:60:3
 825  .  .  .  .  .  .  .  .  .  Init: *ast.AssignStmt {
 826  .  .  .  .  .  .  .  .  .  .  Lhs: []ast.Expr (len = 2) {
 827  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 828  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:6
 829  .  .  .  .  .  .  .  .  .  .  .  .  Name: "_"
 830  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 831  .  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 832  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "_"
 833  .  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 825)
 834  .  .  .  .  .  .  .  .  .  .  .  .  }
 835  .  .  .  .  .  .  .  .  .  .  .  }
 836  .  .  .  .  .  .  .  .  .  .  .  1: *ast.Ident {
 837  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:9
 838  .  .  .  .  .  .  .  .  .  .  .  .  Name: "obj"
 839  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *ast.Object {
 840  .  .  .  .  .  .  .  .  .  .  .  .  .  Kind: var
 841  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "obj"
 842  .  .  .  .  .  .  .  .  .  .  .  .  .  Decl: *(obj @ 825)
 843  .  .  .  .  .  .  .  .  .  .  .  .  }
 844  .  .  .  .  .  .  .  .  .  .  .  }
 845  .  .  .  .  .  .  .  .  .  .  }
 846  .  .  .  .  .  .  .  .  .  .  TokPos: ./cmd/lookup/lookup.go:60:13
 847  .  .  .  .  .  .  .  .  .  .  Tok: :=
 848  .  .  .  .  .  .  .  .  .  .  Rhs: []ast.Expr (len = 1) {
 849  .  .  .  .  .  .  .  .  .  .  .  0: *ast.CallExpr {
 850  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 851  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 852  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:16
 853  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "inner"
 854  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 777)
 855  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 856  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 857  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:22
 858  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "LookupParent"
 859  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 860  .  .  .  .  .  .  .  .  .  .  .  .  }
 861  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:60:34
 862  .  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 2) {
 863  .  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 864  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:35
 865  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "name"
 866  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 675)
 867  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 868  .  .  .  .  .  .  .  .  .  .  .  .  .  1: *ast.Ident {
 869  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:41
 870  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "pos"
 871  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 642)
 872  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 873  .  .  .  .  .  .  .  .  .  .  .  .  }
 874  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 875  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:60:44
 876  .  .  .  .  .  .  .  .  .  .  .  }
 877  .  .  .  .  .  .  .  .  .  .  }
 878  .  .  .  .  .  .  .  .  .  }
 879  .  .  .  .  .  .  .  .  .  Cond: *ast.BinaryExpr {
 880  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 881  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:47
 882  .  .  .  .  .  .  .  .  .  .  .  Name: "obj"
 883  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 839)
 884  .  .  .  .  .  .  .  .  .  .  }
 885  .  .  .  .  .  .  .  .  .  .  OpPos: ./cmd/lookup/lookup.go:60:51
 886  .  .  .  .  .  .  .  .  .  .  Op: !=
 887  .  .  .  .  .  .  .  .  .  .  Y: *ast.Ident {
 888  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:60:54
 889  .  .  .  .  .  .  .  .  .  .  .  Name: "nil"
 890  .  .  .  .  .  .  .  .  .  .  }
 891  .  .  .  .  .  .  .  .  .  }
 892  .  .  .  .  .  .  .  .  .  Body: *ast.BlockStmt {
 893  .  .  .  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:60:58
 894  .  .  .  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
 895  .  .  .  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
 896  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 897  .  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 898  .  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 899  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:4
 900  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fmt"
 901  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 902  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 903  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:8
 904  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Println"
 905  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 906  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 907  .  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:61:15
 908  .  .  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 909  .  .  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.Ident {
 910  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:61:16
 911  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "obj"
 912  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Obj: *(obj @ 839)
 913  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 914  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 915  .  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 916  .  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:61:19
 917  .  .  .  .  .  .  .  .  .  .  .  .  }
 918  .  .  .  .  .  .  .  .  .  .  .  }
 919  .  .  .  .  .  .  .  .  .  .  }
 920  .  .  .  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:62:3
 921  .  .  .  .  .  .  .  .  .  }
 922  .  .  .  .  .  .  .  .  .  Else: *ast.BlockStmt {
 923  .  .  .  .  .  .  .  .  .  .  Lbrace: ./cmd/lookup/lookup.go:62:10
 924  .  .  .  .  .  .  .  .  .  .  List: []ast.Stmt (len = 1) {
 925  .  .  .  .  .  .  .  .  .  .  .  0: *ast.ExprStmt {
 926  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.CallExpr {
 927  .  .  .  .  .  .  .  .  .  .  .  .  .  Fun: *ast.SelectorExpr {
 928  .  .  .  .  .  .  .  .  .  .  .  .  .  .  X: *ast.Ident {
 929  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:63:4
 930  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "fmt"
 931  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 932  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Sel: *ast.Ident {
 933  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  NamePos: ./cmd/lookup/lookup.go:63:8
 934  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Name: "Println"
 935  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 936  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 937  .  .  .  .  .  .  .  .  .  .  .  .  .  Lparen: ./cmd/lookup/lookup.go:63:15
 938  .  .  .  .  .  .  .  .  .  .  .  .  .  Args: []ast.Expr (len = 1) {
 939  .  .  .  .  .  .  .  .  .  .  .  .  .  .  0: *ast.BasicLit {
 940  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  ValuePos: ./cmd/lookup/lookup.go:63:16
 941  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Kind: STRING
 942  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  Value: "\"not found\""
 943  .  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 944  .  .  .  .  .  .  .  .  .  .  .  .  .  }
 945  .  .  .  .  .  .  .  .  .  .  .  .  .  Ellipsis: -
 946  .  .  .  .  .  .  .  .  .  .  .  .  .  Rparen: ./cmd/lookup/lookup.go:63:27
 947  .  .  .  .  .  .  .  .  .  .  .  .  }
 948  .  .  .  .  .  .  .  .  .  .  .  }
 949  .  .  .  .  .  .  .  .  .  .  }
 950  .  .  .  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:64:3
 951  .  .  .  .  .  .  .  .  .  }
 952  .  .  .  .  .  .  .  .  }
 953  .  .  .  .  .  .  .  }
 954  .  .  .  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:65:2
 955  .  .  .  .  .  .  }
 956  .  .  .  .  .  }
 957  .  .  .  .  }
 958  .  .  .  .  Rbrace: ./cmd/lookup/lookup.go:66:1
 959  .  .  .  }
 960  .  .  }
 961  .  }
 962  .  Scope: *ast.Scope {
 963  .  .  Objects: map[string]*ast.Object (len = 4) {
 964  .  .  .  "Lookup": *(obj @ 88)
 965  .  .  .  "hello": *(obj @ 191)
 966  .  .  .  "helloFile": *(obj @ 220)
 967  .  .  .  "main": *(obj @ 243)
 968  .  .  }
 969  .  }
 970  .  Imports: []*ast.ImportSpec (len = 8) {
 971  .  .  0: *(obj @ 12)
 972  .  .  1: *(obj @ 20)
 973  .  .  2: *(obj @ 28)
 974  .  .  3: *(obj @ 36)
 975  .  .  4: *(obj @ 44)
 976  .  .  5: *(obj @ 52)
 977  .  .  6: *(obj @ 60)
 978  .  .  7: *(obj @ 68)
 979  .  }
 980  .  Unresolved: []*ast.Ident (len = 20) {
 981  .  .  0: *(obj @ 111)
 982  .  .  1: *(obj @ 130)
 983  .  .  2: *(obj @ 135)
 984  .  .  3: *(obj @ 161)
 985  .  .  4: *(obj @ 276)
 986  .  .  5: *(obj @ 317)
 987  .  .  6: *(obj @ 344)
 988  .  .  7: *(obj @ 369)
 989  .  .  8: *(obj @ 380)
 990  .  .  9: *(obj @ 422)
 991  .  .  10: *(obj @ 441)
 992  .  .  11: *(obj @ 510)
 993  .  .  12: *(obj @ 531)
 994  .  .  13: *(obj @ 551)
 995  .  .  14: *(obj @ 562)
 996  .  .  15: *(obj @ 687)
 997  .  .  16: *(obj @ 723)
 998  .  .  17: *(obj @ 887)
 999  .  .  18: *(obj @ 898)
1000  .  .  19: *(obj @ 928)
1001  .  }
1002  }
```
