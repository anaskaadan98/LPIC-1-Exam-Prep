---
Weight: "4"
---
## Getting System Information

| Command    | Purpose                                    |
| ---------- | ------------------------------------------ |
| `pwd`      | Print out Present Working Directory        |
| `touch`    | Create an empty file                       |
| `ls`       | Lists the content of the working directory |
| `uname -a` | Kernel and system information              |


>[!Note]
> Hidden files start with a `.` in Linux.


## Getting Command Information

| Command   | Purpose                                        |
| --------- | ---------------------------------------------- |
| `man`     | Open the manual page for any command           |
| `apropos` | Search for relative commands                   |
| `type`    | Basic information about a command              |
| `which`   | Show the exact location of the commands binary |

> [!Note]
> Each command has options that will help us manipulate and/or extend the capabilities of the command. We can learn more about a command by accessing the manual page for it.

> [!Warning]
> The information "hashed", signifies that the command was recently used by the user and, in order to increase system efficiency, it was added to a hash table to make it more accessible the next time you run it.

## Special Directories

When we use the option `-a` with the command `ls` we notice two directories. The `.` and the `..`

`.`: The current working directory.
`..`: The previous directory.

These two special directories are useful with navigation commands.

## Using Your Command History

| Command      | Purpose                                                                                              |
| ------------ | ---------------------------------------------------------------------------------------------------- |
| `history`    | Will return the most recent commands you have executed with the most recent of those appearing last. |
| `history -c` | Clear the history list                                                                               |
- If you want to call up a command again, the up and down arrow keys can be used to easily search through the last commands called up and execute them again by pressing the \[Enter] key.
- \[Ctrl]+\[r] (reverse-i-search) is very suitable to re-execute a longer command quickly and efficiently. After you search for the command press right arrow to paste it then run the command with \[Enter].

### Bash History Environment Variables

| Variable       | Purpose                                                                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `HISTCONTROL`  | `ignorespace:` ignore commands that start with a space<br>`ignoredups:` ignore duplicate commands<br>`ignoreboth:` both of the above |
| `HISTSIZE`     | The number of history commands that will be stored in memory                                                                         |
| `HISTFILESIZE` | The number of history commands that will be stored on disk (`~/.bash_history`)                                                       |

### When To Save History

By default `~/.bash_history` will only be updated when you close the BASH session. Use the `PROMPT_COMMAND` environment variable to update history file between multiple working sessions.

```bash
export PROMPT_COMMAND='history -a'
```

### Persisting History Configuration

Once you've got your history working just right you should store the configuration in your `~/.bashrc` file.

## Environment Variables

| Command  | Purpose                                            |
| -------- | -------------------------------------------------- |
| `echo`   | Print the value of the variable                    |
| `unset`  | Delete an environment variable                     |
| `set`    | Print the environment variable and the functions   |
| `env`    | Print the environment variables                    |
| `export` | Used to update a value for an environment variable |

### Finding Your Environment Variables

We use the `env` command to identify the current values for each of our environment variables.

- `echo` command will print the value of the environment variable if it was preceded with the `$` sign.

```bash
echo $PATH
```

### Creating New Environment Variables

You can add your own custom variables to your environment by using the `=` character.
- If you want them to be persistent, you should add them to the `.bashrc` file.

### Deleting Environment Variables

You could either close the terminal session, reboot or use the command `unset`.
- If you added them to the `.bashrc` file, you are going to have to re-modify the file.

### Quoting to Escape Special Characters

You can do this by wrapping the text inside quotes `"text text text"` or by using the backslash `text\ text\ text`.



---