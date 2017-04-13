# Provenance Semantics of Linux System Calls

## Summary

This document provides more detail regarding the generation of
provenance tags for Linux system calls. 

## Sources

A source is defined as a call that receives data (from the kernel) and
tags that data with a new provenance tag.  Not all data passed from the
kernel is tagged with provenance, i.e., not all return data from
system calls are sources.  We limit the generation of provenance tags
to data returned from the kernel for the
below list of calls.  

| System Call | System Call | System Call |
| ---- | ---- | ---- |
| _sysctl |  getdomainname | gethostname |
| getgroups | getpeername | ioctl |
| pread64 | pread | preadv  |
| read | readdir | readlink |
| readlinkat | recv | recvfrom |
| recvmmsg | recvmsg | syscall |

For the above calls, ValueType of VALUE_TYPE_SRC will be applied the
parameter(s) Values of the Event that will generate a provenance tag
and have the tag associated with the parameter's data.

## Sinks

A sink is defined as a call that passes data to the kernel (or other
mechanism beyond the app sandbox) and a tag is generated and
associated with the data.  When that data is then read again (into
another app), the tag will be associated with the data.

Currently, ClearScope does not track provenance through the kernel.
Currently we generate tags for calls that write to the filesystem or
to the Binder (IPC / RPC) device.  For the filesystem, tags are stored
in shadow files.  For Binder, tags are communicated with each value
communicated.  

The following calls have the potential to generate sink provenance
tags for data passed beyond the app sandbox.  For the calls, the
ValueType of VALUE_TYPE_SINK will be applied to the parameter Values
of the Event that will have the sink provenance tag associated through
the sink call.

| System Call | System Call | System Call |
| ---- | ---- | ---- |
|_sysctl | ioctl | pwrite64 |
|pwrite | pwritev | send |
|sendfile | sendmmsg | sendmsg |
|sendto | write | writev |
|syscall |  | |

## Non-provenance-generating Calls

The remainder of system calls will not generate provenance tags,
though the provenance tags on the control data passed to the kernel
will be reported by ClearScope.

| System Call | System Call | System Call |
| ---- | ---- | ---- |
|*getcwd | *mmap | *mmap2 |
|*mremap | *shmat | _exit |
|_llseek | accept | accept4 |
|access | acct | add_key |
|adjtimex | arch_prctl | bdflush |
|bind | brk | capget |
|capset | chdir | chmod |
|chown | chroot | clock_getres |
|clock_gettime | clock_nanosleep | clock_settime |
|clone  | close | connect |
|creat | delete_module | dup |
|dup2 | dup3 | epoll_create |
|epoll_create1 | epoll_ctl | epoll_pwait |
|epoll_wait | eventfd | execv |
|execve | exit_group | faccessat |
|fallocate | fanotify_init | fanotify_mark |
|fchdir | fchmod | fchmodat |
|fchown | fchownat | fcntl |
|fcntl64 | fdatasync | finit_module |
|flock | fork | fstat |
|fstat64 | fstatat | fstatfs |
|fstatfs64 | fsync | ftruncate |
|futex | futimesat | get_kernel_syms |
|get_mempolicy | get_robust_list | get_thread_area |
|getcpu | getdents | getdents64 |
|getegid | geteuid | getgid |
|getitimer | getpgid | getpid |
|getppid | getpriority | getresgid |
|getresuid | getrlimit | getrusage |
|getsid | getsockname | getsockopt |
|gettid | gettimeofday | getuid |
|init_module | inotify_add_watch | inotify_init |
|inotify_init1 | inotify_rm_watch | int alarm |
|io_cancel | io_destroy | io_getevents |
|io_setup | io_submit | ioperm |
|iopl | ioprio_get | ioprio_set |
|ipc | kcmp | kcmp |
|kexec_load | keyctl | kill |
|lchown | link | linkat |
|listen | lookup_dcookie | lseek |
|lstat | lstat64 | madvise |
|mbind | migrate_pages | mincore |
|mkdir | mkdirat | mknod |
|mknodat | mlock | mlockall |
|mount | move_pages | mprotect |
|mq_notify | mq_open | mq_timedreceive |
|mq_timedsend | mq_unlink | msgget |
|msgrcv | msgsnd | msync |
|munlock | munlockall | munmap |
|name_to_handle_at | nanosleep | nice |
|open | open_by_handle_at | openat |
|pause | pciconfig_iobase | pciconfig_read |
|pciconfig_write | perf_event_open | personality |
|pipe | pipe2 | pivot_root |
|poll | posix_fadvise | posix_fadvise64 |
|ppoll | prctl | pselect |
|ptrace | quotactl | readahead |
|readv | reboot | remap_file_pages |
|rename | renameat | renameat2 |
|request_key | restart_syscall | rmdir |
|rt_sigqueueinfo | rt_tgsigqueueinfo | sched_get_priority_max |
|sched_get_priority_min | sched_getaffinity | sched_getattr |
|sched_getparam | sched_getscheduler | sched_rr_get_interval |
|sched_setaffinity | sched_setattr | sched_setparam |
|sched_setscheduler | sched_yield | select |
|semctl | semget | semop |
|semtimedop | set_robust_list | set_thread_area |
|set_tid_address | setdomainname | setfsgid |
|setfsuid | setgid | setgroups |
|sethostname | setitimer | setns |
|setpgid | setpriority | setregid |
|setresgid | setresuid | setreuid |
|setrlimit | setsid | setsockopt |
|settimeofday | setuid | shutdown |
|sigaction | sigaltstack | signalfd |
|sigpending | sigprocmask | sigreturn |
|sigsuspend | socket | socketcall |
|socketpair | splice | stat |
|stat64 | statfs | statfs64 |
|stime | swapoff | swapon |
|symlink | symlinkat | sync |
|sync_file_range | syncfs | sysfs |
|sysinfo | syslog | tee |
|tgkill | time | timer_create |
|timer_delete | timer_getoverrun | timer_gettime |
|timer_settime | timerfd_create | timerfd_gettime |
|timerfd_settime | times | tkill |
|truncate | truncate64 | umask |
|umount | umount2 | uname |
|unlink | unlinkat | unshare |
|uselib | ustat | utime |
|utimensat | utimes | vfork |
|vhangup | vmsplice | wait4 |
|waitid | prlimit64 |  |
