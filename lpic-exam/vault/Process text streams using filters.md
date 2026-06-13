---
Weight: "2"
---
| Command | Purpose                                                         |
| ------- | --------------------------------------------------------------- |
| `cat`   | - Print out the content of a file<br>- Write into file with `>` |
| `tac`   | Print out the content of a file from last line to first         |
| `zcat`  | Print out the content of a compressed file (`.txt.gzip`)        |
| `diff`  | Shows the difference between two text files                     |
| `echo`  | Print text to terminal or insert into file                      |
| `grep`  | Find provided pattern in a text (`-i` for case sensitivty)      |
| `wc -w` | Word count in file                                              |
| `less`  | Output file in a pager format                                   |
| `more`  | Output file in a pager format                                   |
| `head`  | Print out first 10 lines                                        |
| `tail`  | Print out last 10 lines                                         |
| `sed`   | Stream editor for filtering and transforming text               |
| `od`    | Will past the content of the file in octal format               |
| `od -x` | Will view the content of a the file in hexadecimal format       |
| `od -c` | Will view the hidden characters in a file                       |

```bash
cat file1.txt > file2.txt
```


`>`: Redirect the output and rewrite to file.
`>>`: Redirect the output and append to file.
`|`: Redirect output of command into a second command.

## Ensuring Data Integrity

1. Calculate the SHA256 checksum value of this text file and save the output into another `.txt` file.

```bash
sha256sum moc.txt > sha256.txt
```

2. Verify the file we just use the same command with the switch `-c`

```bash
sha256sum -c sha256.txt
```

output:

```block
moc.txt: OK
```

[[Regular Expression]]