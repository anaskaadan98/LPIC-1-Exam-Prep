Some of the most useful kernel parameters are:

| Name           | Description                                                                                                      |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |
| `acpi`         | Enable/Disables [[ACPI]] support                                                                                 |
| `init`         | Sets an alternative system initiator                                                                             |
| `systemd.unit` | Sets the *systemd* target to be activated ([[Linux Run Levels]])                                                 |
| `mem`          | Sets the amount of available RAM for the system                                                                  |
| `maxcpus`      | Limits the number of processors (or processor cores) visible to the system in symmetric multi-processor machines |
| `quiet`        | Hides most boot messages                                                                                         |
| `vga`          | Selects a video mode                                                                                             |
| `root`         | Sets the root partition, distinct from the one pre-configured in the bootloader.                                 |
| `rootflags`    | Mount options for the root file system                                                                           |
| `ro`           | Makes the initial mount of the root file system read-only                                                        |
| `rw`           | Allows writing in the root file system during initial mount                                                      |
In order to make the changes of the kernel parameters persistent across reboots you need to modify the file `/etc/default/grub` in the line `GRUB_CMDLINE_LINUX`.
- A new configuration file for the bootloader must be generated every time this file changes, which is accomplished by the command:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

- Once the operating system is running, the kernel parameters used for loading the current session are available for reading in the file `/proc/cmdline`.