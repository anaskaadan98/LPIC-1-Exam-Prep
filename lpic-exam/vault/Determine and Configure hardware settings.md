---
Weight: "2"
---
[[Hardware Abstraction Layer|HAL]]: Hardware Abstraction Layer
[[dbus]]: Communication between the hardware and the software
[[BIOS]]: Basic Input/Output System

Commands for hardware Inspection:

The essential commands to identify connected devices in a Linux system are:

| Name    | Description                                                    |
| ------- | -------------------------------------------------------------- |
| `lspci` | Shows all devices currently connected to the PCI bus.          |
| `lsusb` | Lists USB devices currently connected to the machine.          |
| `lsmod` | List each LKM (Loadable Kernel Module) that is already loaded. |
[[OS architecture]]
[[Device ID - UUID]]

> [!Note]
> **LKM:** Loadable Kernel Module

The output command `lsmod` is divided into three columns:

- **Module**: Module name.
- **Size**: The module is stored on the *Hard drive* but it will be loaded to the *RAM* using `modprobe` or `insmod` commands and the number indicates the size of the module in *RAM* not the size of occupation on the *Hard Drive* (When it is stored in the *Hard Drive* it will be compressed but when we load it to the *RAM* it will decompress and that is the actual size of the module).
- **Used by**: Depending modules (Some modules require other modules to work properly).

Commands for manipulating modules:

| Name       | Description                                    |
| ---------- | ---------------------------------------------- |
| `modprobe` | Add or remove modules from the Linux kernel.   |
| `modinfo`  | Shows information about a Linux Kernel module. |
These commands will change the status of the module while running the OS, but if you would like to keep your changes persistent you can change them from the `/etc/modprobe.conf` or use [[Linux file loading directory]] method.

The information of these 3 commands are kept in special files in the directories `/proc` and `/sys`.
- These directories are mount points on RAM used by the kernel to store runtime configuration and information of running processes.
- [[proc directory]]
- [[sys directory]]


[[Linux distributions]]
[[Linux commands]]
[[Linux File Hierarchy Standard]]




---

> [!Note]
> To copy from terminal use `Ctrl + Shift + c`
> To paste to terminal use `Ctrl + Shift + v`
> To clear the terminal use `Ctrl + l`
> In order to write and save in nano editor program use `Ctrl + o` then `Enter` then `Ctrl + x`


