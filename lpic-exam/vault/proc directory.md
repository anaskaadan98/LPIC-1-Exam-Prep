- This is the directory were the kernel keeps it's running commands
- It is created in RAM when the computer boots

The information of `lspci`, `lsusb` and `lsmod` are kept in the following files:

| Name of Directory  | Description                                                    |
| ------------------ | -------------------------------------------------------------- |
| `/proc/cpuinfo`    | List detailed information about the CPU                        |
| `/proc/interrupts` | A list of numbers of the interrupts per IO device for each CPU |
| `/proc/ioports`    | List currently registered IO port regions in use               |
| `/proc/dma`        | List the registered DMA (Direct Memory Access) channels in use |
