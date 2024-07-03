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

* ***The kernel is responsible for context switching. To understand how this works, think about a situation in which a processis running in user mode but it's time slice is up . Here what happens:***

1. The CPU (the actual hardware) interrupts the current process based on an internal timer, switches into kernel mode, and hands control back to the kernel.

2. The kernel records the current state of the CPU and memory, which will be essential to resuming the process that was just interrupted.

3. The kernel performs any tasks that might have come up during the preceding the time slice (such as collecting data from input and output operations.)

4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready to run and one.

5. The kernel prepares the memory for this new process and then prepares the CPU.

6. The kernel tells the CPU how long the time slice will take for the new process will last.

7. The kernel switches the CPU into user mode hands control of the CPU to the process.

* The context switch answers the important question of when the kernel runs. The answer is the it runs between process time slices during a context switch.

* ***The kernel also manage memory during a context switch, which can be a complex job. The following conditions must hold:**

1. the kernel must have it's own private area in memory that user process can't access.

2. Each user process needs it's own section of memory.

3. One user process may not access the private memory of another process.

4. User proxesses can share memory.

5. Some memory im user processes can be read only.

6. The system can use more memory thst is physically present by using disk space as auxiliary.

* `Note:` The implementation of a amemory address map is called a page table.
 
* A device is typically accessible only in kernel mode because improper access (such asa user process asking to turn off the power) could crash the machine.

* The different devices rarely have the same programing interface.

* To present a uniform interface to user proceses in order to simplify the software developer's job.

* There are several other kinds of kernel features available to user processes. **Example:** System calls (or syscalls) performs specifictasks that a user process alone cannot do well or at all. The acts of operating, reading and writing files all involve system calls.

> Two system calls, **`fork()`** and **`exec()`**, are important to understand how processes start:
>
> > *Fork():* When a process calls *fork()*, the kernel creates a nearly identical copy of the process.
> >
> > *Exec():* When a process calls *exec(program)*, the kernel leads and starts program, replacing the current process.
>
> When you entera command into a terminal window, the shell that is running inside the terminal window calls *fork()* to create acopy of the shell, and then the new copy of the shellcalls*exec(command)* to run command.

```ruby
+-------------+          +------------+                +-------------+
|    shell    | ------>  |    fork    |  ----------->  |    shell    |
+-------------+          +------------+       |        +-------------+
                                              |        +-----------------+          +---------------+
                                              +----->  |  copy of shell  | ------>  | exec(command) | -----+
                                                       +-----------------+          +---------------+      |
                                                                                                           ⌄
                                                                                                     +-----------+             
                                                                                                     |  command  |
                                                                                                     +-----------+
```










