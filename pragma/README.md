# pragma

## general

//go:noescape
//go:noinline
//go:norace
//go:nosplit
//go:notinheap
//go:nowritebarrier
//go:nowritebarrierrec
//go:systemstack
//go:uintptrescapes
//go:yeswritebarrierrec

## binary-only-package

//go:binary-only-package

## cgo_dynamic_linker

//go:cgo_dynamic_linker "<path>"

## cgo_export_dynamic

//go:cgo_export_dynamic <local> <remote>
//go:cgo_export_dynamic __guard_local __guard_local
//go:cgo_export_dynamic __progname
//go:cgo_export_dynamic _cgo_panic
//go:cgo_export_dynamic _cgo_topofstack
//go:cgo_export_dynamic crosscall2
//go:cgo_export_dynamic environ
//go:cgo_export_dynamic main.main
//go:cgo_export_dynamic runtime.edata _edata
//go:cgo_export_dynamic runtime.end _end
//go:cgo_export_dynamic runtime.etext _etext

## cgo_export_static

//go:cgo_export_static <local> <remote>
//go:cgo_export_static _cgo_panic
//go:cgo_export_static _cgo_reginit
//go:cgo_export_static _cgo_topofstack
//go:cgo_export_static crosscall2
//go:cgo_export_static main
//go:cgo_export_static main.main
//go:cgo_export_static xx_cgo_panicmem xx_cgo_panicmem

## cgo_import_dynamic

//go:cgo_import_dynamic <local> [<remote> ["<library>"]]
//go:cgo_import_dynamic _ _ "/usr/lib/libSystem.B.dylib"
//go:cgo_import_dynamic _ _ "libsendfile.so"
//go:cgo_import_dynamic _ _ "libsocket.so"
//go:cgo_import_dynamic libc____errno ___errno "libc.so"
//go:cgo_import_dynamic libc___major __major "libc.so"
//go:cgo_import_dynamic libc___makedev __makedev "libc.so"
//go:cgo_import_dynamic libc___minor __minor "libc.so"
//go:cgo_import_dynamic libc___xnet_bind __xnet_bind "libsocket.so"
//go:cgo_import_dynamic libc___xnet_connect __xnet_connect "libsocket.so"
//go:cgo_import_dynamic libc___xnet_getsockopt __xnet_getsockopt "libsocket.so"
//go:cgo_import_dynamic libc___xnet_listen __xnet_listen "libsocket.so"
//go:cgo_import_dynamic libc___xnet_llisten __xnet_llisten "libsocket.so"
//go:cgo_import_dynamic libc___xnet_recvmsg __xnet_recvmsg "libsocket.so"
//go:cgo_import_dynamic libc___xnet_sendmsg __xnet_sendmsg "libsocket.so"
//go:cgo_import_dynamic libc___xnet_sendto __xnet_sendto "libsocket.so"
//go:cgo_import_dynamic libc___xnet_socket __xnet_socket "libsocket.so"
//go:cgo_import_dynamic libc___xnet_socketpair __xnet_socketpair "libsocket.so"
//go:cgo_import_dynamic libc_Getcwd getcwd "libc.so"
//go:cgo_import_dynamic libc_getcwd getcwd "libc.so"
//go:cgo_import_dynamic libc_gettimeofday gettimeofday "/usr/lib/libSystem.B.dylib"
//go:cgo_import_dynamic libc_Gettimeofday gettimeofday "libc.so"
//go:cgo_import_dynamic libc_gettimeofday gettimeofday "libc.so"
//go:cgo_import_dynamic runtime._AddVectoredExceptionHandler AddVectoredExceptionHandler%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._CloseHandle CloseHandle%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._CreateEventA CreateEventA%4 "kernel32.dll"
//go:cgo_import_dynamic runtime._CreateIoCompletionPort CreateIoCompletionPort%4 "kernel32.dll"
//go:cgo_import_dynamic runtime._CreateThread CreateThread%6 "kernel32.dll"
//go:cgo_import_dynamic runtime._CreateWaitableTimerA CreateWaitableTimerA%3 "kernel32.dll"
//go:cgo_import_dynamic runtime._DuplicateHandle DuplicateHandle%7 "kernel32.dll"
//go:cgo_import_dynamic runtime._ExitProcess ExitProcess%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._FreeEnvironmentStringsW FreeEnvironmentStringsW%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetConsoleMode GetConsoleMode%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetEnvironmentStringsW GetEnvironmentStringsW%0 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetProcAddress GetProcAddress%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetProcessAffinityMask GetProcessAffinityMask%3 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetQueuedCompletionStatus GetQueuedCompletionStatus%5 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetStdHandle GetStdHandle%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetSystemInfo GetSystemInfo%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._GetThreadContext GetThreadContext%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._LoadLibraryA LoadLibraryA%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._LoadLibraryW LoadLibraryW%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._ResumeThread ResumeThread%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetConsoleCtrlHandler SetConsoleCtrlHandler%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetErrorMode SetErrorMode%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetEvent SetEvent%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetProcessPriorityBoost SetProcessPriorityBoost%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetThreadPriority SetThreadPriority%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetUnhandledExceptionFilter SetUnhandledExceptionFilter%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._SetWaitableTimer SetWaitableTimer%6 "kernel32.dll"
//go:cgo_import_dynamic runtime._SuspendThread SuspendThread%1 "kernel32.dll"
//go:cgo_import_dynamic runtime._SwitchToThread SwitchToThread%0 "kernel32.dll"
//go:cgo_import_dynamic runtime._timeBeginPeriod timeBeginPeriod%1 "winmm.dll"
//go:cgo_import_dynamic runtime._timeEndPeriod timeEndPeriod%1 "winmm.dll"
//go:cgo_import_dynamic runtime._VirtualAlloc VirtualAlloc%4 "kernel32.dll"
//go:cgo_import_dynamic runtime._VirtualFree VirtualFree%3 "kernel32.dll"
//go:cgo_import_dynamic runtime._VirtualQuery VirtualQuery%3 "kernel32.dll"
//go:cgo_import_dynamic runtime._WaitForSingleObject WaitForSingleObject%2 "kernel32.dll"
//go:cgo_import_dynamic runtime._WriteConsoleW WriteConsoleW%5 "kernel32.dll"
//go:cgo_import_dynamic runtime._WriteFile WriteFile%5 "kernel32.dll"
//go:cgo_import_dynamic runtime._WSAGetOverlappedResult WSAGetOverlappedResult%5 "ws2_32.dll"

## cgo_import_static

//go:cgo_import_static <local>
//go:cgo_import_static __msan_free_go
//go:cgo_import_static __msan_malloc_go
//go:cgo_import_static __msan_read_go
//go:cgo_import_static __msan_write_go
//go:cgo_import_static __tsan_acquire
//go:cgo_import_static __tsan_finalizer_goroutine
//go:cgo_import_static __tsan_fini
//go:cgo_import_static __tsan_free
//go:cgo_import_static __tsan_func_enter
//go:cgo_import_static __tsan_func_exit
//go:cgo_import_static __tsan_go_atomic32_compare_exchange
//go:cgo_import_static __tsan_go_atomic32_exchange
//go:cgo_import_static __tsan_go_atomic32_fetch_add
//go:cgo_import_static __tsan_go_atomic32_load
//go:cgo_import_static __tsan_go_atomic32_store
//go:cgo_import_static __tsan_go_atomic64_compare_exchange
//go:cgo_import_static __tsan_go_atomic64_exchange
//go:cgo_import_static __tsan_go_atomic64_fetch_add
//go:cgo_import_static __tsan_go_atomic64_load
//go:cgo_import_static __tsan_go_atomic64_store
//go:cgo_import_static __tsan_go_end
//go:cgo_import_static __tsan_go_ignore_sync_begin
//go:cgo_import_static __tsan_go_ignore_sync_end
//go:cgo_import_static __tsan_go_start
//go:cgo_import_static __tsan_init
//go:cgo_import_static __tsan_malloc
//go:cgo_import_static __tsan_map_shadow
//go:cgo_import_static __tsan_proc_create
//go:cgo_import_static __tsan_proc_destroy
//go:cgo_import_static __tsan_read
//go:cgo_import_static __tsan_read_pc
//go:cgo_import_static __tsan_read_range
//go:cgo_import_static __tsan_release
//go:cgo_import_static __tsan_release_merge
//go:cgo_import_static __tsan_report_count
//go:cgo_import_static __tsan_write
//go:cgo_import_static __tsan_write_pc
//go:cgo_import_static __tsan_write_range
//go:cgo_import_static _cgo_yield
//go:cgo_import_static _cgoPREFIX_Cfunc__Cmalloc
//go:cgo_import_static x_cgo_callers
//go:cgo_import_static x_cgo_init
//go:cgo_import_static x_cgo_mmap
//go:cgo_import_static x_cgo_munmap
//go:cgo_import_static x_cgo_notify_runtime_init_done
//go:cgo_import_static x_cgo_set_context_function
//go:cgo_import_static x_cgo_setenv
//go:cgo_import_static x_cgo_sigaction
//go:cgo_import_static x_cgo_sys_thread_create
//go:cgo_import_static x_cgo_thread_start
//go:cgo_import_static x_cgo_unsetenv

## cgo_ldflag

//go:cgo_ldflag "<arg>"

## cgo_unsafe_args

//go:cgo_unsafe_args

## generate

//go:generate -command run echo Now is the time
//go:generate ./mkalldocs.sh
//go:generate bundle -o h2_bundle.go -prefix http2 -underscore golang.org/x/net/http2
//go:generate bundle -o socks_bundle.go -dst net/http -prefix socks -underscore golang.org/x/net/internal/socks
//go:generate echo $GOARCH $GOFILE:$GOLINE ${GOPACKAGE}abc xyz$GOPACKAGE/$GOFILE/123
//go:generate echo hello world
//go:generate echo no, no, a thousand times no
//go:generate echo oh yes my man
//go:generate echo Success
//go:generate env ZONEINFO=$GOROOT/lib/time/zoneinfo.zip go run genzabbrs.go -output zoneinfo_abbrs_windows.go
//go:generate go run $GOROOT/src/syscall/mksyscall_windows.go -output zsyscall_windows.go eventlog.go service.go syscall_windows.go security_windows.go
//go:generate go run $GOROOT/src/syscall/mksyscall_windows.go -output zsyscall_windows.go syscall.go
//go:generate go run $GOROOT/src/syscall/mksyscall_windows.go -output zsyscall_windows.go syscall_windows.go security_windows.go psapi_windows.go
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p arm
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p arm64
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p mips
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p ppc64
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p s390x
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p wasm
//go:generate go run ../stringer.go -i $GOFILE -o anames.go -p x86
//go:generate go run decgen.go -output dec_helpers.go
//go:generate go run encgen.go -output enc_helpers.go
//go:generate go run gen.go
//go:generate go run gen.go -full -output md5block.go
//go:generate go run gen.go -output palette.go
//go:generate go run gengoos.go
//go:generate go run genzfunc.go
//go:generate go run make_tables.go
//go:generate go run makeisprint.go -output isprint.go
//go:generate go run maketables.go -tables=all -output tables.go
//go:generate go run mkbuiltin.go
//go:generate go run mkduff.go
//go:generate go run mkfastlog2table.go
//go:generate go run mksizeclasses.go
//go:generate go run mksyscall_windows.go -systemdll -output zsyscall_windows.go syscall_windows.go security_windows.go
//go:generate go run root_darwin_arm_gen.go -output root_darwin_armx.go
//go:generate go run wincallback.go
//go:generate run for all good men
//go:generate stringer -type AddrType
//go:generate stringer -type attr
//go:generate stringer -type Attr -trimprefix=Attr
//go:generate stringer -type delim
//go:generate stringer -type element
//go:generate stringer -type EType -trimprefix T
//go:generate stringer -type jsCtx
//go:generate stringer -type Op -trimprefix Op
//go:generate stringer -type Operator -linecomment
//go:generate stringer -type state
//go:generate stringer -type Tag -trimprefix=Tag
//go:generate stringer -type token -linecomment
//go:generate stringer -type urlPart
//go:generate stringer -type=Accuracy
//go:generate stringer -type=Class
//go:generate stringer -type=Op -trimprefix=O
//go:generate stringer -type=RelocType
//go:generate stringer -type=RelocTypeGeneric,RelocTypeX86_64,RelocTypeARM,RelocTypeARM64 -output reloctype_string.go
//go:generate stringer -type=RoundingMode
//go:generate stringer -type=SymKind

## linkname

//go:linkname ___ps_strings __ps_strings
//go:linkname __cgofn__cgoPREFIX_Cfunc__Cmalloc _cgoPREFIX_Cfunc__Cmalloc
//go:linkname __tsan_acquire __tsan_acquire
//go:linkname __tsan_finalizer_goroutine __tsan_finalizer_goroutine
//go:linkname __tsan_fini __tsan_fini
//go:linkname __tsan_free __tsan_free
//go:linkname __tsan_go_end __tsan_go_end
//go:linkname __tsan_go_ignore_sync_begin __tsan_go_ignore_sync_begin
//go:linkname __tsan_go_ignore_sync_end __tsan_go_ignore_sync_end
//go:linkname __tsan_go_start __tsan_go_start
//go:linkname __tsan_init __tsan_init
//go:linkname __tsan_malloc __tsan_malloc
//go:linkname __tsan_map_shadow __tsan_map_shadow
//go:linkname __tsan_proc_create __tsan_proc_create
//go:linkname __tsan_proc_destroy __tsan_proc_destroy
//go:linkname __tsan_release __tsan_release
//go:linkname __tsan_release_merge __tsan_release_merge
//go:linkname __tsan_report_count __tsan_report_count
//go:linkname _cgo_callers _cgo_callers
//go:linkname _cgo_init _cgo_init
//go:linkname _cgo_mmap _cgo_mmap
//go:linkname _cgo_munmap _cgo_munmap
//go:linkname _cgo_notify_runtime_init_done _cgo_notify_runtime_init_done
//go:linkname _cgo_panic _cgo_panic
//go:linkname _cgo_runtime_cgocall runtime.cgocall
//go:linkname _cgo_runtime_cgocallback runtime.cgocallback
//go:linkname _cgo_runtime_gobytes runtime.gobytes
//go:linkname _cgo_runtime_gostring runtime.gostring
//go:linkname _cgo_runtime_gostringn runtime.gostringn
//go:linkname _cgo_set_context_function _cgo_set_context_function
//go:linkname _cgo_setenv runtime._cgo_setenv
//go:linkname _cgo_sigaction _cgo_sigaction
//go:linkname _cgo_sys_thread_create _cgo_sys_thread_create
//go:linkname _cgo_thread_start _cgo_thread_start
//go:linkname _cgo_unsetenv runtime._cgo_unsetenv
//go:linkname _cgo_yield _cgo_yield
//go:linkname _cgoCheckPointer runtime.cgoCheckPointer
//go:linkname _cgoCheckResult runtime.cgoCheckResult
//go:linkname _environ environ
//go:linkname _guard_local __guard_local
//go:linkname _iscgo runtime.iscgo
//go:linkname _progname __progname
//go:linkname _runtime_cgo_panic_internal runtime._cgo_panic_internal
//go:linkname _runtime_cgocallback runtime.cgocallback
//go:linkname bytes_Compare bytes.Compare
//go:linkname bytes_IndexByte bytes.IndexByte
//go:linkname compileCallback syscall.compileCallback
//go:linkname executablePath os.executablePath
//go:linkname libc____errno libc____errno
//go:linkname libc___xnet_bind libc___xnet_bind
//go:linkname libc___xnet_connect libc___xnet_connect
//go:linkname libc___xnet_getsockopt libc___xnet_getsockopt
//go:linkname libc___xnet_listen libc___xnet_listen
//go:linkname libc___xnet_recvmsg libc___xnet_recvmsg
//go:linkname libc___xnet_sendmsg libc___xnet_sendmsg
//go:linkname libc___xnet_sendto libc___xnet_sendto
//go:linkname libc___xnet_socket libc___xnet_socket
//go:linkname libc___xnet_socketpair libc___xnet_socketpair
//go:linkname libc_accept libc_accept
//go:linkname libc_Access libc_Access
//go:linkname libc_Adjtime libc_Adjtime
//go:linkname libc_Chdir libc_Chdir
//go:linkname libc_chdir libc_chdir
//go:linkname libc_Chmod libc_Chmod
//go:linkname libc_Chown libc_Chown
//go:linkname libc_Chroot libc_Chroot
//go:linkname libc_chroot libc_chroot
//go:linkname libc_clock_gettime libc_clock_gettime
//go:linkname libc_Close libc_Close
//go:linkname libc_close libc_close
//go:linkname libc_Dup libc_Dup
//go:linkname libc_execve libc_execve
//go:linkname libc_exit libc_exit
//go:linkname libc_Fchdir libc_Fchdir
//go:linkname libc_Fchmod libc_Fchmod
//go:linkname libc_Fchown libc_Fchown
//go:linkname libc_fcntl libc_fcntl
//go:linkname libc_forkx libc_forkx
//go:linkname libc_Fpathconf libc_Fpathconf
//go:linkname libc_Fstat libc_Fstat
//go:linkname libc_Fsync libc_Fsync
//go:linkname libc_Ftruncate libc_Ftruncate
//go:linkname libc_getcontext libc_getcontext
//go:linkname libc_Getcwd libc_Getcwd
//go:linkname libc_Getdents libc_Getdents
//go:linkname libc_Getegid libc_Getegid
//go:linkname libc_Geteuid libc_Geteuid
//go:linkname libc_getexecname libc_getexecname
//go:linkname libc_Getgid libc_Getgid
//go:linkname libc_getgroups libc_getgroups
//go:linkname libc_gethostname libc_gethostname
//go:linkname libc_getpeername libc_getpeername
//go:linkname libc_Getpid libc_Getpid
//go:linkname libc_getpid libc_getpid
//go:linkname libc_Getppid libc_Getppid
//go:linkname libc_Getpriority libc_Getpriority
//go:linkname libc_Getrlimit libc_Getrlimit
//go:linkname libc_getsockname libc_getsockname
//go:linkname libc_Gettimeofday libc_Gettimeofday
//go:linkname libc_Getuid libc_Getuid
//go:linkname libc_ioctl libc_ioctl
//go:linkname libc_Kill libc_Kill
//go:linkname libc_kill libc_kill
//go:linkname libc_Lchown libc_Lchown
//go:linkname libc_Link libc_Link
//go:linkname libc_lseek libc_lseek
//go:linkname libc_Lstat libc_Lstat
//go:linkname libc_madvise libc_madvise
//go:linkname libc_malloc libc_malloc
//go:linkname libc_Mkdir libc_Mkdir
//go:linkname libc_Mknod libc_Mknod
//go:linkname libc_mmap libc_mmap
//go:linkname libc_munmap libc_munmap
//go:linkname libc_Nanosleep libc_Nanosleep
//go:linkname libc_Open libc_Open
//go:linkname libc_open libc_open
//go:linkname libc_Pathconf libc_Pathconf
//go:linkname libc_pipe libc_pipe
//go:linkname libc_port_associate libc_port_associate
//go:linkname libc_port_create libc_port_create
//go:linkname libc_port_dissociate libc_port_dissociate
//go:linkname libc_port_getn libc_port_getn
//go:linkname libc_Pread libc_Pread
//go:linkname libc_pthread_attr_destroy libc_pthread_attr_destroy
//go:linkname libc_pthread_attr_getstack libc_pthread_attr_getstack
//go:linkname libc_pthread_attr_init libc_pthread_attr_init
//go:linkname libc_pthread_attr_setdetachstate libc_pthread_attr_setdetachstate
//go:linkname libc_pthread_attr_setstack libc_pthread_attr_setstack
//go:linkname libc_pthread_create libc_pthread_create
//go:linkname libc_Pwrite libc_Pwrite
//go:linkname libc_raise libc_raise
//go:linkname libc_read libc_read
//go:linkname libc_Readlink libc_Readlink
//go:linkname libc_recvfrom libc_recvfrom
//go:linkname libc_Rename libc_Rename
//go:linkname libc_Rmdir libc_Rmdir
//go:linkname libc_sched_yield libc_sched_yield
//go:linkname libc_select libc_select
//go:linkname libc_sem_init libc_sem_init
//go:linkname libc_sem_post libc_sem_post
//go:linkname libc_sem_reltimedwait_np libc_sem_reltimedwait_np
//go:linkname libc_sem_wait libc_sem_wait
//go:linkname libc_sendfile libc_sendfile
//go:linkname libc_Setegid libc_Setegid
//go:linkname libc_Seteuid libc_Seteuid
//go:linkname libc_Setgid libc_Setgid
//go:linkname libc_setgid libc_setgid
//go:linkname libc_setgroups libc_setgroups
//go:linkname libc_setitimer libc_setitimer
//go:linkname libc_Setpgid libc_Setpgid
//go:linkname libc_setpgid libc_setpgid
//go:linkname libc_Setpriority libc_Setpriority
//go:linkname libc_Setregid libc_Setregid
//go:linkname libc_Setreuid libc_Setreuid
//go:linkname libc_Setrlimit libc_Setrlimit
//go:linkname libc_Setsid libc_Setsid
//go:linkname libc_setsid libc_setsid
//go:linkname libc_setsockopt libc_setsockopt
//go:linkname libc_Setuid libc_Setuid
//go:linkname libc_setuid libc_setuid
//go:linkname libc_shutdown libc_shutdown
//go:linkname libc_sigaction libc_sigaction
//go:linkname libc_sigaltstack libc_sigaltstack
//go:linkname libc_sigprocmask libc_sigprocmask
//go:linkname libc_Stat libc_Stat
//go:linkname libc_Symlink libc_Symlink
//go:linkname libc_Sync libc_Sync
//go:linkname libc_syscall libc_syscall
//go:linkname libc_sysconf libc_sysconf
//go:linkname libc_Truncate libc_Truncate
//go:linkname libc_Umask libc_Umask
//go:linkname libc_Unlink libc_Unlink
//go:linkname libc_usleep libc_usleep
//go:linkname libc_utimensat libc_utimensat
//go:linkname libc_utimes libc_utimes
//go:linkname libc_wait4 libc_wait4
//go:linkname libc_write libc_write
//go:linkname main_init main.init
//go:linkname main_main main.main
//go:linkname mutexevent sync.event
//go:linkname plugin_lastmoduleinit plugin.lastmoduleinit
//go:linkname proc__major libc___major
//go:linkname proc__makedev libc___makedev
//go:linkname proc__minor libc___minor
//go:linkname proc__xnet_bind libc___xnet_bind
//go:linkname procGetcwd libc_getcwd
//go:linkname readGCStats runtime/debug.readGCStats
//go:linkname reflect_chancap reflect.chancap
//go:linkname sync_atomic_CompareAndSwapPointer sync/atomic.CompareAndSwapPointer
