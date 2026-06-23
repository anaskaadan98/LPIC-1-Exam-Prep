---
Weight: "2"
---
# Checking Disk Usage

`du`: is recursive in nature. The command will show how much disk space files and directories are using.

**Basic Syntax**:

```bash
du [options] [file_or_directory]
```


**Most Useful Options**

| Option              | Purpose                            |
| ------------------- | ---------------------------------- |
| `-h`                | Human-readable sizes               |
| `-s`                | Summary only                       |
| `-a`                | Include files                      |
| `-c`                | Show grand total                   |
| `-d N`              | Limit depth (GNU version)          |
| `--max-depth=N`     | Limit recursion depth              |
| `-x`                | Stay on the current filesystem     |
| `--exclude=PATTERN` | Exclude matching files/directories |

**Frequently Used `du` Commands**

| Command                | Purpose                                                          |
| ---------------------- | ---------------------------------------------------------------- |
| `du`                   | Show disk usage for the current directory and its subdirectories |
| `du /path`             | Show usage for a specific directory                              |
| `du -sh /path`         | Show only the total size of a directory                          |
| `du -ah`               | Include both files and directories                               |
| `du -ch`               | Show a grand total at the end                                    |
| `du -d 1`              | Limit output to 1 directory level deep                           |
| `du --max-depth=2`     | Show usage up to 2 levels deep]                                  |
| `du -x`                | Stay on one filesystem (don't cross mounted filesystems)         |
| `du -h --exlude=*.log` | Exclude matching files                                           |
| `du -h *`              | Show sizes of items in the current directory                     |
| `du -hs *`             | Show summarized size of each item in the current directory       |
| `du -h /var/log`       | Show disk usage for `/var/log`                                   |
| `du -sh ~`             | Show total size of your home directory                           |

# Checking for Free Space

`df`: Show information about mounted filesystems, including total size, used space, available space, and usage percentage.

**Basic Syntax**

```bash
df [options] [filesystem]
```

**Most Useful Options**

| Option    | Purpose                 |
| --------- | ----------------------- |
| `-h`      | Human-readable sizes    |
| `-H`      | SI units (1000-based)   |
| `-T`      | Show filesystem type    |
| `-i`      | Show inode information  |
| `-a`      | Show all filesystems    |
| `-x TYPE` | Exclude filesystem type |
| `--total` | Show total usage        |

**Frequently Used `df` Commands**

| Option            | Purpose                                                 |
| ----------------- | ------------------------------------------------------- |
| `df`              | Show disk usage for all mounted filesystems             |
| `df -h`           | Show sizes in human-readable format (KB, MB, GB, TB)    |
| `df -H`           | Human-readable using powers of 1000 instead of 1024     |
| `df -T`           | Show filesystem type                                    |
| `df -Th`          | Show filesystem type and human-readable sizse           |
| `df /home`        | Show the filesystem containing `/home`                  |
| `df -i`           | Show inode usage instead of disk space                  |
| `df -ih`          | Show inode usage in a readable format                   |
| `df -a`           | Include pseudo, duplicate, and inaccessible filesystems |
| `df -x tmpfs`     | Exclude filesystems of type `tmpfs`                     |
| `df -x squashfs`  | Exclude `squashfs` filesystems                          |
| `df --total`      | Display a grand total line                              |
| `df -h /dev/sda1` | Show information for a specific filesystem              |

# Maintaining ext2, ext3 and ext4 Filesystetms

`fsck`: A command used to check and repair filesystems for errors.

> [!Warning]
> Run `fsck` only on unmounted filesystems whenever possible. Running it on a mounted filesystem can cause corruption.

**Most Useful Options**

| Option    | Purpose                                       |
| --------- | --------------------------------------------- |
| `-y`      | Automatically fix errors                      |
| `-n`      | Never make changes                            |
| `-f`      | Force filesystem                              |
| `-C`      | Show progress                                 |
| `-A`      | Check all filesystem in `/etc/fstab`          |
| `-R`      | Skip root filesystem (used with `-A`)         |
| `-p`      | Attempt to automatically fix any errors found |
| `-M`      | Skip mounted filesystms                       |
| `-t TYPE` | Specify filesystem type                       |

**Frequently Used `fsck` Commands**

| Command                  | Purpose                                          |
| ------------------------ | ------------------------------------------------ |
| `fsck /dev/sdb1`         | Check a filesystem and prompt before repairs     |
| `fsck -y /dev/sdb1`      | Automatically answer "yes" to all repairs        |
| `fsck -n /dev/sdb1`      | Check only; do not make changes                  |
| `fsck -f /dev/sdb1`      | Force a check even if filesystem appears clean   |
| `fsck -C /dev/sdb1`      | Show progress bar                                |
| `fsck -A`                | Check all filesystems listed in `/etc/fstab`     |
| `fsck -AR`               | Check all filesystems except the root filesystem |
| `fsck -M /dev/sdb1`      | Skip checking if filesystem is mounted           |
| `fsck -t ext4 /dev/sdb1` | Specify filesystem type                          |
| `fsck.ext4 /dev/sdb1`    | Run the ext4-specific checker directly           |
## Fine Tuning an ext Filesystem

The utility used to display or modify parameters of ext2/ext3/ext4 is called `tune2fs`.

**Basic Syntax**

```bash
sudo tune2fs [options] <device>
```

**Most Useful Options**

| Option | Purpose                        |
| ------ | ------------------------------ |
| `-l`   | List filesystem parameters     |
| `-L`   | Set label                      |
| `-m`   | Set reserved block percentage  |
| `-c`   | Set mount-count check interval |
| `-i`   | Set time-based check interval  |
| `-e`   | Define error handling behavior |
| `-U`   | Change UUID                    |
| `-j`   | Add a jounral                  |
| `-o`   | Set default mount options      |

**Frequently Used Commands**

| Command                                       | Purpose                              |
| --------------------------------------------- | ------------------------------------ |
| `tune2fs -l /dev/sda1`                        | Display filesystem information       |
| `tune2fs -L DATA /dev/sda1`                   | Set filesystem label                 |
| `tune2fs -m 1 /dev/sda1`                      | Set reserved blocks percentage       |
| `tune2fs -c 30 /dev/sda1`                     | Check filesystem every 30 mounts     |
| `tune2fs -c 0 /dev/sda1`                      | Disable mount-count checks           |
| `tune2fs -e continue /dev/sda1`               | Set behavior when errors occur       |
| `tune2fs -U random /dev/sda1`                 | Generate a new UUID                  |
| `tune2fs -j /dev/sda1`                        | Add journaling to an ext2 filesystem |
| `tune2fs -o journal_data_writeback /dev/sda1` | Set mount options                    |
# Maintaining XFS Filesystems

`xfs_repair`: is the primary tool used to check and repair XFS filesystems.

**Most Useful Options**

| Option              | Purpose                                  |
| ------------------- | ---------------------------------------- |
| `-n`                | No-modify mode (safe inspection)         |
| `-L`                | Clear the XFS log and repair             |
| `-v`                | Verbose output                           |
| `-P`                | Disable metadata prefetching             |
| `-o force_geometry` | Force geometry recovery in special cases |

**Frequently Used Commands**

| Command                                  | Purpose                                           |
| ---------------------------------------- | ------------------------------------------------- |
| `xfs_repair /dev/sdb1`                   | Check and repair an XFS filesystem                |
| `xfs_repair -n /dev/sdb1`                | Check only (no modifications)                     |
| `xfs_repair -L /dev/sdb1`                | Force log (journal) zeroing and repair            |
| `xfs_repair -v /dev/sdb1`                | Verbose output                                    |
| `xfs_repair -P /dev/sdb1`                | Disable prefetching during repair                 |
| `xfs_repair -o force_geometry /dev/sdb1` | Force geometry information when needed            |
| `xfs_repair /dev/mapper/vg_data-lv_data` | Repair an XFS filesystem on an LVM logical volume |

---