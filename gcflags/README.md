# gcflags

version: [devel +35693d037f9d](https://github.com/golang/go/tree/35693d037f9d)

## debugtab

[go/src/cmd/compile/internal/gc/main.go#L62-L111@5b0ec1a6ac0e](https://github.com/golang/go/blob/5b0ec1a6ac0e/src/cmd/compile/internal/gc/main.go#L62-L111)

```go
// Debug arguments.
// These can be specified with the -d flag, as in "-d nil"
// to set the debug_checknil variable.
// Multiple options can be comma-separated.
// Each option accepts an optional argument, as in "gcprog=2"
var debugtab = []struct {
	name string
	help string
	val  interface{} // must be *int or *string
}{
	{"append", "print information about append compilation", &Debug_append},
	{"checkptr", "instrument unsafe pointer conversions", &Debug_checkptr},
	{"closure", "print information about closure compilation", &Debug_closure},
	{"compilelater", "compile functions as late as possible", &Debug_compilelater},
	{"disablenil", "disable nil checks", &disable_checknil},
	{"dclstack", "run internal dclstack check", &debug_dclstack},
	{"gcprog", "print dump of GC programs", &Debug_gcprog},
	{"libfuzzer", "coverage instrumentation for libfuzzer", &Debug_libfuzzer},
	{"nil", "print information about nil checks", &Debug_checknil},
	{"panic", "do not hide any compiler panic", &Debug_panic},
	{"slice", "print information about slice compilation", &Debug_slice},
	{"typeassert", "print information about type assertion inlining", &Debug_typeassert},
	{"wb", "print information about write barriers", &Debug_wb},
	{"export", "print export data", &Debug_export},
	{"pctab", "print named pc-value table", &Debug_pctab},
	{"locationlists", "print information about DWARF location list creation", &Debug_locationlist},
	{"typecheckinl", "eager typechecking of inline function bodies", &Debug_typecheckinl},
	{"dwarfinl", "print information about DWARF inlined function creation", &Debug_gendwarfinl},
	{"softfloat", "force compiler to emit soft-float code", &Debug_softfloat},
	{"defer", "print information about defer compilation", &Debug_defer},
	{"fieldtrack", "enable fieldtracking", &objabi.Fieldtrack_enabled},
}

const debugHelpHeader = `usage: -d arg[,arg]* and arg is <key>[=<value>]
<key> is one of:
`

const debugHelpFooter = `
<value> is key-specific.
Key "checkptr" supports values:
	"0": instrumentation disabled
	"1": conversions involving unsafe.Pointer are instrumented
	"2": conversions to unsafe.Pointer force heap allocation
Key "pctab" supports values:
	"pctospadj", "pctofile", "pctoline", "pctoinline", "pctopcdata"
`
```

### Usage

```sh
go build -o /dev/null -gcflags='all=-d=append,checkptr=1,checkptr=2,closure,compilelater,disablenil,dclstack,gcprog=2,libfuzzer,nil,panic,slice,typeassert,wb,export,pctab=(pctospadj,pctofile,pctoline,pctoinline,pctopcdata),locationlists,typecheckinl,dwarfinl,softfloat,defer,fieldtrack' <package import path>/...
```

### Details

TODO(zchee): write here.

## SSA

[go/src/cmd/compile/internal/ssa/compile.go#L222-L240@go1.15.2](https://github.com/golang/go/blob/go1.15.2/src/cmd/compile/internal/ssa/compile.go#L222-L240)

### Usage

```sh
go build -o /dev/null -gcflags='-d=ssa/<phase>/<flag>[=<value>|<function_name>] <package import path>/...'
```

### \<phase\>

- `check`
- `all`
  - Support flags:
    - `time`
    - `mem`
    - `dump`
- `build`
- `intrinsics`
  - Support flags:
    - `on`
    - `off`
    - `debug`

[go/src/cmd/compile/internal/ssa/compile.go#L426-L482@35693d037f9d](https://github.com/golang/go/blob/35693d037f9d/src/cmd/compile/internal/ssa/compile.go#L426-L482)

```go
// list of passes for the compiler
var passes = [...]pass{
	// TODO: combine phielim and copyelim into a single pass?
	{name: "number lines", fn: numberLines, required: true},
	{name: "early phielim", fn: phielim},
	{name: "early copyelim", fn: copyelim},
	{name: "early deadcode", fn: deadcode}, // remove generated dead code to avoid doing pointless work during opt
	{name: "short circuit", fn: shortcircuit},
	{name: "decompose args", fn: decomposeArgs, required: !go116lateCallExpansion, disabled: go116lateCallExpansion}, // handled by late call lowering
	{name: "decompose user", fn: decomposeUser, required: true},
	{name: "pre-opt deadcode", fn: deadcode},
	{name: "opt", fn: opt, required: true},               // NB: some generic rules know the name of the opt pass. TODO: split required rules and optimizing rules
	{name: "zero arg cse", fn: zcse, required: true},     // required to merge OpSB values
	{name: "opt deadcode", fn: deadcode, required: true}, // remove any blocks orphaned during opt
	{name: "generic cse", fn: cse},
	{name: "phiopt", fn: phiopt},
	{name: "gcse deadcode", fn: deadcode, required: true}, // clean out after cse and phiopt
	{name: "nilcheckelim", fn: nilcheckelim},
	{name: "prove", fn: prove},
	{name: "early fuse", fn: fuseEarly},
	{name: "decompose builtin", fn: decomposeBuiltIn, required: true},
	{name: "expand calls", fn: expandCalls, required: true},
	{name: "softfloat", fn: softfloat, required: true},
	{name: "late opt", fn: opt, required: true}, // TODO: split required rules and optimizing rules
	{name: "dead auto elim", fn: elimDeadAutosGeneric},
	{name: "generic deadcode", fn: deadcode, required: true}, // remove dead stores, which otherwise mess up store chain
	{name: "check bce", fn: checkbce},
	{name: "branchelim", fn: branchelim},
	{name: "late fuse", fn: fuseLate},
	{name: "dse", fn: dse},
	{name: "writebarrier", fn: writebarrier, required: true}, // expand write barrier ops
	{name: "insert resched checks", fn: insertLoopReschedChecks,
		disabled: objabi.Preemptibleloops_enabled == 0}, // insert resched checks in loops.
	{name: "lower", fn: lower, required: true},
	{name: "addressing modes", fn: addressingModes, required: false},
	{name: "lowered deadcode for cse", fn: deadcode}, // deadcode immediately before CSE avoids CSE making dead values live again
	{name: "lowered cse", fn: cse},
	{name: "elim unread autos", fn: elimUnreadAutos},
	{name: "tighten tuple selectors", fn: tightenTupleSelectors, required: true},
	{name: "lowered deadcode", fn: deadcode, required: true},
	{name: "checkLower", fn: checkLower, required: true},
	{name: "late phielim", fn: phielim},
	{name: "late copyelim", fn: copyelim},
	{name: "tighten", fn: tighten}, // move values closer to their uses
	{name: "late deadcode", fn: deadcode},
	{name: "critical", fn: critical, required: true}, // remove critical edges
	{name: "phi tighten", fn: phiTighten},            // place rematerializable phi args near uses to reduce value lifetimes
	{name: "likelyadjust", fn: likelyadjust},
	{name: "layout", fn: layout, required: true},     // schedule blocks
	{name: "schedule", fn: schedule, required: true}, // schedule values
	{name: "late nilcheck", fn: nilcheckelim2},
	{name: "flagalloc", fn: flagalloc, required: true}, // allocate flags register
	{name: "regalloc", fn: regalloc, required: true},   // allocate int & float registers + stack slots
	{name: "loop rotate", fn: loopRotate},
	{name: "stackframe", fn: stackframe, required: true},
	{name: "trim", fn: trim}, // remove empty blocks
}
```


### \<flags\>

- `on`
- `off`
- `debug`
- `mem`
- `time`
- `test`
- `stats`
- `dump`
- `seed`

### =\<value\>

defaults to 1.

### \<function_name\>

`<function_name>` is required for the `dump` flag, and specifies the name of function to dump after `<phase>`.

### Examples

```console
go compile -o /dev/null -d=ssa/check/on <package import path>/...
# or
go build -o /dev/null -gcflags='-d=ssa/check/on' <package import path>/...
```

enables checking after each phase

```console
go compile -o /dev/null -d=ssa/check/seed=1234 <package import path>/...
# or
go build -o /dev/null -gcflags='-d=ssa/check/seed=1234' <package import path>/...
```

enables checking after each phase, using 1234 to seed the PRNG
used for value order randomization.

```console
go compile -o /dev/null -d=ssa/all/time <package import path>/...
# or
go build -o /dev/null -gcflags='-d=ssa/all/time' <package import path>/...
```

enables time reporting for all phases.

```console
go compile -o /dev/null -d=ssa/prove/debug=2 <package import path>/...
# or
go build -o /dev/null -d=ssa/prove/debug=2 <package import path>/...
```

sets debugging level to 2 in the prove pass
Multiple flags can be passed at once, by separating them with
commas.

For example:

```console
go compile -o /dev/null -d=ssa/check/on,ssa/all/time <package import path>/...
# or
go build -o /dev/null -d=ssa/check/on,ssa/all/time <package import path>/...
```
