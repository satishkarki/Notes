## How User Space Starts?

First lets check, what is running as PID 1 in my WSL.
```bash
$ ps -p 1 -o pid,comm,args

# Output
    PID COMMAND         COMMAND
      1 systemd         /sbin/init
```
Userspace “starts” at the exact moment the kernel successfully executes the first userspace program, called PID 1. Everything after that - services, login, networking - is launched by PID 1 (directly or indirectly).

### Intro to `init`

Init (short for "initialization") is the very first process that the Linux kernel starts after the system boots. 

Three main `init` I like to list in terms of efficency:
`system V` < `upstart` < `systemd`

***Runlevels and systemd targets***

Runlevels and systemd targets are both ways to define different "modes" or states that a Linux system can be in after booting — like "normal multi-user mode", "single-user maintenance mode", "graphical desktop mode", "shutdown", etc.



