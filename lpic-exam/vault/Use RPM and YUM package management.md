---
Weight: "3"
---
## The RPM Package Manager (rpm)

The essential tool for managing software packages on Red Hat based (or derived) system.


| Command                 | Purpose                                                |
| ----------------------- | ------------------------------------------------------ |
| `rpm -i PACKAGENAME`    | Installing a package                                   |
| `rpm -U PACKAGENAME`    | Upgrading a package                                    |
| `rpm -ivh PACKAGENAME`  | This will install in verbose mode with a progress bar  |
| `rpm -e PACKAGENAME`    | Removing a package                                     |
| `rpm -qa`               | List of all installed packages                         |
| `rpm -qi PACKAGENAME`   | To get information about an *installed* package        |
| `rpm -qip PACKAGENAME`  | To get information about a **Not** *installed* package |
| `rpm -ql PACKAGENAME`   | List the content of an installed package               |
| `rpm -qf /PATH/TO/FILE` | Finding out which package owns a specific file         |
Using `rpm` we can't solve dependencies just like `dpkg`, you will have to solve them manually. 

## YellowDog Updater Modified (YUM)

It is similar to the `apt` utility on Debian-based systems, being able to search for, install, update remove packages and automatically handle dependencies. `yum` can be used to install a single package, or to upgrade a whole system at once.

| Command                             | Purpose                                        |
| ----------------------------------- | ---------------------------------------------- |
| `yum search PACKAGENAME`            | Search for a package                           |
| `yum install PACKAGENAME`           | Install a package                              |
| `yum update PACKAGENAME`            | Update a package                               |
| `yum whatprovides /PATH/TO/FILE`    | Finding which package provides a specific file |
| `yum info PACKAGENAME`              | Getting information about a package            |
| `yum-config-manager --add-repo URL` | To add a repository to a `.repo` file          |
| `yum repolist --all`                | List all of available repositories             |

## Managing Software Repositories 

For `yum` the "repos" are listed in the directory `/etc/yum.repos.d/`. Each repository is represented by a `.repo` file.

Extra repositories can be added by the user by adding a `.repo` file in the directory mentioned above, or at the end of `/etc/yum.conf`

## DNF

The package management too used on Fedora, and is a fork of `yum`

| Command                             | Purpose                                                |
| ----------------------------------- | ------------------------------------------------------ |
| `dnf search PATTERN`                | Searching for a package                                |
| `dnf info PACKAGENAME`              | Getting an information about a package                 |
| `dnf install PACKAGENAME`           | Install a package                                      |
| `dnf clean all`                     | Auto remove all un-used dependencies                   |
| `dnf remove PACKAGENAME`            | Remove a package                                       |
| `dnf update PACKAGENAME`            | Update a package                                       |
| `dnf upgrade PACKAGENAME`           | Upgrading a package                                    |
| `dnf provides /PATH/TO/FILE`        | Finding which package provides a specific file         |
| `dnf list --installed`              | Getting a list of all packages installed in the system |
| `dnf repoquery -l PACKAGENAME`      | List the content of an installed package               |
| `dnf repolist`                      | List all available repositories                        |
| `dnf-config-manager --add-repo URL` | To add a repository to a `.repo` file                  |

## Managing Software Repositories

Just as with `yum` and `zypper`, `dnf` works with software repositories. Each distribution has a list of default repositories, and administrators can add or remove repos as needed.

For `dnf` the "repos" are listed in the directory `/etc/yum.repos.d/`. Each repository is represented by a `.repo` file.

Extra repositories can be added by the user by adding a `.repo` file in the directory mentioned above, or at the end of `/etc/yum.conf`

## Zypper

The package management tool used on SUSE Linux and OpenSUSE. It is similar to `apt` and `yum`, being able to install, update and remove packages from a system, with automated dependency resolution.

| Command                            | Purpose                                                          |
| ---------------------------------- | ---------------------------------------------------------------- |
| `zypper refresh`                   | Updating the package index                                       |
| `zypper se PACKAGENAME`            | Searching for a package                                          |
| `zypper se -i PACKAGENAME`         | To check if a specific package is installed                      |
| `zypper in PACKAGENAME`            | Install a software package                                       |
| `zypper rm PACKAGENAME`            | Remove a software package                                        |
| `zypper se provides /PATH/TO/FILE` | Finding which package provides a specific file                   |
| `zypper info PACKAGENAME`          | Getting an information about a package                           |
| `zypper repos`                     | List of all the repositories currently registered in your system |
| `zypper addrepo`                   | To add a new software repository for `zypper`                    |
| `zypper removerepo`                | To remove a repository                                           |
## Managing Software Repositories

Just as with `yum` and `zypper`, `dnf` works with software repositories. Each distribution has a list of default repositories, and administrators can add or remove repos as needed.

For `dnf` the "repos" are listed in the directory `/etc/zypp/repos.d/`. Each repository is represented by a `.repo` file.

Extra repositories can be added by the user by adding a `.repo` file in the directory mentioned above, or at the end of `/etc/zypp/zypp.conf`

---