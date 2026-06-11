---
Weight: "3"
---
## Software Packages

Software packages is a pre-compiled software with the ending format (`.deb`). It is a standardized way to distribute these packages is called a package manager, one good example for it would be: [[Debian Package Managers]].

### dpkg Commands

| Command                       | Purpose                                         |
| ----------------------------- | ----------------------------------------------- |
| `dpkg -i PACKAGENAME`         | Installing a package                            |
| `dpkg -r PACKAGENAME`         | Removing a package                              |
| `dpkg -I PACAGENAME`          | Getting information about a package             |
| `dpkg -L PACKAGENAME`         | Listing installed packages and package contents |
| `dpkg -s /PATH/TO/FILE`       | Finding out which package owns a specific file  |
| `dpkg-reconfigur PACKAGENAME` | Re-configuring installed packages               |
### apt-get/apt Commands

| Command                          | Purpose                                                                                                                 |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `apt-get update`                 | Updating the package index                                                                                              |
| `apt-get install PACKAGENAME`    | Installing a package                                                                                                    |
| `apt-get remove PACKAGENAME`     | Removing a package                                                                                                      |
| `apt-get purge PACKAGENAME`      | Removing a package and it's configuration files from the system                                                         |
| `apt-get install -f PACKAGENAME` | Try to fix the broken packages by installing the missing dependencies, ensuring that all packages are consistent again. |
| `apt-get upgrade`                | Upgrading all installed packages                                                                                        |
| `apt-get search PACKAGENAME`     | Searching for a package                                                                                                 |
### The Sources List

APT uses a list of sources to know where to get packages from. This list is stored in the file `/etc/apt/sources.list.d/ubunut.sources`

The output: 

```block
Types: deb
URIs: http://archive.ubuntu.com/ubuntu/
Suites: resolute resolute-updates resolute-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

...
...

```

