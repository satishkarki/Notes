## A mental model of boot process
```bash
Firmware
  -> Bootloader
     -> kernel entry (arch asm)
        -> start_kernel() [C]
           -> initcalls (drivers/subsystems)
           -> mount initramfs or rootfs
           -> execve("/sbin/init")  => PID 1
              -> userspace boot continues
```

***Kernel Ring Buffer***
It is the Kernel's built-in circular log storage. To view the logs we can use the following commands.

```bash
$ dmesg | less 
$ dmesg -T #human readable timestamps
$ dmesg -w #follow new kernel message live
```
Unlike the ring buffer, the systemd journal is persistent. It is a userspace log store and keeps more history than the ring buffer.

```bash
journalctl -k -b            # kernel logs this boot
journalctl -k -b -1         # previous boot
journalctl -k -p err..alert # only errors and worse
```
***Kernel Parameters***
It is a settings string that tells the kernel how to boot and what environment it's in. The kernel exposes it at `/proc/cmdline`

```bash
$ cat /proc/cmdline

# I am using WSL
# Output
initrd=\initrd.img WSL_ROOT_INIT=1 panic=-1 nr_cpus=20 hv_utils.timesync_implicit=1 console=hvc0 debug pty.legacy_count=0 WSL_ENABLE_CRASH_DUMP=1
```

What is the keyparameter trying to say ?

This cmdline says: boot Linux in a WSL2/Hyper-V VM, use an initrd, use up to 20 CPUs, send kernel logs to the hypervisor console, enable Hyper-V time sync behavior, crank debug verbosity, don’t auto-reboot on panic, and enable WSL crash-dump related behavior.

---
## Boot Loaders
Here is a funny "chicken-and-egg" problem. 

The function of bootloader is to load the kernel into memory and then start the kernel with a set of kernel paramters.

But where is kernel and kernel parameter? They are somewhere on the root filesystems. But the kernel hasn't started yet !!

***Solution***: Staged Bootstrapping. 

Bootloader uses BIOS/UEFI to access disks. And modern bootloader has the capability to read the partition tables and have built-in support for read-only access to filesystem.

### GRUB
GRand Unified Bootloader (GRUB 2): its core job is to select and load a kernel + initramfs + cmdline, then jump into the kernel.



