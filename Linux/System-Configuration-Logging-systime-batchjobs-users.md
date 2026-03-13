## The structure of `/etc`
Everything in here is meant to be human-readable text files or subdirectories that control how the entire system behaves. It is system-wide (applies to all users), owned by root, and survives reboots.

```bash
$ ls -F /etc
NetworkManager/         gtk-3.0/              python3/
apt/                    issue.net             rcS.d/
bash.bashrc             kernel/               resolv.conf@
```
***Extra***
```bash
$ ls -F /etc

-F: The option (flag) that adds a character to the end of each listed item to identify its type:

    /: Indicates a directory.
    *: Indicates an executable file.
    @: Indicates a symbolic link.
    |: Indicates a named pipe (FIFO).
    =: Indicates a socket.
    (no symbol): Indicates a regular file.
```
***Difference between `/etc/systemd/` and `/usr/lib/systemd`***
* /usr/lib/systemd/ = factory defaults from packages (hands off!)

* /etc/systemd/ = your custom layer that overrides everything else (this is where the action happens)

## System Logging
Modern Linux (pretty much everything since ~2015) uses two complementary logging systems that often run side-by-side:

* systemd-journald — the native, binary, structured logger built into systemd (default on virtually all current distributions)
* rsyslog (or sometimes syslog-ng) — the traditional text-based syslog daemon, still widely used for compatibility, file-based logs, remote logging, and enterprise habits

***Searching and Monitoring Logs***

`journalctl` is the primary tool for querying and displaying logs from the systemd journal (managed by systemd-journald).

It reads binary journal files (usually in `/var/log/journal/` if persistent, or `/run/log/journal/` if volatile) and presents them in a human-readable way, with rich filtering options.

1. Basic Usage and Navigation
    ```bash
    journalctl                  # Show all logs (oldest first, paged in less/more)
    journalctl -e               # Jump to the end (newest entries first — most common)
    journalctl -r               # Reverse order (newest first)
    journalctl -n 100           # Last 100 lines
    journalctl -f               # Follow / tail -f mode (real-time monitoring)
    ```
2. Time-based Filtering
    ```bash
    journalctl --since "2026-03-12 18:00"          # From specific date/time
    journalctl --since "yesterday"                 # Since midnight yesterday
    journalctl --since "1 hour ago"                # Last hour
    journalctl --since "2026-03-10" --until "2026-03-11 23:59"
    journalctl --since today -u ssh                # Today’s SSH logs only
    journalctl -S "2 days ago" -U now              # Shorthands: -S = --since, -U = --until
    ```
3. Boot-based Filtering
    ```bash
    journalctl -b                   # Current boot only (most common)
    journalctl -b -1                # Previous boot
    journalctl -b -2                # Two boots ago
    journalctl --list-boots         # Show all available boots with IDs and times
    journalctl -b 156019a44a774a0b  # By boot ID (from --list-boots)
    ```
4. Service/Unit Filtering
    ```bash
    journalctl -u ssh               # All sshd.service logs
    journalctl -u nginx.service -u php-fpm.service  # Multiple units
    journalctl -u "nginx*"          # Wildcard (all nginx-related units)
    journalctl -u ssh --since "1 hour ago" -f   # SSH last hour + follow live
    ```
5. Priority/Severity Filtering

    Priorities (0–7, lower number = more severe):

        0 emerg, 1 alert, 2 crit, 3 err, 4 warning, 5 notice, 6 info, 7 debug

    ```bash
    journalctl -p err               # Errors and worse (err, crit, alert, emerg)
    journalctl -p err -b            # Errors this boot
    journalctl -p 3..1              # Range: critical (1) to error (3)
    journalctl -p warning..emerg    # By name range
    journalctl -p debug -u myapp    # Debug level for specific service
    ```
6. Other Common Filtering 
    ```bash
    journalctl -k                   # Kernel messages only (like dmesg)
    journalctl _PID=1234            # By process ID
    journalctl _UID=1000            # By user ID (your user)
    journalctl _COMM=sshd           # By command name
    journalctl _SYSTEMD_UNIT=nginx.service  # Explicit field match
    journalctl grep "error\|failed" # Simple text search (case insensitive with -i)
    journalctl -g "authentication failure"  # Grep-style (same as above)
    journalctl -o json-pretty       # Structured output (JSON)
    journalctl -o verbose           # Show all fields (great for debugging)
    journalctl -x                   # Add explanations/catalog messages where available
    ```
7. Real Time Monitoring
    ```bash
    journalctl -f
    journalctl -u ssh -f -g "Failed password" # Watch SSH attempts live (great for spotting brute-force)
    journalctl -kf -p err # Watch kernel + errors live this boot
    ```
***Logfile Rotation***

Logfile rotation in Linux manages growing log files by periodically "rotating" them: renaming the current log (e.g., `/var/log/syslog` → `/var/log/syslog.1`), creating a fresh empty log file for new entries, optionally compressing old ones (.gz), and eventually deleting the oldest ones to prevent disk exhaustion.

**Core components of Log Rotation**
1. Main config → `/etc/logrotate.conf`

    Sets global defaults (e.g., weekly rotation, keep 4 old files, compress, create new file with 0640 permissions).
2. Package/service configs → `/etc/logrotate.d/` (directory)

    * Most real rules live here (one file per service, e.g., rsyslog, nginx, apache2, journald).
    * Packages install their own rotation rules here automatically.
3. Execution mechanism
    * Debian/Ubuntu family: Usually a script in `/etc/cron.daily/logrotate` (runs via anacron or cron once per day).
    * Fedora/RHEL family: Same approach — `/etc/cron.daily/logrotate` script, but sometimes systemd timers can be involved in newer setups.
## User Management Files
