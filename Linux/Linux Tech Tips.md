# Linux Tech Tips

This note is based  on the book -  `How Linux Works` - by Brain Ward.
---
## The Bourne Shell : /bin/sh

Linux uses an enhanced version of the Bourne shell called bash or the "Bourne-again" shell. `/bin/shell` is a link to bash in Linux. 
```bash
# To change Shell
chsh 
```
```bash
$ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/usr/bin/tmux
```
```shell
# MAN page for chsl
$ chsh -h
Usage: chsh [options] [LOGIN]

Options:
  -h, --help                    display this help message and exit
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             new login shell for the user account
```
```bash
# Example
$ chsh -s /usr/bin/tmux
```
---

## Basic Commands

```bash
cat # Output the contents of one or more file
$ cat /etc/passwd
```
```bash
$ ls # List the content of a directory
$ ls --help
$ ls -l #detailed long list
$ ls -R # list subdirectories recursively
$ ls -a # Don't ignore entries starting with .
```
```bash
$ cp file1 file2
$ cp file dir
$ cp file1 file2 file3 dir
```
```bash
$ mv file1 file2
```
```bash
$ touch file
```
```bash
$ rm file
```
```bash
$echo Hello Again.
Hello Again.
```
---

### Navigating Directories
```bash
/ -> root
../ -> parent directory
./ -> Current directory
```
```bash
$ cd dir # Change Directory
$ mkdir dir # Make Directory
$ rmdir dir # Remove Directory
```
---
### Shell Globbing
```bash
> at* expands to all files that start with at
> *at expands to all the files that end with at
> *at* expands to all files that contains at
> b?at expands to match exactly one arbitrary character # b?at matches boat and brat
```
---
## Intermediate Command
```bash
$ grep root /etc/passwd
# Output
root:x:0:0:root:/root:/bin/bash
nm-openvpn:x:121:122:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
```

less displays the content of a very large file one screenful at a time. To go to next page press space, to go back, press b, to quit q
```bash
$ grep ie /usr/share/dict/words | less
```
```bash
# print working directory
$ pwd
```
```bash
# difference between two files
$ diff file1 file2
```
```bash
# Check file or directory
$ file CCNA
CCNA: directory

$ file ./CCNA/CISCO\ commands 
./CCNA/CISCO commands: very short file (no magic)
```

