# Linux_Notes

* OS is a peice of system software that manages hardware resources like - CPU, memory and bulk devices.

* OS also provides an efficient and secure environment for processes.

* OS also provides security to users and processes.

* OS also provides abstraction.

* ***Abstraction:*** It is the process for hiding objects, processes and procedures.

* ***Multilevel Abstraction:*** It is abstraction done at multiple levels.

```
+------------------+
|       User       |
+------------------+
| User Application | __
+------------------+  |
|System Application|  |
+------------------+  |
|  System Utility  |  |--OS Layers
+------------------+  |
|      Kernel      |  |
+------------------+  |
|     Hardware     | __
+------------------+ 
```

* User gives command to user or system, application(s) interect with system utility, then system utility interect with kernel, and kernel directly interects with Hardware.

* The Linux kernel contains system calls and device drivens, it is also responsible for core hardware management and process management.

* Linux basesd operating system has two modes of running kernel mode. Kernel space and user mode/space.

* High priority tasks are done by kernel and kernel runs in kernel mode.

* Normal priority tasks are done in user mode.

* The memory is also dynamicly segmented into kernel and user space. Kernel space contains kernel data and user space contains normal process data. Normal process cna never      acess kernel space data and vise-versa.

* Main memory stores program, data, state and user data.

* One of kernel's tasks is to split memery into many subdivisions.

* ***The kernel is in charge of managing tasks in four general system areas:***

1. ***Processes:*** The kernel is responsible for determining which processes are allowed to use the CPU.

2. ***Memory:*** the kernel needs to keep track of all memory -what is currently allocated to a particular process, what might be shared between processes, amd what is free.

3. ***Device Driver:*** The kernel act as an interface between hardware (such as a device) and processes. It's usually the kernel he kernel's job to operate the hardware.

4. ***System salls and support:*** Processes normally use system calls to communicate with the kernel.

* ***Process management:*** Describes the starting, pausing, resuming, scheduling, and terminating of processes.

* The processes use the CPU for a small fraction of a second, then pauses; then another process uses the CPU for another fraction of a second; then another process takes a       turn, and so on. Each piece of time is called -time size.

* The act of one process giving up control of the CPU to another is called a context switch.

* The kernel is responsible for context switching. To understand how this works, think about a situation in which a processis running in user mode but it's time slice is up . Here what happens:

1. The CPU (the actual hardware) interrupts the current process based on an internal timer, switches into kernel mode, and hands control back to the kernel.

2. The kernel records the current state of the CPU and memory, which will be essential to resuming the process that was just interrupted.

3. The kernel performs any tasks that might have come up during the preceding the time slice (such as collecting data from input and output operations.)

4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready to run and one.

5. The kernel prepares the memory for this new process and then prepares the CPU.














