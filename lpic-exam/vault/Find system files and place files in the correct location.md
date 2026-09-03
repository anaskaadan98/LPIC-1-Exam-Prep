---
Weight: "2"
---
![[Linux File Hierarchy Standard]]

## Temporary Files

Temporary files are files used by programs to store data that are only needed for a short time. This can be the data of running processes, crash logs, scratch files from an autosave, intermediary files used  during a file conversion, cache file and such.

**Location of Temporary Files**:

**/tmp**: The recommendation is that this directory be cleared (all files erased) during system boot-up, although this is not mandatory.

**/var/tmp**: This should not be cleared during the system boot-up. Files stored here will usually persist between reboots.

**/run**: This directory contains run-time variable data used by running processes. This location must be cleared during system boot-up. 


> [!Note]
>  There is nothing which prevents a program from creating temporary files elsewhere on the system, but it is good practice to respect the conventions set by the FHS.

## Finding files
To search for files on a Linux system, you can use the `find` command. This is a very powerful tool, full of parameters that can suit its behaviour and modify output exaclty to your needs.

example:

```bash
find . -name '*.txt'
./moc.txt
./001.txt
./file_new.txt
./.secret.txt
```

> [!Note]
>  Keep in mind that  the `-name` parameter is case sensitive. If you wish to do a case insensitive search, use `-iname`.

**Common commands for `find`**

|Command|What it does|
|---|---|
|`find . -name "file.txt"`|Find a file by exact name|
|`find . -iname "file.txt"`|Find by name, case-insensitive|
|`find . -type f`|Find all regular files|
|`find . -type d`|Find all directories|
|`find . -type l`|Find symbolic links|
|`find . -name "*.log"`|Find all `.log` files|
|`find . -path "*backup*"`|Find paths containing `backup`|
|`find . -size +100M`|Find files larger than 100 MB|
|`find . -size -10M`|Find files smaller than 10 MB|
|`find . -empty`|Find empty files/directories|
|`find . -user john`|Find files owned by user `john`|
|`find . -group developers`|Find files owned by group `developers`|
|`find . -perm 755`|Find files with exactly permission `755`|
|`find . -mtime -7`|Modified within the last 7 days|
|`find . -mtime +30`|Modified more than 30 days ago|
|`find . -maxdepth 1 -type f`|Search only the current directory|
|`find . -mindepth 2 -type f`|Don't search at the starting directory level|
## Using `locate` and `updatedb`

`locate` and `updatedb` are commands that can be used to quickly find a file matching a given pattern on a Linux system. But unlike `find`, `locate` will not search the filesystem for the pattern, instead, it looks it up on a database built by running the `updatedb` command. This gives you very quick results, but they may be impercise depending on when the database was last updated.

**Common commands for `locate`**:

| Command                 | Purpose                            |
| ----------------------- | ---------------------------------- |
| `locate filename`       | Search for a filename              |
| `locate -i filename`    | Case-insensitive search            |
| `locate "*.log"`        | Find files matching a pattern      |
| `locate -n 10 filename` | Show only 10 results               |
| `locate -r "pattern"`   | Search using a regular expression  |
| `locate -c filename`    | Count matching results             |
| `locate -b "\filename"` | Match only the basename            |
| `locate -e filename`    | Show only currently existing files |
**Controlling the Behavior of `updatedb`**

The behavior of `updatedb` can be controlled by the file `/etc/updatedb.conf`. This is a text file where each line controls one variable.

|Variable|Excludes based on...|
|---|---|
|`PRUNEFS`|Filesystem **type**|
|`PRUNENAMES`|Directory **name**|
|`PRUNEPATHS`|Full **path**|
|`PRUNE_BIND_MOUNTS`|**Bind mounts**|
## Finding Binaries, Manual Pages and Source Code

`which` is a very useful command that shows the full path to an executable. 

Example:
```bash
which bash
/usr/bin/bash
```

If the `-a` option is added the command will show all pathnames that match the executable.

Example:
```bash
which -a bash
/usr/bin/bash
/bin/bash
```

`type` is  a similar command which will show information about a binary, including where it is located and its type. 

Example:
```bash
type bash
bash is /usr/bin/bash
```

If the `-a` option is added the command will show all pathnames that match the executable.

Example:
```bash
type -a bash
bash is /usr/bin/bash
bash is /bin/bash
```

And the `-t` parameter will show the file type of the command which can be `alias`, `keyword`, `function`, `builtin` or `file`. 

```bash
type -t bash
file

type -t ll
alias

type -t type
type is a built-in shell command
```

The command `whereis` is more versatile and besides binaries can also be used to show the location of man pages or even source code for a program (if available in your system).

Example:
```bash
whereis bash
bash: /usr/bin/bash /usr/share/man/man1/bash.1.gz
```

You can quickly filter the results using commandline switches like `-b`, which will limit them to only the binaries, `-m`, which will limit them to only man pages, or `-s`, which will limit them to only the source code.

Example:
```bash
whereis -b bash
bash: /usr/bin/bash

whereis -m bash
bash: /usr/share/man/man1/bash.1.gz
```

---