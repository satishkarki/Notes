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

Both are ways to define different "modes" or states that a Linux system can be in after booting — like "normal multi-user mode", "single-user maintenance mode", "graphical desktop mode", "shutdown", etc.

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

### systemd configuration
When someone says systemd configuation, they usually means unit configuration file. We looked at the example of `.mount unit` above in `systemd` section.

As mentioned before, units are the building block of systemd. 

***Core Structure***
```bash
# Comments start with # or ; (ignored by systemd)
# Empty lines are also ignored

[SectionName]
Directive1=value
Directive2=value
Directive3=value1 value2 value3   # space-separated lists are common
Directive4="value with spaces or special chars"

[AnotherSection]
DirectiveA=yes
DirectiveB=no
DirectiveC=30s                    # many values support units like s, ms, min, h, etc.
```
 ***Example***
 ```bash
 [Unit]
Description=Nginx HTTP and reverse proxy server
Documentation=man:nginx(8)
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/sbin/nginx -g 'daemon on; master_process on;' -s reload
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

### systemd operation
`systemctl` is the main command-line tool for managing systemd. It lets you start/stop/reload units, check status, manage boot behavior (enable/disable), inspect the system, and more.

Request to activate, reactivate, and restart units are called `jobs` in systemd.

```bash
$ systemctl list-jobs
```
Key difference: reload vs restart

* reload → graceful, no downtime (sends SIGHUP or similar to the process)
* restart → full stop + start → brief downtime, but ensures clean state

***1. Basic Service Control (start / stop / restart / reload)***

| Command                              | What it does                                                                 | Example                                      | When to use it                                      |
|--------------------------------------|------------------------------------------------------------------------------|----------------------------------------------|-----------------------------------------------------|
| `systemctl start <unit>`             | Activates (starts) the unit if it's not already running                      | `sudo systemctl start nginx.service`         | Launch a stopped service                            |
| `systemctl stop <unit>`              | Deactivates (stops) the unit cleanly                                        | `sudo systemctl stop nginx.service`          | Gracefully shut down                                |
| `systemctl restart <unit>`           | Stops then starts the unit again (full cycle)                               | `sudo systemctl restart nginx.service`       | After config change that requires full restart      |
| `systemctl reload <unit>`            | Tells the unit to reload its configuration without stopping (if supported)  | `sudo systemctl reload nginx.service`        | Reload config (e.g., new virtual hosts in nginx/apache) without dropping connections |
| `systemctl reload-or-restart <unit>` | Smart: reloads if possible, otherwise restarts                              | `sudo systemctl reload-or-restart nginx`     | Safe default when unsure if reload is supported     |
| `systemctl try-restart <unit>`       | Restarts only if already running (no-op if stopped)                         | —                                            | Conditional restart                                 |

***2. Status & Inspection***
| Command                              | What it shows                                                                 | Example                                      |
|--------------------------------------|-------------------------------------------------------------------------------|----------------------------------------------|
| `systemctl status <unit>`            | Detailed status + last 10 journal lines + PID, memory usage, cgroup info, etc. | `systemctl status sshd`                      |
| `systemctl list-units`               | All currently loaded and active units (default: shows running ones)          | `systemctl` (shortcut)                       |
| `systemctl list-units --type=service`| Only service units (loaded and/or active)                                     | —                                            |
| `systemctl list-units --failed`      | Only units that are in failed state                                           | Great for quick troubleshooting              |
| `systemctl list-unit-files`          | All installed unit files + their enable/disable/static state                  | `systemctl list-unit-files --type=service`   |
| `systemctl cat <unit>`               | Shows the effective (merged) unit file content including overrides/drop-ins   | `systemctl cat nginx.service`                |

***3. Boot-time / Enable-Disable Behavior***
| Command                     | What it does                                                                 | Example                              |
|-----------------------------|------------------------------------------------------------------------------|--------------------------------------|
| `systemctl enable <unit>`   | Makes the unit start automatically at boot (creates symlinks in target.wants/) | `sudo systemctl enable nginx`        |
| `systemctl disable <unit>`  | Removes auto-start at boot (deletes the symlinks)                            | `sudo systemctl disable nginx`       |
| `systemctl is-enabled <unit>` | Checks the enable/disable state of the unit (returns "enabled", "disabled", "static", "masked", etc.) | `systemctl is-enabled sshd`          |
| `systemctl mask <unit>`     | Completely prevents the unit from being started (even manually) — very strong lock (creates symlink to /dev/null) | Rarely used, but good for locking out unwanted units |
| `systemctl unmask <unit>`   | Reverses a previous mask, allowing the unit to be started again             | —                                    |

***4. System-wide Actions***
| Command                  | What it does                                                                 |
|--------------------------|------------------------------------------------------------------------------|
| `systemctl reboot`       | Reboots the system (graceful shutdown + restart)                             |
| `systemctl poweroff`     | Powers off the system completely (graceful shutdown)                         |
| `systemctl halt`         | Halts the system (stops all processes and CPU, but does not power off)       |
| `systemctl suspend`      | Suspends the system to RAM (quick resume, low power usage)                   |
| `systemctl daemon-reload`| Reloads systemd manager configuration (must run after editing any unit files) |

### systemd process tracking and synchronization
