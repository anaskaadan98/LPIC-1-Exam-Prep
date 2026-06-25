---
Weight: "3"
---
# Introduction

Being a multi-user system, Linux needs some way to track who owns each file and whether or not a user is allowed to perform actions on a file. This is to ensure the privacy of users who might want to keep the contents of their files confidential, as well as to ensure collaboration by making certain files accessible to multiple users.

This is done through a three-level permissions system. Every file on disk is owned by a user and a user group and has three sets of permission

| Commands | Purpose                    |
| -------- | -------------------------- |
| `chmod`  | Modify the permission      |
| `chown`  | Modify the ownership       |
| `chgrp`  | Modify the group ownership |

# Querying Information about Files and Directories

The command `ls -l` is used to get a listing of the contents of any directory.

```bash
17:30:56  grey  ~/LPIC-1-Exam-Prep  ❯ ls -l 
total 16
-rw-rw-r-- 1 grey grey 1061 Jun  6 18:55 LICENSE
-rw-rw-r-- 1 grey grey 1863 Jun 14 15:56 README.md
drwxrwxr-x 3 grey grey 4096 Jun 18 18:28 lpic-exam
drwxrwxr-x 3 grey grey 4096 Jun 18 18:46 playground
```

| File Type | User  | Group | Other | User Ownership | Group Ownership | Size | Timestamp    | File Name |
| :-------: | ----- | ----- | ----- | -------------- | --------------- | ---- | ------------ | --------- |
|    `d`    | `rwx` | `rwx` | `r-x` | grey           | grey            | 4096 | Jun 18 18:46 | lpic-exam |

# Understanding Filetypes

| File Type | Meaning          | Comment                                                                                                             |
| --------- | ---------------- | ------------------------------------------------------------------------------------------------------------------- |
| `-`       | Normal file      | A file can contain data of any kind and help to manage this data. Files can be modified, moved, copied and deleted. |
| `d`       | Directory        | A directory contains other files or directories and helps to organize the file system.                              |
| `l`       | Symbolic link    | This "file" is a pointer to another file or directory elsewhere in the filesystem                                   |
| `b`       | Block device     | A virtual or physical device, usually disks or other kinds of storage devices                                       |
| `c`       | Character device | This file stands for a virtual or physical device                                                                   |
| `s`       | Socket           | Sockets serve as "conduits" passing information between two programs.                                               |
# Understanding Permissions

| Permission | Meaning                                            |
| :--------: | -------------------------------------------------- |
|    `r`     | Stands for *read* and has an octal value of 4      |
|    `w`     | Stands for *write* and has an octal value of 2     |
|    `x`     | Stands for *execute* and has an octal value of `1` |
# Modifying File Permissions

The permissions to change can be described in two different ways, or "modes".

**Symbolic Mode**

When describing which permissions to change in *symbolic mode* the first character indicate whose permissions you will alter:

| Indicator | Meaning  |
| --------- | -------- |
| `u`       | user     |
| `g`       | group    |
| `o`       | other    |
| `a`       | everyone |
- `+`: Grant you a permission
- `-`: Revoke a permission
- `=`: Set it to a specific value

If we take this:

```bash
-rw-rw-r-- 1 grey grey 1863 Jun 14 15:56 README.md
```

If we want to add execute permissions for the group we would type:

```bash
chmod g+x README.md
```

When run on a directory, `chomd` modifies only the directory's permissions. `chmod` also has a recursive mode, which is useful for when you want to change the permissions for "all files inside a directory and its subdirectories". To use this, add the parameter `-R` after the command name, before the permissions to change.

**Octal Mode**

In *octal mode*, the permissions are specified in a different way: as a three-digit value on octal notation, a base-8 numeric system.

- `r`: will take the value of 4
- `w`: will take the value of 2
- `x`: will take the value of 1

```bash
chmod 674 README.md
```

# Modifying File Ownership

**Basic Syntax**

```bash
chown USERNAME:GROUPNAME FILENAME
```

- Keep in mind that the user who owns a file does not need to belong to the group who owns a file.
- Unless you are the system administrator (root), you cannot change ownership of a file to another user or group you do not belong to. If you try to do this, you will get the error message `Operation not permitted`.

## Querying Groups

Before changing the ownership of a file, it might be useful to know which groups exist on the system, which users are members of a group and to which groups a user belongs.

| Command                 | Purpose                                                                          |
| ----------------------- | -------------------------------------------------------------------------------- |
| `getent group`          | See which groups exist on your system                                            |
| `groups`                | To know which groups a user belongs, add the username as a parameter to `groups` |
| `groupmems -g cdrom -l` | See which users belong to a group                                                |

## Default Permissions

Each file and directory has a default set of permissions and they are done by the command `umask`.

![[umask-table.png]]

For example,

```bash
-rw-rw-r-- 1 grey grey 1863 Jun 14 15:56 README.md
```

```bash
umask
0002
```

As you can see, `002` corresponds to `rw-rw-r--`, exactly as we requested. the leading zero can be ignored.

# Special Permissions

Besides the read, write and execute permission for user, group and others, each file can have three other *special permissions* which can alter the way a directory works or how a program runs. The can be specified either in symbolic or octal mode, and are as follows:

|Permission|Symbol|Numeric Value|Applies To|
|---|---|---|---|
|SUID (Set User ID)|`s`|4000|Files|
|SGID (Set Group ID)|`s`|2000|Files & Directories|
|Sticky Bit|`t`|1000|Directories (mostly)|
## SUID (Set User ID)

When a user executes a file with SUID set, the program runs with the **permissions of the file owner**, not the user running it.

This means:
- File owner = root
- Program runs with root privileges
- Normal users can update their password

## SGID (Set Group ID)

When executed, the program runs with the permissions of the file's group.

You can combine multiple special permissions on one parameter. So, to set SGID (value 2) and SUID (value 4) in octal mode for the script `test.sh` with permission `755`, you would type:

```bash
chmod 6755 test.sh
```

The output would be:
```bash
ls -lh test.sh
-rwsr-sr-x 1 carol carol 66 Jan 18 17:29 test.sh
```

---