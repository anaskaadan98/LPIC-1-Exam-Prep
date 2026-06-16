---
Weight: "4"
---
# Job Control

*Jobs* are processes that have been started interactively through a terminal, sent to the background and have not yet finished execution.

You can find out about the active jobs by running the command:

```bash
jobs
```

`Ctrl + z`: Suspend a command from running
`Ctrl + c`: Cancel a command from running

| Options | Purpose                                                                  |
| ------- | ------------------------------------------------------------------------ |
| `-l`    | Will additionally display the process ID (PID)                           |
| `-n`    | List only processes that have changed status since the last notification |
| `-p`    | Lists process IDs                                                        |
| `-r`    | List only running jobs                                                   |
| `-s`    | List only stopped (or suspended) jobs                                    |
`&`: Start a process directly in the background.

- Once the process is in the background we can either `kill` or bring it to the foreground with the command `fg`.

## Detached Jobs: nohup

It is possible to detach jobs from sessions and have them run even after the session is closed. This is achieved with the `nohup` ("no hangup") command:

```bash
nohup COMMAND &
```

## Process Monitoring

| Command  | Purpose                                                                |
| -------- | ---------------------------------------------------------------------- |
| `watch`  | Allows to monitor a programs's output change over time every 2 seconds |
| `top`    | Dynamic output of process monitoring                                   |
| `ps aux` | Static output of process monitoring                                    |


## Sending Signals to Processes: kill

- Every single process has a unique process identifier or PID.
- `SIGTERM` signals are a range of numbers `0 - 15` were as `0` is the strongest Termination Signal that could be sent to a process.

| Command | Purpose                                             |
| ------- | --------------------------------------------------- |
| `pgrep` | To find out the PID of a process by using it's name |
| `pidof` | To find out the PID of a process by using it's name |
| `pkill` | Kills a process based on it's name                  |
Signals can be specified either by (Name, Number or Option)

> [!Tip]
> We can use command substitution to save some time
> ```bash
> kill -1 $(pgrep sleep)
> ```


# Features of Terminal Multiplexers

Terminal multiplexers such as **screen** and **tmux** allow users to manage multiple terminal sessions within a single terminal interface. Their key features include:
- Creating **sessions** that contain one or more **windows**, where programs run.
- Splitting windows into multiple **panes** for working with several programs at the same time.
- Using a **command prefix/key combination** for easy control and navigation.
- **Detaching sessions** so programs continue running in the background even if the terminal closes, freezes, or a remote connection is lost.
- Supporting **socket connections** and **copy mode**.
- Being **highly customizable** to suit different workflows.

## Screen

GNU Screen is invoked just by typing `screen` into the terminal.

While working with windows it is important to remember the following:
- Windows run their programs completely independent of each other.
- Programs will continue to run even if their window is not visible (also when the screen is detached)

To remove a window, simply terminate the program running in it. Once the last window is removed, `screen` will itself terminate. Alternatively, use `prefix + k` while in the window you want to remove.

`screen` can divide a terminal screen up into multiple regions in which to accommodate windows. These division can be either horizontal or vertical.


### Screen Commands

| Commands       | Purpose                                      |
| -------------- | -------------------------------------------- |
| `Ctrl+a`       | Screen command prefix                        |
| `prefix + w`   | See all windows at the bottom                |
| `prefix + c`   | Create a new window                          |
| `prefix + A`   | Rename the window's title                    |
| `prefix + n`   | Go to next window                            |
| `prefix + p`   | Go to previous window                        |
| `prefix + #`   | Go to window number `#`                      |
| `prefix + "`   | See a list of all windows                    |
| `prefix + S`   | Split window horizontally                    |
| `prefix + `\|  | Split window vertically                      |
| `prefix + Tab` | Move between regions                         |
| `prefix + Q`   | Terminate all regions except the current one |
| `prefix + X`   | Terminate current region                     |
| `prefix + d`   | Detach a session                             |
| `prefix + [`   | Enter copy/scrollback mode                   |
| `prefix + j`   | Paste text on window                         |
| `prefix + l`   | Changes the window kill                      |
| `prefix + ?`   | View all bindings                            |

### Screen Options

| Options                         | Purpose                                                                 |
| ------------------------------- | ----------------------------------------------------------------------- |
| `screen -t NAME`                | Create a new screen with a predefined name                              |
| `screen -ls`                    | List of all sessions                                                    |
| `screen -S`                     | Create a new session with a descriptive name                            |
| `screen -S SESSION-PID -X quit` | To kill a session, quit out of all its windows or just type the command |
| `screen -r SESSION-NAME`        | Reattach session into terminal                                          |

### Session Detachment

For a number of reasons you may want to detach a screen session from its terminal:
- To let your computer at work do its business and connect remotely later from home.
- To share a session with other users.

**Important options for session reattaching:**
- Reattach a session and - if necessary - detach it first
- Create a session first if does not exist
- Use the first session if more than one is available
- Reattach a session - if necessary - detach and logout remotely first
- If a session is running, the reattach, if it was not running create it and notify the user
- Start `screen` in *detached mode* This is useful for system startup scripts
- Same as above but does not fork a new process 

### Copy & Paste: Scrollback Mode

1. Enter copy/scrollback mode
2. Move to the beginning of the piece of text you want to copy using the arrow keys
3. Mark the beginning of the piece of text you want to copy: Space
4. Move to the end of the piece of text you want to t copy using the arrow keys.
5. Mark the end of the piece of text you want to copy: Space
6. Go to the window of your choice and paste the piece of text

### Customization of Screen

The system-wide configuration file for screen is `/etc/screenrc`. Alternatively, a user-level `~/.screenrc` can be used.

| Configuration      | Purpose                                                | Key Information     |
| ------------------ | ------------------------------------------------------ | ------------------- |
| SCREEN SETTINGS    | Define general Screen configuration options            | `defscrllback 1024` |
| SCREEN KEYBINDINGS | Customize keyboard shortcuts and commands              | `bind l kill`       |
| COMMAND PREFIX     | Modify the default command prefix key                  | `escape ^Bb`        |
| TERMINAL SETTINGS  | Configure terminal behavior, window sizes, and buffers | `defnonblock 5`     |
| STARTUP SCREENS    | Automatically launch programs when Screen starts       | `screen -t top top` |

## tmux

`tmux` is a terminal multiplexer; it allow you to create several "pseudo terminals" from a single terminal.

### tmux features
- Client-server model.
- Interactive selection of sessions, windows and clients via menus
- The same window can be linked to a number of sessions
- Availability of both *vim* and *Emacs* key layouts
- `UTF-8` and `256-colour` terminal support

### tmux commands

>[!Warning]
> `tmux` takes in the same commands as `screen` but the only difference is the default `prefix` (`Ctrl+b`) and splitting commands.


![[#Screen#Screen Commands]]

commands available only in `tmux`

| Command                       | Purpose                    |
| ----------------------------- | -------------------------- |
| `prefix + z`                  | Zoom/unzoom pane           |
| `prefix + Ctrl + Arrow`       | Interactive pane resizing  |
| `prefix + $`                  | Rename session             |
| `prefix + q`                  | Display pane numbers       |
| `prefix + q` then pane number | Switch to pane by number   |
| `prefix + f`                  | Find window by name        |
| `prefix + .`                  | Change window index number |
| `prefix + "`                  | Split window horizontally  |
| `prefix + %`                  | Split window vertically    |

The window-splitting facility of `screen` is also  present in `tmux`. The resulting divisions are not called *regions* but *panes*. The most important difference between regions and panes is that the latter are complete pseudo-terminals linked to a window. This means that killing a pane will also kill its pseudo-terminal and any associated programs running within.

### Copy & Paste: Scrollback Mode

`tmux` also features copy mode in basically the same fashion as `screen`. The only difference command-wise is that you use `Ctrl + Space` to mark the beginning of the selection and `Alt + w` to copy the selected text.


### Customization of tmux

The configuration files for `tmux` are typically located `/etc/tmux.conf` and `~/.tmux.conf`


---