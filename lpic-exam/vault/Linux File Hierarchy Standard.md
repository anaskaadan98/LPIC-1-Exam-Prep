`FHS` It is the official guideline that dictates the layout, naming conventions, and directory structure of the file system in Linux and other Unix-like operating systems.

![[Linux-file-system-hierarchy-Linux-file-structure-optimized.jpg]]

| Directory | Name             | Description                                                 |
| --------- | ---------------- | ----------------------------------------------------------- |
| `/`       | root             | The first mounting point on a physical hard drive.          |
| `/bin`    | Command binaries | The executable files for any commands.                      |
| `/boot`   | Boot loader      | The files of the bootloader that loades the BIOS and the OS |
| `/dev`    | Devices          | Files related to any connected external devices             |
| `/etc`    | Config files     | Contains configuration files (settings)                     |
| `/home`   | Home directory   | Users home directories                                      |
| `/lib`    | Library          | Library files for executables                               |
| `/proc`   | Process          | Virtual file system                                         |
| `/root`   | root home        | The home directory of the root user                         |
| `/sbin`   | System binaries  | The executable files for system based commands              |
| `/tmp`    | Temproary        | Temporary file storage for running applications             |
| `/usr`    | User             | User binaries (executable or script), often r/o             |
| `/var`    | Variable         | Storage of variable files, logs and mails                   |
| `/media`  | Media            | Mount place for removable (USB) media                       |
| `/mnt`    | Mount            | Legacy location for mounting removable media                |
| `/run`    | Run              | Information about the running system since last boot        |
