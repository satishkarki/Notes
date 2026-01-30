After knowing how the Linux Kernel presents devices to userspace. Now its to look at how we can partition disks, create and maintain filesystems that goes inside disk partitions, and work with the swap space.

## Partitioning Disk Devices
* Partitons are the subdivisons of the whole disk
* Partitions are defined on a small area of the disk called partition table
* Two types of partition tables: Master Boot Record (MBR) and GUID Parttion Table (GPT)
* Linux Partitioning tools: `parted`, `gparted`, `fdisk`, `gdisk`

### Viewing Partition Table
```bash
$ sudo parted -l
# OR
$ fdisk -l
# OR
$ lsblk
```
```bash
# Output of 'parted -l'
Model: ATA Samsung SSD 870 EVO 1TB (scsi)
Disk /dev/sda: 1000GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system     Name     Flags
 1      1049kB  538MB   537MB   fat32           EFI      boot, esp
 2      538MB   4295MB  3757MB  ext4
 3      4295MB  1000GB  996GB   ext4

Model: WD My Passport 0820 (scsi)
Disk /dev/sdb: 2000GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type      File system  Flags
 1      1049kB  2000GB  2000GB  primary   ntfs         lba
 ```
```bash
# Output of fdisk -l 
sudo fdisk -l
Disk /dev/ram0: 4 MiB, 4194304 bytes, 8192 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/ram1: 4 MiB, 4194304 bytes, 8192 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
```

	

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
> Which one to choose: `fdisk` or `parted` ? 

{: .prompt-tip }
<!-- markdownlint-restore -->
With fdisk, you design your new partition table before making the actual changes to the disk, and it makes changes only when you exit the program. But with the parted, partitions are created, modified, and removed as you issue the command.

### Creating a Partition Table

#### Check and select the device 
In my case it is a flash drive and it is mounted as `/dev/sdb`, once the drive is selected, type `p` to print the current partition on the flash drive. 

```bash
$ lsscsi
$ sudo fdisk /dev/sdb
```
```bash
# Output
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.
...
...
...

# print the current table
Command (m for help): p

Disk /dev/sdb: 115.41 GiB, 123924905984 bytes, 242040832 sectors
Disk model: TESLADRIVE      
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B9083D28-1E94-45BC-A8A3-DA68BE09A9A9

Device       Start     End Sectors  Size Type
/dev/sdb1       64     635     572  286K Microsoft basic data
/dev/sdb2      636   17019   16384    8M EFI System
/dev/sdb3    17020 3577255 3560236  1.7G Apple HFS/HFS+
/dev/sdb4  3577256 3577855     600  300K Microsoft basic data
```
#### Deleting a partition
Here in my example, I am deleting `sdb3` using the command `d` and printing the output with `p`.
```bash
# deleting a partition
Command (m for help): d
Partition number (1-4, default 4): 3

Partition 3 has been deleted.

# print the partition again
Command (m for help): p
Disk /dev/sdb: 115.41 GiB, 123924905984 bytes, 242040832 sectors
Disk model: TESLADRIVE      
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B9083D28-1E94-45BC-A8A3-DA68BE09A9A9

Device       Start     End Sectors  Size Type
/dev/sdb1       64     635     572  286K Microsoft basic data
/dev/sdb2      636   17019   16384    8M EFI System
/dev/sdb4  3577256 3577855     600  300K Microsoft basic data
```
#### Creating a new partition
We can use `n` command to create a new partition. As seen in the below example, it will prompt you for the sector to choose, lets say you want to create multiple partition, one of them is 200MB then you will enter the first sector (default) and in the next line add `+200M`. 

But in my case, I am creating a partition on the remaining entire sectors. SO I will just hit `enter` twice.

```bash
Command (m for help): n
Partition number (3,5-176, default 3): 3
First sector (17020-242040786, default 3577856): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (3577856-242040786, default 242038783): 

Created a new partition 3 of type 'Linux filesystem' and of size 113.7 GiB.
```

Now if I check all the partitions available, I get the following result
```bash
Command (m for help): p
Disk /dev/sdb: 115.41 GiB, 123924905984 bytes, 242040832 sectors
Disk model: TESLADRIVE      
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B9083D28-1E94-45BC-A8A3-DA68BE09A9A9

Device       Start       End   Sectors   Size Type
/dev/sdb1       64       635       572   286K Microsoft basic data
/dev/sdb2      636     17019     16384     8M EFI System
/dev/sdb3  3577856 242038783 238460928 113.7G Linux filesystem
/dev/sdb4  3577256   3577855       600   300K Microsoft basic data

Partition table entries are not in disk order.

Command (m for help): 
```
In the above output, at the end it says, the partition table entries are not in the disk order. `sdb4`'s last sector is 3577855 and `sdb3`'s first sector is 3577856 which makes sense. It is a poor way to create partition and difficult to maintain.

#### Saving the changes
```bash
Command (m for help): w
The partition table has been altered.
Failed to remove partition 3 from system: No such device or address

The kernel still uses the old partitions. The new table will be used at the next reboot. 
Syncing disks.

```

#### Cleanest modern approach:
Use `gdisk` instead of `fdisk` for GPT disks — it has better tools for reordering/optimizing.

```bash
sudo gdisk /dev/sdb
```
Then inside gdisk:

    * s → sort partitions (reorders entries to match disk order)
    * p → verify
    * w → write

gdisk’s sort function often fixes this automatically without deleting anything.

## File System
I have gone in depth about the file system in my post [Head First Dive Into File System](https://satishkarki.com/posts/File-System/). So in this section, I will touch on the subject of creating, mounting  and remounting of the file system.

### Creating a Filesystem
```bash
sudo mkfs.<filesystem-type> [options] /dev/sdXn
# or the generic form (less common now):
sudo mkfs -t <filesystem-type> [options] /dev/sdXn
```
***Example***
```bash
sudo mkfs.ext4 /dev/sdb3           # Create ext4 filesystem
sudo mkfs.xfs -f /dev/nvme0n1p2    # Create XFS (force with -f if needed)
sudo mkfs.vfat -F 32 /dev/sdc1     # Create FAT32 for USB drive
sudo mkfs.btrfs -L mypool /dev/sdd # Create Btrfs with label "mypool"
```
***Behind the Hood***
`mkfs` is the front end, it is a symlink to a series of file creation utilities in '`sbin`.

```bash
$ ls -l /sbin/mkfs.*
```
```bash
# Output
-rwxr-xr-x 1 root root 22912 Sep 15 20:08 /sbin/mkfs.bfs
-rwxr-xr-x 1 root root 35144 Sep 15 20:08 /sbin/mkfs.cramfs
lrwxrwxrwx 1 root root     6 Apr 28  2024 /sbin/mkfs.ext2 -> mke2fs
lrwxrwxrwx 1 root root     6 Apr 28  2024 /sbin/mkfs.ext3 -> mke2fs
lrwxrwxrwx 1 root root     6 Apr 28  2024 /sbin/mkfs.ext4 -> mke2fs
-rwxr-xr-x 1 root root 52048 Mar 31  2024 /sbin/mkfs.fat
-rwxr-xr-x 1 root root 43408 Sep 15 20:08 /sbin/mkfs.minix
lrwxrwxrwx 1 root root     8 Mar 31  2024 /sbin/mkfs.msdos -> mkfs.fat
lrwxrwxrwx 1 root root     6 Apr  8  2024 /sbin/mkfs.ntfs -> mkntfs
lrwxrwxrwx 1 root root     8 Mar 31  2024 /sbin/mkfs.vfat -> mkfs.fat
```
### Mounting a FileSystem


