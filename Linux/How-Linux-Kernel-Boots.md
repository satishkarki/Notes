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

