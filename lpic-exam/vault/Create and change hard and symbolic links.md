---
Weight: "2"
---
There are two types of links on a Linux system:

**Symbolic links:** They point to the path of another file. If you delete the file the link will still exist, but it stops working, as it now points to nothing.

**Hard links:** Think of a hard link as a second name for the original file. They additional entry in the filesystem pointing to the same place (inode) on the disk.

> [!Tip]
> An *inode* is a data structure that stores attributes for an object on a filesystem.

## Working with hard links

**Create hard links**:
sysntax:
```bash
ln TARGET LINK_NAME
```

The `TARGET`  must exist already (this is the file the link will point to)

example:
```bash
ln target.txt /home/carol/Documents/hardlink
```

This will create a file named `hardlink` on the directory `/home/carol/Documents/`, linked to the file `target.txt` on the current directory.

**Managing Hard Links**

Hard links are entries in the filesystem which have different names but point to the same data on disk. If you change the contents of one of the names, the contents of all other names pointing to that file change since all these names point to the very same data. If you delete one of the names, the other names will still work.

You can check this by using the `-i` parameter of `ls`.

```bash
ls -li
total 28
70254594 -rw-rw-r-- 2 grey grey   13 Aug 27 17:37 file_new.txt
70254594 -rw-rw-r-- 2 grey grey   13 Aug 27 17:37 hardlink
```

**Moving and Removing Hard Links**

Since hard links are treated as regular files, they can be deleted with `rm` and renamed or moved around the filesystem with `mv`. And since a hard link pointse to the same inode of the target, it can be moved around freely, without fear of breaking the link.

## Symbolic Links

**Creating symbolic links**

The command used to create a symbolic link is also `ln`, but with the `-s` parameter added.

```bash
ln -s target.txt /home/carol/Documents/softlink
```

This will create a file named `softlink` in the directory `/home/carol/Documents/`, pointing to the file `target.txt` on the current directory.

**Managing Symbolic links**

Symbolic links point to another path in the filesystem. You can create soft links to files and directories, even on different partitions.

```bash
ls -lh
lrwxrwxrwx 1 grey grey   12 Aug 27 17:45 softlink -> file_new.txt
```

In the example above, the first character on the permissions for the file `soflink` is `l`, indicating a symbolic link.

>[!Note]
> On file and directory listing, soft links themselves always show the permissions `rwx` for the user, the group and others, but in practice the access permissions for them are the same as those for the target.


**Moving and Removing Symbolic links**

- Symbolic links can be **removed with `rm`** and **moved or renamed with `mv`**.
- Relative symbolic links can **break when moved**, because the target path is interpreted relative to the link’s location.

Example: 
```bash
ln -s original.txt softlink
``` 

works only while `softlink` remains in the same directory as `original.txt`.

- To prevent this, create the link using the target’s **absolute path**, e.g:

```bash
ln -s /home/carol/Documents/original.txt softlink
```

- An absolute-path symbolic link continues to work **regardless of where the link itself is moved**.

---