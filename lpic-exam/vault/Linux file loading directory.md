Usually when you want to modify some settings you search for a file with the extension `<module_name>.conf`.

For example: `/etc/modprobe.conf` contains settings related to modules, but if you would like to keep this file intact and keep your changes separated in a separate file you can add it to `/etc/modprobe.d/file.conf`.

Because the system contains a loop that searches for other `.conf` files to include and they are all stored inside a directory named `/etc/<module_name>.d/*`