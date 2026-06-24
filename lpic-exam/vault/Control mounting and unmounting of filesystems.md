---
Weight: "3"
---
# Mounting and Unmounting Filesystems

**Basic Syntax**:

```bash
mount -t TYPE DEVICE MOUNTPOINT
```

`TYPE`: The type of the filesystem being mounted (e.g. ext4, btrfs, exfat, etc)
`DEVICE`: The name of the partition containing the filesystem (e.g. `/dev/sdb1`)
`MOUNTPOINT`: Where the filesystem will be mounted. The mounted-on directory need not to be empty, although it must exist. Any files in it, however, will be inaccessible by name while the filesystem is mounted.

- To unmount a filesystem, use the `umount` command.

| Option   | Purpose                                                         |
| -------- | --------------------------------------------------------------- |
| `-t`     | List mounted filesystem according to a type                     |
| `-a`     | This will mount all filesystems listed in the file `/etc/fstab` |
| `-o`     | Specify mount options                                           |
| `-r`     | Read-only mount                                                 |
| `-w`     | Read-write mount                                                |
| `--bind` | Bind mount a direrctory                                         |
| `-L`     | Mount by label                                                  |
| `-U`     | Mount by UUID                                                   |

**Frequently Used `mount` Commands**

| Command                                      | Description                            |
| -------------------------------------------- | -------------------------------------- |
| `mount`                                      | List mounted filesystem                |
| `mount /dev/sdb1 /mnt`                       | Mount a partition                      |
| `mount -t ext4 /dev/sdb1 /mnt`               | Mount and specify fielsystem type      |
| `mount -o ro /dev/sdb1 /mnt`                 | Mount read-only                        |
| `mount -o rw /dev/sdb1 /mnt`                 | Mount read-write                       |
| `mount -a`                                   | Mount all filesystem from `/etc/fstab` |
| `mount UUID=<uuid> /mnt`                     | Mount using a UUID                     |
| `mount LABEL=DATA /mnt`                      | Mount using a filesystem label         |
| `mount -o remount,rw /`                      | Remount root filesystem as read-write  |
| mount -o remount, ro /                       | Remount filesystem as read-only        |
| `mount -t iso9660 -o loop file.iso /mnt/iso` | Mount an ISO image                     |
| `mount -o loop file.img /mnt/img`            | Mount a disk image file                |

## Dealing with Open Files

When unmounting a filesystem, you may encounter an error message stating that the `target is busy`. This will happen if any files on the filesystem are open.

`lsof`: List processes accessing the filesystem and which file are open.

**Basic Syntax**

```bash
lsof <device-name>
```

# Where to Mount

Traditionally, `/mnt` was the directory under which all external devices would be mounted and a number of pre-configured "anchor points" for common devices.

`/media`: The new default mount point for any user-removable media

# Mounting Filesystems on Bootup

The file `/etc/fstab` contains descriptions about the filesystems that can be mounted. This is a text file, where each line describes a filesystem to be mounted, with six fields per line in the following order:

```bash
FILESYSTEM MOUNTPOINT TYPE OPTIONS DUMP PASS
```

| Column     | Purpose                                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| FILESYSTEM | The device containing the filesystem to be mounted                                                                        |
| MOUNTPOINT | Where the filesystem will be mounted                                                                                      |
| TYPE       | The filesystem type                                                                                                       |
| OPTIONS    | Mount options that will be passed to `mount`                                                                              |
| DUMP       | Indicator number for filesystems that should be considered for backup. Usually it is zero, meaning they should be ignored |
| PASS       | Define the order in which the filesystem will be checked on bootup                                                        |

**Mount Options**

| Option                | Purpose                                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `atime` and `noatime` | Every time a file is read the access time information is updated. Disabling this can speed up disk I/O. (Not modification time) |
| `auto` and `notauto`  | Whether the filesystem can or can't be mounted automatically with `mount -a`                                                    |
| `defaults`            | This will pass the options `rw`, `suid`,`dev`,`exec`,`auto`,`nouser` and `async` to `mount`                                     |
| `dev` and `nodev`     | Whether character or block devices in the mounted filesystem should be interpreted                                              |
| `exec` and `noexec`   | Allow or deny permission to execute binaries on the filesystem                                                                  |
| `user` and `nouser`   | Allows or not an ordinary user to mount the filesystem                                                                          |
| `group`               | Allows a user to mount the filesystem if the user belongs to the same group which owns the device containing it                 |
| `owner`               | Allows a user to mount a filesyustem if the user owns the device containing it                                                  |
| `suid` and `nosuid`   | Allow, or not, SETUID and SETGID bits to take effect                                                                            |
| `ro` and `rw`         | Mount a filesystem as read-only or writable                                                                                     |
| `remount`             | This will attempt to remount an already mounted filesystem                                                                      |
| `sync` and `async`    | Whether to do all I/O operations to the filesystem synchronously or asynchronously.                                             |

# Using UUIDs and Lables

The command `lsblk` can be used to query information about a filesystem and find out the label and UUID associated to it. 

```bash
lsblk -f <device-name>
```

# Mounting Disks with Systemd

Among many other tasks, systemd can also be used to manage the mounting (and automounting) of filesystems.

To use this feature of systemd, you need to create a configuration file called a `mount unit`. Each volume to be mounted gets its own mount unit and they need to be placed in `/etc/systemd/system`.

After that, you need to restart the `systemd` daemon with the `systemctl` command, and start the unit:

```bash
systemctl daemon-reload
systemctl start mnt-external.mount
```

You can check the status of the mounting with the command

```bash
systemctl status mnt-external.mount
```

# Automounting a Mount Unit

Mount units can be automounted whenever the mount point is accessed. To do this, you need an `.automount` file, alongside the `.mount` file describing the unit.

| Options   | Purpose                                      |
| --------- | -------------------------------------------- |
| `start`   | Only enable the unit for the current session |
| `stop`    | Deactivate one or more units                 |
| `status`  | Show runtime status of one or more units     |
| `enable`  | Enable one or more unit files                |
| `disable` | Disable one or more unit files               |
| `sleep`   | Put the system to sleep                      |

---