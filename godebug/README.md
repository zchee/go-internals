# GODEBUG

version: [devel +9ea6364a5e9f](https://github.com/golang/go/tree/9ea6364a5e9f)

## runtime

[go/src/src/runtime/extern.go#L24-L147@9ea6364a5e9f](https://github.com/golang/go/blob/9ea6364a5e9f/src/runtime/extern.go#L24-L147)

The `GODEBUG` variable controls debugging variables within the runtime.
It is a comma-separated list of name=val pairs setting these named variables:

### allocfreetrace

Setting `allocfreetrace=1` causes every allocation to be
profiled and a stack trace printed on each object's allocation and free.

### clobberfree

Setting `clobberfree=1` causes the garbage collector to
clobber the memory content of an object with bad content when it frees
the object.

### cgocheck

Setting `cgocheck=0` disables all checks for packages
using cgo to incorrectly pass Go pointers to non-Go code.

Setting `cgocheck=1` (the default) enables relatively cheap
checks that may miss some errors.  Setting cgocheck=2 enables
expensive checks that should not miss any errors, but will
cause your program to run slower.

### efence

Setting `efence=1` causes the allocator to run in a mode
where each object is allocated on a unique page and addresses are
never recycled.

### gccheckmark

Setting `gccheckmark=1` enables verification of the
garbage collector's concurrent mark phase by performing a
second mark pass while the world is stopped.  
If the second pass finds a reachable object that was not found by concurrent
mark, the garbage collector will panic.

### gcpacertrace

setting `gcpacertrace=1` causes the garbage collector to
print information about the internal state of the concurrent pacer.

### gcshrinkstackoff

Setting `gcshrinkstackoff=1` disables moving goroutines
onto smaller stacks. In this mode, a goroutine's stack can only grow.

### gcstoptheworld

setting `gcstoptheworld=1` disables concurrent garbage collection,
making every garbage collection a stop-the-world event.

Setting `gcstoptheworld=2` also disables concurrent sweeping after the garbage collection finishes.

### gctrace

Setting `gctrace=1` causes the garbage collector to emit a single line to standard
error at each collection, summarizing the amount of memory collected and the
length of the pause.

The format of this line is subject to change.

Currently, it is:

	gc # @#s #%: #+#+# ms clock, #+#/#/#+# ms cpu, #->#-># MB, # MB goal, # P

where the fields are as follows:

	gc #        the GC number, incremented at each GC
	@#s         time in seconds since program start
	#%          percentage of time spent in GC since program start
	#+...+#     wall-clock/CPU times for the phases of the GC
	#->#-># MB  heap size at GC start, at GC end, and live heap
	# MB goal   goal heap size
	# P         number of processors used

The phases are stop-the-world (STW) sweep termination, concurrent
mark and scan, and STW mark termination.  

The CPU times for mark/scan are broken down in to assist time (GC performed in
line with allocation), background GC time, and idle GC time.  

If the line ends with "(forced)", this GC was forced by a
runtime.GC() call.

### inittrace

Setting `inittrace=1` causes the runtime to emit a single line to standard
error for each package with init work, summarizing the execution time and memory
allocation.

No information is printed for inits executed as part of plugin loading
and for packages without both user defined and compiler generated init work.

The format of this line is subject to change. Currently, it is:

	init # @#ms, # ms clock, # bytes, # allocs

where the fields are as follows:

	init #      the package name
	@# ms       time in milliseconds when the init started since program start
	# clock     wall-clock time for package initialization work
	# bytes     memory allocated on the heap
	# allocs    number of heap allocations

### madvdontneed

Setting `madvdontneed=0` will use `MADV_FREE`
instead of `MADV_DONTNEED` on Linux when returning memory to the
kernel.

This is more efficient, but means RSS numbers will
drop only when the OS is under memory pressure.

### memprofilerate

Setting `memprofilerate=X` will update the value of runtime.MemProfileRate.

When set to 0 memory profiling is disabled.  Refer to the description of
MemProfileRate for the default value.

### invalidptr

`invalidptr=1` (the default) causes the garbage collector and stack
copier to crash the program if an invalid pointer value (for example, 1)
is found in a pointer-typed location.

Setting `invalidptr=0` disables this check.

This should only be used as a temporary workaround to diagnose buggy code.
The real fix is to not store integers in pointer-typed locations.

### sbrk

setting `sbrk=1` replaces the memory allocator and garbage collector
with a trivial allocator that obtains memory from the operating system and
never reclaims any memory.

### scavenge

`scavenge=1` enables debugging mode of heap scavenger.

### scavtrace

Setting `scavtrace=1` causes the runtime to emit a single line to standard
error, roughly once per GC cycle, summarizing the amount of work done by the
scavenger as well as the total amount of memory returned to the operating system
and an estimate of physical memory utilization.

The format of this line is subject to change, but currently it is:

	scav # # KiB work, # KiB total, #% util

where the fields are as follows:

	scav #       the scavenge cycle number
	# KiB work   the amount of memory returned to the OS since the last line
	# KiB total  the total amount of memory returned to the OS
	#% util      the fraction of all unscavenged memory which is in-use

If the line ends with `"(forced)"`, then scavenging was forced by a
debug.FreeOSMemory() call.

### scheddetail

Setting `schedtrace=X` and `scheddetail=1` causes the scheduler to emit
detailed multiline info every X milliseconds, describing state of the scheduler,
processors, threads and goroutines.

### schedtrace

Setting `schedtrace=X` causes the scheduler to emit a single line to standard
error every X milliseconds, summarizing the scheduler state.

### tracebackancestors

Setting `tracebackancestors=N` extends tracebacks with the stacks at
which goroutines were created, where N limits the number of ancestor goroutines to
report.

This also extends the information returned by runtime.Stack. Ancestor's goroutine
IDs will refer to the ID of the goroutine at the time of creation; it's possible for this
ID to be reused for another goroutine. Setting N to 0 will report no ancestry information.

### asyncpreemptoff

`asyncpreemptoff=1` disables signal-based asynchronous goroutine preemption.

This makes some loops non-preemptible for long periods, which may delay GC and
goroutine scheduling.

This is useful for debugging GC issues because it also disables the conservative stack scanning used
for asynchronously preempted goroutines.
