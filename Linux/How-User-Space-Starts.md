## How User Space Starts?

First lets check, what is running as PID 1 in my WSL.
```bash
$ ps -p 1 -o pid,comm,args

# Output
PID     COMMAND         COMMAND
1       systemd         /sbin/init
```
Userspace “starts” at the exact moment the kernel successfully executes the first userspace program, called PID 1. Everything after that - services, login, networking - is launched by PID 1 (directly or indirectly).

---
## Intro to `init`

Init (short for "initialization") is the very first process that the Linux kernel starts after the system boots. 

Three main `init` listed in terms of efficency:
`system V` < `upstart` < `systemd`

***Runlevels and systemd targets***

Runlevels belongs to old Sys V init where as targets belongs to modern systemd init.

both ways to define different "modes" or states that a Linux system can be in after booting — like "normal multi-user mode", "single-user maintenance mode", "graphical desktop mode", "shutdown", etc.

```bash
# Example of Target
$ ls /etc/systemd/system/sysinit.target.wants/
apparmor.service        setvtrgb.service        systemd-resolved.service
keyboard-setup.service  systemd-pstore.service  systemd-timesyncd.service
```
```bash
# To check system's run level
$ who -r
run-level 5  2026-02-18 13:54
```
---
### `systemd`

Boot Flow
```bash
kernel → systemd (PID 1)
            ↓
   activates default.target
            ↓ (symlink)
   → graphical.target    OR    → multi-user.target
            ↓                              ↓
   starts display-manager       starts getty (text logins),
   (GDM/SDDM/…)                 cron, sshd, networking…
            ↓
   → login screen / desktop
```
If I check my WSL, here is the current default target
```bash
$ systemctl get-default

# Output
graphical.target
```
Ok, so what is a target? - A target is like a milestone or checkpoint during boot. It groups together many services/units that should be started together.

* multi-user.target : Full console/server mode
* graphical.target : Full desktop/graphical mode

So Target is a collection of Units. What are units? - These are the building blocks- almost everything systemd does is "activate/deactivate/manage a unit".

***Example***

```bash
# .mount unit
[Unit]
Description=Mount /data

[Mount]
What=/dev/sdb1
Where=/data
Type=ext4
Options=defaults

[Install]
WantedBy=multi-user.target
```
***Handy Commands to Explore Units***
```bash
# List all possible unit types
systemctl --type=help

# List all loaded units of a type
systemctl list-units --type=service
systemctl list-units --type=target

# Show everything systemd knows about a unit
systemctl cat nginx.service
systemctl show nginx.service

# List dependencies (what starts when this starts)
systemctl list-dependencies multi-user.target

# Find all timer units
systemctl list-timers --all
```

***Unit Types***
```bash
$ systemctl --type=help

# Output
Available unit types:
service # A process/daemon you want to start, stop, restart, supervise
mount # A filesystem mount point
swap # A swap file or partition
socket # A network socket, Unix socket, or FIFO — for socket activation
target # A synchronization point / group of other units (like old runlevels)
device # A kernel device (usually auto-generated from udev)
automount # On-demand mounting (mount only when accessed)
timer # A cron-like timer that activates another unit
path # Watches a file or directory for changes → activates a service
slice # A group for resource control (cgroups v2)
scope # Externally started processes grouped by systemd (e.g. via D-Bus)
```




