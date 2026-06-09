---
Weight: "3"
---
**SysV Standard**: A service manager based on the *SysVinit* standard controls which daemons and resources will be available by employing the concept of [[Linux Run Levels]].

**systemd:** A modern system and services manager that has a concurrent structure, employs sockets and D-Bus for service activation, on-demand daemon execution, process monitoring, snapshot support, system session recovery, mount point control and a dependency-based service control.

There are seven distinct types of systemd units:

| Unit typs | Description                                                                                                                                                                                                    |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| service   | The most common unit type, for active system resources that can be initiated, interrupted and reloaded.                                                                                                        |
| socket    | The socket unit type can be a filesystem socket or a network socket. All socket units have a corresponding service unit, loaded when the socket receives a request.                                            |
| device    | A device unit is associated with a hardware device identified by the kernel.                                                                                                                                   |
| mount     | A mount point definition in the filesystem, similar to an entry in `/etc/fstab`.                                                                                                                               |
| automount | An automount unit is also a mount point definition in the filesystem, but mounted automatically. Every automount unit has a corresponding mount unit, which is initiated when the automount point is accessed. |
| target    | A target unit is a grouping of other units, managed as a single unit.                                                                                                                                          |
| snapshot  | A snapshot unit is a saved state of the systemd manager (not available on every Linux distribution).                                                                                                           |
The main command for controlling systemd units is `systemctl`, which is used to execute all tasks regarding unit activation, deactivation, execution, interruption, monitoring, etc.

- The configuration files associated with every unit can be found in the `/lib/systemd/system/` directory.
- The command `systemctl list-unit-files` lists all available units and shows if they are enabled to start when the system boots.
- The option `--type` will select only the units for a given type, as in:
	- `systemctl list-unit-files --type=service`
	- `systemctl list-unit-files --type=target`

**acpid**: The acpid daemon is the main power manager for Linux and allows finer adjustments to the actions following power related events, like closing the laptop lid, low battery or battery charging levels.

**Upstart**: Is a discontinued event-based replacement for the traditional `init` daemon. The initialization scripts used by Upstart are located in the directory `/etc/init/`.

## Shutdown and Restart

The `shutdown` command adds extra functions to the `power off` process, it automatically notifies all logged-in users with a warning message in their shell sessions and new logins are prevented.

After `shutdown` is executed, all processes receive the *SIGTERM*  signal, followed by the *SIGKILL* signal, the n the system shuts down or changes its runlevel.

To change the default options for `shutdown`, the command should be executed with the following syntax:

```bash
shutdown [option] time [message]
```

- The `time` parameter defines when the requested action will be executed, accepting the following formats:

**hh:mm**: This format specifies the execution time as hour and minutes.
**+m**: This format specifies how many minutes to wait before execution.
**now** or **+0**: This format determines immediate execution.

- The `message` parameter is the warning text sent to all terminal sessions of logged-in users.
- We can limit users that will be able to restart the machine by sending the signal `Ctrl + Alt + Del` and this is possible by placing option `-a` for the `shutdown` command present at the line regarding `ctrlaltdel` in the `/etc/inittab` file. By doing this, only users whose usernames are in the `/etc/shutdown.allow` file will be able to restart the system with the `Ctrl + Alt + Del` keystroke combination.
- The `systemctl` command can also be used to turn off or to restart the machine (`systemd reboot` or `systemd poweroff`).
 
> [!NOTE] 
> The command `wall` is able to send a message to terminal sessions of all logged-in users.


---