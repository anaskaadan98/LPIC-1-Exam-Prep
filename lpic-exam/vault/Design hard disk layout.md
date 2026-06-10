---
Weight: "2"
---
**Mount Points**: Before a filesystem can be accessed on Linux it need to be mounted. So, when you mount a filesystem, you're making it accessible & merging it with the existing filesystem. The mount point acts as the location where this merge occurs.

The mount point must exist before mounting the filesystem. In case if you mounted the filesystem on an already existing one with some files in it, these files will not be accessible until you unmount the filesystem.

## As good practice

<u>Basic Desktop</u>:

| Partition Name | Size      |
| :------------: | --------- |
|      `/`       | Biggest   |
|    `/boot`     | 100 MB+   |
|    `/swap`     | 1-2 x RAM |

<u>Network Workstation</u>:

| Partition Name | Size      |
| :------------: | --------- |
|      `/`       |           |
|    `/boot`     | 100 MB+   |
|    `/home`     |           |
|    `/swap`     | 1-2 x RAM |

<u>Server Setup</u>:

| Partition Name | Size      |
| :------------: | --------- |
|      `/`       |           |
|    `/boot`     | 100 MB+   |
|    `/home`     |           |
|     `/var`     |           |
|     `/usr`     | read only |
|    `/swap`     | 1-2 x RAM |

- In order to make sure your system will still be able to boot in case of a crash on the *root* filesystem or if you wish to use a filesystem which the *bootloader* cannot understand in the *root* partition, or if it uses an unsupported encryptoiin or compression method, you need to separate the *bootloader-related* files on a `/boot` partition.
- Keeping user's personal directories under `/home` on a separate partition makes it easier to reinstall the system without the risk of accidentally touching user data.
- Keeping data related to a web or database server under `/var` on a separate partition (or even separate disk) makes system administration easier to manage.
	- A missbehaved process may write data until there is no free space left on the filesystem.
	- If `/var` is under `/` this may trigger a kernel panic and filesystem corruption, causing a situation that is difficult to recover from. But if `/var` is kept under a separate partition, the root filesystem will be unaffected.
- For performance reasons, You may want to keep the *root* filesystem `/` on a speedy SSD unit, and bigger directories like `/home` and `/var` on slower hard disks which offer much more space for a fraction of the cost.


## The EFI System Partition (ESP)

Used by machines based on *UEFI* to store bootloaders and kernel images for the operating systems installed.
- The partition is formatted in a FAT-based filesystem. 
- On a **Microsoft Windows** machine this will be the first one on the disk
- On a **Linux System** it will be mounted under `/boot/efi`.

## The `swap` partition

The `swap` partition is used to swap memory pages from RAM to disk as needed. This partition need to be of a specific type, and set-up with a proper utility called `mkswap` before it can be used.

The `swap` partition cannot be mounted like the others, meaning that you cannot access it like a normal directory and peek at its contents.

Linux also supports the use of `swap files` instead of partitions, which can be useful to quickly increase swap space when needed.

## Logical Volume Management (LVM)

A form of storage virtualization that offers system administrators a more flexible approach to managing disk space than traditional partitioning.

Physical Volume (PV) are grouped into Volume Groups (VG) which abstract the underlying devices and are seen as a single logical device, with the combined storage capacity of the component PVs

---