---
Weight: "4"
---
# Redirects

It is done using certain characters from the keyboard which sends the standard output of one command to the standard input of another (or to a file).

| Characters | Purpose                  |
| ---------- | ------------------------ |
| `1>`       | `stdout` -> `stdin`/file |
| `<`        | `stdin`/file <- `stdout` |
| \|         | `stdout` -> `stdin`      |
| `2>`       | `stderr` -> `stdin`/file |
| `>>`       | Append `stdout` -> file  |

- `1>`: `stdout`
- `2>`: `stderr`
- `&>`or `>&`: redirect operation

> [!Note]
> You can redirect `stdout` of a command to `stdin` of another command, but you can't redirect the `stderr` of a command to `stdin` of another. You should first redirect `stderr` towards `stdout` and then redirect that into `stdin`

Files are overwritten by output redirects unless Bash option `noclobber` is enabled.

```bash
set -o noclobber #  or -C will Enable
set +o noclobber #  or +C will Disable
```

## Extended arguments

A command on Unix and most Unix-like operating systems used to build and execute commands from standard input. It converts input from standard input into arguments to a command.

### Basic Syntax

```bash
xargs [options] [command]
```

---