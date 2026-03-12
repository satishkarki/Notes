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

