---
Weight: "4"
---
## File and Folder Manipulation

| Command | Purpose                                            |
| ------- | -------------------------------------------------- |
| `cp`    | Copy file/folder from source to destination        |
| `mv`    | Move/Rename file/folder from source to destination |
| `rm`    | Remove file/folder                                 |
| `mkdir` | Create a new folder                                |
| `rmdir` | Remove a folder recursivly                         |
| `find`  | Search command for files in a directory hierarchy  |
- Use the `-r` with `cp` and `rm` commands for recursive operations on folders.

## File Globbing and Wildcards

| Character | Puspose                                                                                               |
| --------- | ----------------------------------------------------------------------------------------------------- |
| `*`       | An occurrence of any characters                                                                       |
| `?`       | An occurrence of one character                                                                        |
| `[]`      | An occurrence of any character specified by the character enclosed in brackets (we could use a range) |

## How to find files

```bash
find STARTING_PATH OPTIONS EXPRESSION
```

- STARTING_PATH: defines the directory were the search begins
- OPTIONS: Controls the behavior and adds specific criteria to optimize the search process
- EXPRESSION: Defines the search query

## Using criteria to Speed Search

| Criteria      | Purpose                                                                |
| ------------- | ---------------------------------------------------------------------- |
| `-type`       | Switches to finding files based on type                                |
| `-name`       | performs a search based on the given name                              |
| `-iname`      | Like the one before but the case is not sensitive                      |
| `-not`        | Returns those results that do *not* match the test case                |
| `-maxdepth N` | Searches the current directory as well as subdirectories N levels deep |
| `-mtime`      | Locating files by modification time                                    |
| `-size`       | Locating file by size                                                  |
| `-exec`       | Acting on the result set                                               |


```bash
find . -name "*.conf" -exec chomd 644 `{}` \;
```

## Archiving Files

The **tar** command (Archiving and Compression):
- Create tar archives
- Extract tar archives
- Display a list of the files included in the archive
- Add additional files to an existing archive

```bash
tar [OPERATION_AND_OPTONS] [OUTPUT_ARCHIVE] [SOURCE_FILES]
```

| Operations and Options                  | Purpose                                                      |
| --------------------------------------- | ------------------------------------------------------------ |
| `--create (-c)`                         | Create a new tar archive                                     |
| `--extract (-x)`                        | Extract the entire archive or one more files from an archive |
| `--list (-t)`                           | Display a list of the files included in the archive          |
| `--verbose (-v)`                        | Show the files being processed by the `tar` command          |
| `--file=archive-name (-f archive-name)` | Specifies the archive file name                              |

Compressing with `tar`:
- `-czvf`: will create `.tar.gz` (gzip)
- `-cjvf`: will create `.tar.bz` (bzip2)

## The cpio Command

`cpio` stands for "copy in, copy out":
- Copying files to an archive.
- Extracting files from an archive


## The dd Command

It copies data from one location to another.

```bash
dd if=oldfile of=newfile
```


---