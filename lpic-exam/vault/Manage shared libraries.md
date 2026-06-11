---
Weight: "1"
---
## Concepts of Shared libraries

A collection of code that are intended to be used by many different programs.

**Static libraries:** A copy of the library code is embedded into the program and becomes part of it.

**Shared (or dynamic) Libraries:** At run time, the linker simply takes care that the program references libraries correctly. So, the shared library must be available to satisfy the program's dependencies. This approach is to manage system resources as it helps reduce the size of program files and only one copy of the library is loaded in memory, even when it is used by multiple programs.

## Configuration of Shared Library Paths

- `/etc/ld.so.conf`
- `/etc/ld.so.conf.d/`

## Searching for the Dependencies of Particular Executable

1. Find out the full path of the executable 

```bash
which <command>
```

2. Search for the dependencies of a shared objects

```bash
ldd /path/to/<command>
```



---