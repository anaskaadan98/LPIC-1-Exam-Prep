---
Weight: "2"
---
# Introduction

A multitasking or multiporcessing operating system can run multiple processes at once. On a single-processor system, this is achieved by rapidly switching between processes to create the illusion of simultaneous execution. The same technique is also used in symmetric multiprocessor (*SMP*) systems because there are often more processes than available CPU cores.

## The Linux Scheduler

Linux is a preemptive multi-processing operating system that implements a scheduler that organizes the process queue. Every process has two predicates that intervene on its scheduling: the *scheduling policy* and the *scheduling priority*.

**Scheduling policies**:
- real-time policies
- normal policies

## Reading Priorities

Linux reserves static priorities:
- real-time processes \[0 to 99]
- normal processes \[100 to 139]

Lower value meaning higher priority.
The static priority of an active process can be found in the `sched` file, located in its respective directory inside the `/proc` filesystem.

The PID 1 process is the *init* or the *system* process, the first process the kernel start during system initialization.
The standard priority for normal processes is 120, so it can be decreased to 100 or increased to 139.
You can verify the priority of all running process can be verified with the command `ps -Al` or `ps -el`.

The `PRI` column indicates the static priority assigned by the kernel and the actual priority is obtained by adding 40.

## Process Niceness

Every normal process begins with a default nice value of 0 (priority 120)
Nice numbers range from -20 (less nice, high priority) to 19 (more nice, low priority)
The `NI` column in `ps` output indicates the *nice* number.

Only the `root` user can decrease the niceness of a process below `zero`.

| Command                     | Purpose                                                                             |
| --------------------------- | ----------------------------------------------------------------------------------- |
| `nice -n`                   | Change the niceness to a specified value                                            |
| `renice -# -p <process-id>` | Change the value of niceness for a process                                          |
| `renice +# -g users`        | The niceness of processes owned by `users` of the group `users` will be raised in # |

---