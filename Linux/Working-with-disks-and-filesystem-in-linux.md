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


