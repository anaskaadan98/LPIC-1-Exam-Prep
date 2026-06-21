---
Weight: "2"
---
# Introduction

A partition is a logical subset of the physical disk, and information about partitions are stored in a partition table. This table includes information about the first and last sectors of the partition and its type, and further details on each partition.

Usually each partition is seen by an operating system as a separate "disk", even if they all reside in the same physical media.

# Understanding MBR and GPT

**MBR**: The partition table is stored on the first sector of a disk, called the *Boot sector*, along with a boot loader, which on Linux systems is usually the *GRUB* bootloader. (This is common with *BIOS*)

**GUID**: A partitioning system that addresses many of the limitations of MBR. There is no practical limit on disk size, and the maximum number of partitions are limited only by the operating system itself. (This is common with *UFEI*)

## Managing MBR Partitions with FDISK

`fdisk` is an interactive, menu-driven utility.

### Basic Syntax

```bash
fdisk <Disk-Name>
```

> [!Note]
> All disk-related operations in this lesson need to be done as the user `root`, or with `root` privileges using `sudo`.

When invoked, `fdisk` will show a greeting, then a warning and it will wait for your commands.

#### Common commands

| Command    | Purpose                        |
| ---------- | ------------------------------ |
| `fdisk -l` | List partitions                |
| `n`        | Create partition               |
| `d`        | Delete partition               |
| `t`        | Change type                    |
| `p`        | Print table                    |
| `v`        | Verify table                   |
| `w`        | Save changes                   |
| `q`        | Quit without saving            |
| `g`        | Create GPT                     |
| `o`        | Create MBR                     |
| `m`        | Help                           |
| `F`        | Checking for unallocated Space |

**Printing the Current Partition Table**
The command `p` is used to print the current partition table. The output is something like this:

```block
Command (m for help): p

Disk /dev/nvme0n1: 1.86 TiB, 2048408248320 bytes, 4000797360 sectors
Disk model: PC SN810 NVMe WDC 2048GB                
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 1299D063-7B5E-44DD-A705-B052029C9AA8

Device             Start        End    Sectors  Size Type
/dev/nvme0n1p1      2048    1050623    1048576  512M EFI System
/dev/nvme0n1p2   1050624    3147775    2097152    1G Linux filesystem
/dev/nvme0n1p3   3147776  100804607   97656832 46.6G Linux filesystem
/dev/nvme0n1p4 100804608  139868159   39063552 18.6G Linux filesystem
/dev/nvme0n1p5 139868160 4000794623 3860926464  1.8T Linux filesystem
```

| Column      | Purpose                                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------------------- |
| **Device**  | The device assigned to the partition                                                                            |
| **Boot**    | Show whether the partition is "bootable" or not                                                                 |
| **Start**   | The sector where the partition starts                                                                           |
| **End**     | The sector where the partition ends                                                                             |
| **Sectors** | The total number of sectors in the partition. Multiply it by the sector size to get the partition size in bytes |
| **Size**    | The size of the partition in "human readable" format                                                            |
| **Id**      | The numerical value representing the partition type                                                             |
| **Type**    | The description of the partition type.                                                                          |

## Primary vs Extended Partitions

On **MBR** disks, you get at most *4 primary partition entries*. To have more than 4 usable partitinos, make one of those entries an **extended partition**, then create multiple **logical partitions** inside it. Linux generally doesn't care whether a filesystem is on a primary partition or a logical partition.

| Type     | Purpose                                            |
| -------- | -------------------------------------------------- |
| Primary  | Normal partition                                   |
| Extended | Container for logical partitions                   |
| Logical  | Partitions that live inside the extended partition |
## Changing the Partition Type

The partition type must be specified by its corresponding hexadecimal code, and you can see a list of all the valid codes by using the command `l`

```block
Command (m for help): l
  1 EFI System                     C12A7328-F81F-11D2-BA4B-00A0C93EC93B
  2 MBR partition scheme           024DEE41-33E7-11D3-9D69-0008C781F39F
  3 Intel Fast Flash               D3BFE2DE-3DAF-11DF-BA40-E3A556D89593
  4 BIOS boot                      21686148-6449-6E6F-744E-656564454649
  5 Sony boot partition            F4019732-066E-4E12-8273-346C5641494F
  6 Lenovo boot partition          BFBFAFE7-A34F-448A-9A5B-6213EB736C22
  7 PowerPC PReP boot              9E1A2D38-C612-4316-AA26-8B49521E5A8B
  8 ONIE boot                      7412F7D5-A156-4B13-81DC-867174929325
  9 ONIE config                    D4E6E2CD-4469-46F3-B5CB-1BFF57AFC149
 10 Microsoft reserved             E3C9E316-0B5C-4DB8-817D-F92DF00215AE
 11 Microsoft basic data           EBD0A0A2-B9E5-4433-87C0-68B6B72699C7
 12 Microsoft LDM metadata         5808C8AA-7E8F-42E0-85D2-E1E90434CFB3
 13 Microsoft LDM data             AF9B60A0-1431-4F62-BC68-3311714A69AD
 14 Windows recovery environment   DE94BBA4-06D1-4D40-A16A-BFD50179D6AC
 15 IBM General Parallel Fs        37AFFC90-EF7D-4E96-91C3-2D7AE055B174
 16 Microsoft Storage Spaces       E75CAF8F-F680-4CEE-AFA3-B001E56EFC2D
 17 HP-UX data                     75894C1E-3AEB-11D3-B7C1-7B03A0000000
 18 HP-UX service                  E2A1E728-32E3-11D6-A682-7B03A0000000
 19 Linux swap                     0657FD6D-A4AB-43C4-84E5-0933C84B4F4F
 20 Linux filesystem               0FC63DAF-8483-4772-8E79-3D69D8477DE4
 21 Linux server data              3B8F8425-20E0-4F3B-907F-1A25A76F98E8
 22 Linux root (x86)               44479540-F297-41B2-9AF7-D131D5F0458A
 23 Linux root (x86-64)            4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709
:
```


## Managing GUID Partitions with GDISK

The utility `gdisk` is the equivalent of `fdisk` when dealing with GPT partitioned disks. 

One major improvement over MBR is that GPT stores **redundant metadata**:
1. A **primary GPT header** and partition table at the beginning of the disk
2. A **backup GPT header** and partition table at the end of the disk

```block
+----------------------------------------------------------------+
| Main Header | Main Table | Data | Backup Table | Backup Header |
+----------------------------------------------------------------+
Beginning of Disk                                      End of Disk
```

If one copy gets corrupted, the other can often be used to restore it.

![[Create partitions and filesystems#Common commands]]

**Recovery Options**

GPT disks store backup copies of the GPT header and partition table, making it easy to recover disks in case this data has been damaged. `gdisk` provides features to aid in those recovery tasks, accessed with the r command.

| Options | Purpose                                                |
| ------- | ------------------------------------------------------ |
| `b`     | Rebuild the main GPT header from the backup copy       |
| `c`     | Rebuild the main partition table from the backup copy  |
| `d`     | Rebuild the backup GPT header from the main header     |
| `e`     | Rebuild the backup partition table from the main table |
| `f`     | Convert MBR -> GPT                                     |
| `g`     | Convert GPT -> MBR                                     |
| `?`     | Display all recovery commands and descriptions         |
## Creating File Systems

Partitioning divides the disk, while formatting creates the structure that allows files and directories to exist inside those partitions.

**Common Linux Filesystems**

| Filesystem | Origin     | Notes                            |
| ---------- | ---------- | -------------------------------- |
| `ext4`     | Linux      | Most common Linux filesystem     |
| `ext3`     | Linux      | Older version of ext4            |
| `ext2`     | Linux      | Very old Linux filesystem        |
| `XFS`      | Linux      | Good for large files and servers |
| `Btrfs`    | Linux      | Advanced features like snapshots |
| `FAT32`    | MS-DOS     | Widely compatible                |
| `exFAT`    | Mircorsoft | Common on USB drives             |
| `NTFS`     | Windows    | Default Windows filesystem       |
| `HFS+`     | macOS      | Older Mac filesystem             |
| `APFS`     | macOS      | Modern Apple filesystem          |

### The `mkfs` Command

Linux uses **mkfs** (**Make FileSystem**) to create filesystems

**General Syntax**

```bash
mkfs [options] -t <filesystem_type> <device>
```

**Common options**

| Option       | Meaning                                              |
| ------------ | ---------------------------------------------------- |
| `-t`         | Specify filesystem type                              |
| `-V`         | Verbose mode (show what is being executed)           |
| `-h`         | Display help                                         |
| `-n`         | Dry run (show what would be done without formatting) |
| `-L LABEL`   | Assign a filesystem label                            |
| `-m PERCENT` | Reserve space for root                               |
| `-b SIZE`    | Set block size                                       |
| `-F`         | Force creation even if device looks mounted          |

**Common commands**

| Command      | Creates          |
| ------------ | ---------------- |
| `mkfs.ext4`  | ext4 filesystem  |
| `mkfs.ext3`  | ext3 filesystem  |
| `mkfs.ext2`  | ext2 filesystem  |
| `mkfs.xfs`   | XFS filesystem   |
| `mkfs.btrfs` | Btrfs filesystem |
| `mkfs.fat`   | FAT filesystem   |
| `mkfs.ntfs`  | NTFS filesystem  |

## Getting to know the `Btrfs` filesystem

A modern, copy-on-write (CoW) file system for Linux. It is designed to handle large storage capacities while offering advanced features like built-in-snapshots, data itegrity checks, compression, and native software RAID capabilities

**Creating a Btrfs Filesystem**

```bash
mkfs.btrfs /dev/sdb1
```

**Managing Subvolumes**

A **subvolume** in Btrfs is like a separate filesystem inside a larger Btrfs filesystem.

Unlink normal directories, subvolumes can:
- Be mounted independently
- Have their own snapshots
- Be sent/received for backups
- Be managed separately

**Working with Snapshots**

Snapshots are just like subvolumes, but pre-populated with the contents from the volume from which the snapshot was taken.

**Most Common Commands**

| Task                      | Command                                      |
| ------------------------- | -------------------------------------------- |
| Create subvolume          | `btrfs subvolume create /path`               |
| List subvolumes           | `btrfs subvolume list /mountpoint`           |
| Show details              | `btrfs subvolume show /path`                 |
| Mount subvolume           | `mount -o subvol=name device mountpoint`     |
| Create snapshot           | `btrfs subvolume snapshot source dest`       |
| Create read-only snapshot | `btrfs subvolume snapshot -r source dest`    |
| Delete subvolume          | `btrfs subvolume delete /path`               |
| Get default subvolume     | `btrfs subvolume get-default /mountpoint`    |
| Set default subvolume     | `btrfs subvolume set-default ID /mountpoint` |

## Managing Partitions with GNU Parted

GNU Parted is a very powerful partition editor that can be used to create, delete, move, resize, rescue and copy partitions. It can work with both GPT and MBR disks, and cover almost all of your disk management needs.

**Basic Syntax**:

```bash
parted <device-name> <command> <option>
```


**Common Commands**

| Command      | Purpose                        |
| ------------ | ------------------------------ |
| `print`      | Show partition table           |
| `mklabel`    | Create a partition table       |
| `mkpart`     | Create a partition             |
| `rm`         | Remove a partition             |
| `resizepart` | Resize a partition             |
| `name`       | Name a GPT partition           |
| `set`        | Enable/disable partition flags |
| `quit`       | Exit parted                    |
| `help`       | Show Help                      |
**Common Flag**

| Flag   | Purpose                 |
| ------ | ----------------------- |
| `boot` | BIOS bootable partition |
| `esp`  | EFI System Partition    |
| `lvm`  | LVM physical volume     |
| `raid` | Software RAID           |
| `swap` | Linux swap partition    |

**Creating a Partition**

To create a partition the command `mkpart` is used, using the syntax:

```bash
mkpart <parttype> <fstype> <start> <end>
```

**PARTTYPE**: Is the partition type, which can be primary, logical or extended in case an MBR partition table is used.
**FSTYPE**: Specifies which filesystem will be used on this partition. Note that `parted` will not create the filesystem. It just sets a flag on the partition which tells the OS what kind of data to expect from it.
**START**: Specifies the exact point on the device where the partition begins. You can use different units to specify this point. `2s` can used to refer to the second sector of the disk, while `1m` refers to the beginning of the first megabyte of the disk.
**END**: Specifies the end of the partition.

## Resizing ext2/3/4 Partitions

`parted` can be used to resize partitions to make them bigger or smaller. However, there are some caveats:
- During resizing the partition must be unused and unmounted.
- You need enough free space *after* the partition to grow it to the size you want.

The command is `resizepart`, followed by the partition number and where it should end. But resizing the partition is only one part of the task. You also need to resize the filesystem that resides in it. For `ext2/3/4` filesystems this done with the `resize2fs` command.

```bash
resize2fs <device> <size>
```

## Creating Swap Partitions

On Linux, the system can swap memory pages from RAM to disk as needed, storing them on a separate space usually implemented as a separate partition on a disk, called the swap partition or simply swap. This partition need to be of a specific type, and set-up with a proper utility (`mkswap`) before it can be used.

If you are using `parted`, the partition should be identified as a swap partition during creation, just use `linux-swap` as the filesystem type.

**Common Commands**:

| Command             | Task                  |
| ------------------- | --------------------- |
| `mkswap /dev/sdb1`  | Create swap sginature |
| `swapon /dev/sdb1`  | Enable swap           |
| `swapon --show`     | Show active swap      |
| `free -h`           | View memory/swap      |
| `swapoff /dev/sdb1` | Disable swap          |
| `swapoff -a`        | Disable all swap      |
| `cat /proc/swaps`   | Show swap devices     |