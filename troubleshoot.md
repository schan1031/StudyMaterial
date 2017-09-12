# Troubleshooting

### strace
- Debugging tool for troubleshooting
- Monitors system calls and signals for specific programs
- Useful for debugging execution of a program
- Traces execution sequence of a binary from start to end
- `-e` traces specific system call
- `-o` write to output file
- `-p` runs strace on a program already running by process id
- `-t` prints timestamp for each output line
- `-r` prints relative timestamp
- `-c` generates report of system calls

***Examples***
```bash
$ strace ls

execve("/bin/ls", ["ls"], [/* 68 vars */]) = 0
brk(NULL)                               = 0x1478000
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7fb595f9e000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=93137, ...}) = 0
mmap(NULL, 93137, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7fb595f87000
close(3)                                = 0
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
...
...
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 4), ...}) = 0
write(1, "bash  networksops.md  README.md "..., 49bash  networksops.md  README.md  troubleshoot.md
) = 49
close(1)                                = 0
close(2)                                = 0
exit_group(0)                           = ?
+++ exited with 0 +++


$ strace -e open ls

open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libpcre.so.3", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libdl.so.2", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libpthread.so.0", O_RDONLY|O_CLOEXEC) = 3
open("/proc/filesystems", O_RDONLY)     = 3
open("/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = 3
open(".", O_RDONLY|O_NONBLOCK|O_DIRECTORY|O_CLOEXEC) = 3
bash  networksops.md  README.md  troubleshoot.md
+++ exited with 0 +++
```

More details [here](http://www.thegeekstuff.com/2011/11/strace-examples).

### ltrace
- useful for debugging user-space application programs
- can default segfaults, can find which lines are issues
