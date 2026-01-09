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
