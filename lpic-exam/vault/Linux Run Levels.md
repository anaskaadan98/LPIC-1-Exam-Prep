A *runlevel* can be defined as a preset single-digit integer for defining the operating state of your LINUX or UNIX-based operating system. Each runlevel designates a different system configuration and allows access to different combinations of processes.

![[boot-the-system-04.png]]

The modern way to change between *runlevels* is:

```bash
sudo systemctl set-default <runlevel>.target
reboot
```

In order to check for which *runlevel* we are currently running:

```bash
sudo systemctl get-default
```

The only runlevel definitions shared between all distributions are the runlevels 0, 1, 6.

The program responsible for managing runlevels and associated daemons/resources is `/sbin/init`.
- Each runlevel have access to certain scripts and capabilities to the system, and these scripts are usually stored under the directory `/etc/init.d/*`.
The requested runlevel is defined by a kernel parameter or in the `/etc/inittab` file
- The syntax of the `/etc/inittab` file uses this format:
```
id:runlevels:action:process
```

The available actions are:

| Action     | Description                                                                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| boot       | The process will be executed during system initialization. The field `runlevels` is ignored.                                                       |
| bootwait   | The process will be executed during system initialization and `init` will wait until it finishes to continue. The field `runlevels` is ignored.    |
| sysinit    | The process will be executed after system initialization, regardless of runlevel. The field `runlevels` is ignored                                 |
| wait       | The process will be executed for the given runlevels and `init` will wait until it finshes to continue                                             |
| respawn    | The process will be restarted if it is terminated                                                                                                  |
| ctrlaltdel | The process will be executed when the init process receives the `SIGINT` signal, triggered when the key sequence of `Ctrl + Alt + Del` is pressed. |
The default runlevel is also defined in `/etc/inittab`.

After each time you modify the `/etc/inittab` file you should run the command:

```bash
telinit q
```

The scripts used by `init` to setup each runlevel are stored in the directory `/etc/init.d`. 

![[init.d-output.png]]

The files are separated into multiple directories, each one are for those runlevels. These files are just symbolic links to the actual scripts in `/etc/init.d`.
A links filename starting with letter `K` determines that the service will be killed when entering the runlevel (kill). Starting with letter `S`, the service will be started when entering the runlevel (start).

![[rc-output.png]]



---