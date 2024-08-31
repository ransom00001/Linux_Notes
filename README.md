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

* The memory is also dynamicly segmented into kernel and user space. Kernel space contains kernel data and user space contains normal process data. Normal process cna never     acess kernel space data and vise-versa.

* Main memory stores program, data, state and user data.

* One of kernel's tasks is to split memery into many subdivisions.

* ***The kernel is in charge of managing tasks in four general system areas:***

1. ***Processes:*** The kernel is responsible for determining which processes are allowed to use the CPU.

2. ***Memory:*** the kernel needs to keep track of all memory -what is currently allocated to a particular process, what might be shared between processes, amd what is free.

3. ***Device Driver:*** The kernel act as an interface between hardware (such as a device) and processes. It's usually the kernel he kernel's job to operate the hardware.

4. ***System salls and support:*** Processes normally use system calls to communicate with the kernel.

* ***Process management:*** Describes the starting, pausing, resuming, scheduling, and terminating of processes.

* The processes use the CPU for a small fraction of a second, then pauses; then another process uses the CPU for another fraction of a second; then another process takes a      turn, and so on. Each piece of time is called -time size.

* The act of one process giving up control of the CPU to another is called a context switch.

* ***The kernel is responsible for context switching. To understand how this works, think about a situation in which a processis running in user mode but it's time slice is     up . Here what happens:***

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

  >`Note:` The implementation of a amemory address map is called a page table.
 
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
> When you entera command into a terminal window, the shell that is running inside the terminal window calls *fork()* to create acopy of the shell, and then the new copy of     the shellcalls*exec(command)* to run command.

```
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
            
  >`Note:` The process asking the kernel to create another process must perform a *fork()* system call. This notation derives from the way the call would be written in the C      programming language.

* The kernel also supports user processes with features other than traditional system calls, the most common of which are pseudodevices. Pseudodevices look like devices to      user processes, but they are implemented purely in software. This means they don't technically need to be the kernel, but are usually there for practical reasons.

* Random number generatet device (/dev /random).

* A user processes that accesses a pseudodevice must use a system call to open the device, so processes can't entirely avoid system calls.

* The main memory that the kernel allocates for user processes is called user space. Because a process is simply a state (or image) in memory, user space also refers to the     memory for the entire collection of running processes.

* Most of the real actions on a linux system happens in user space. Though all processes are essentially equal from the kernel's point of veiw, they perform different tasks     for users.

* Basic services are at the bottom level (closest to the kernel), utility services are in the middle, and applications that are users touch are at the top.

* ***Interface:*** Interface is the way of giving or taking information or objects.

* ***User Pracesses***

```
                 +-------------------+
                 | communication bus |  
                 +-------------------+
                     ^           ^
               +-----|           |------+
               |                        |
+------------------+                +-----------------+
|  user interface  |  <-----------> |   web browser   |
+------------------+                +-----------------+
     |          |                           |
     |          |                           |
     |          |                +----------------------+
     |          |                | name catching server |
     |          |                +----------------------+
     |          +---------------------+    |
     |                                |    |
+-----------------------+       +--------------------+
| network configuration |       | diagnostic logging |
+-----------------------+       +--------------------+
```

* Linux is a unix flavour at heart.

###### The Bourne Shell: /bin/sh

* The shell is one of the most important parts of a umix system. A shell is a progeam that runs command. These commands can be other programs or built -in features of the       shell.

* We can also create our own commands.

* ***Shell Scripts:*** Text files that contains a sequence of shell commands

* There are many different Unix shells, but all derives features from the  bourne shell (/bin/sh).

>`For more details about Unix for beginners than you’ll find here, consider reading The Linux Command Line, 2nd edition (No Starch Press, 2019), UNIX for the Impatient, 2nd edition (Addison-Wesley Professional, 1995), and Learning the UNIX Operating System, 5th edition (O’Reilly, 2001).`

* Every unix system needs a version of the  bourne shell in order to funtion correctly.

* Limux uses an enhanced version of the bourne shell called bash or the "bourne-again" shell.

  >`Note:` the bash shell is the default shell on most Linux distribution, and /bin/sh is a link to bash on a Linux system.

* ***Echo command:*** echo is a Linux/Unix command tool used for displaying lines of text or string which are passed as argument on the command line.

* ***Argument in command:*** command usually begin with a program to run and may be followed by arguments that tell the program what to operate and how to do so.

* ***Cat command:*** the cat command reads each file parameter in sequence and write it to standard output.

  >`Note:` many arguments are options that modify the default behavior of a program and typically begin with a dash (-).

* The cat program simply outputs the contents of one or more files or another source of input.

* Unix processes use I/O streams to read and write data. processes read data from input streams and writes to output streams.

  >`Note:` in linux and conputer programing in general, standard streams are input and output (I/O) communication channels betwween a program and it's environment.

* Cat reads from the standard input streams provided by the Linux kernel rather then a stream connected to a file, the standard input is connected to the terminal where you run cat.

* standard output is similar. The kernel gives each process a output stream where it can write it's output. The cat command always writes it's output to the standard output. When you ran catin the terminal, standard output was connected to that terminal, so that where you saw the output.

## Linux Structure

```
                                         +-------+  
                                         | LINUX |
                                         +-------+
                                             |
   +--------+-------+-------+-------+--------+--------+-------+-------+-------+-------+
   |        |       |       |       |        |        |       |       |       |       |
 /boot    /dev    /usr    /bin    /sbin    /home    /lib    /tmp    /var    /etc    /proc
                    |                        |
              +-----------+             +---------+
              |           |             |         |
           local        /bin          user1     user2...
              |
            /bin
```
* The Linux file system is a cryptic labyrinth of directories defined by the the filesystem hierarchy standard.

* A Linux file system can have miltiple users on a computer.

  >`Note:` * ***root user:*** The special user in the /etc /passwd file with the user ID [UID]of [0]

* *Binaries:* bin directories in Linux are dedicated areas for storing executable files.

* *Executable files:* an executable file is one which can be run as a program.

* Binaries or executables are essential to the entire operating system, you can run these binaries from the command line at any time.

### Directories

* * ***/bin directories:*** binaries -> commands that are essential to operate an system.

* ***/sbin directories:*** system binaries that should only be executed by the root user.

* ***/lib directory:*** many of the directories may share common libraries which are stored in the lib directory.'

* ***/boot directory:*** to load operating system files into main memory is known as booting.

* ***/dev directory:*** (device files). here you can interface with hardware or drivers.

* ***/var directory:*** store log files and cache files.

* ***/proc directory:*** keep track of running processes but don't really exist.

* ***forward /:*** root directory.

* ***/root directory:*** root user can use only.

* ***/home directory:*** home directory is a personal directory assigned to a user on a Unix or Linux- based system.

* ***/bin:*** binaries -> commands that are essential to operate an system.

* ***/sbin:*** system binaries -> only root user can use it. Only used for major changes in configuration file or for system maintanence.

* ***/proc:*** process information -> all the processes exist in the directory.

* ***/boot:*** boot loader files.

* ***/dev:*** device files ->

```
                                         /dev
                                           |
                                +----------+-------------+
                                |          |             |
                             files    directories   device files

```
1. Files -> plain text files.......
2. Directories -> (folders).
3. Device files -> special type of files -> interface between hardware and software.

* ***/mnt:*** (mount directories) -> it shows external storage device data.
  EX: hardware, pendrive, etc.

* ***/media:*** (removable device files) -> EX: data of pendrive will show in media directory.

* ***/etc:*** (editable text configuration).

* ***/srv:*** (service data).

* ***/sys:***  (system). all system data like kernel, hardware.

* ***/lib:*** (system libraries).

* ***/tmp:*** (temporary files).

* ***/usr:*** (user programs).

* ***/var:*** (variable files).

* ***/opt:*** (optional applications).

  >`Note:` *bits:* binary digits (0 and 1)

#### Commands

* ***pwd:*** This command shows where we are.

* ***sudo su:*** This command makes you a *Root user*
  
* ***cd command:*** change directory.

* ***cd .. or cd ../ :***
 
* ***cd ../.. :***
 
* ***cd - :***

* ***cd ~ :***

* ***cd --help:***
 
* `To create a New File- 'nano (file name)' will help.`
 
##### ls commands

* ***ls:*** (lists contents). With ls command we can list out the contents of a directory.

ls syntax

+---------------------------------------------------------------------------------------------------+
|   ls   |  Options  |    Work                                                                      |
||
|   ls   |    -l     |  displays detailed information about files and directories.                  |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -a     |  displays all files and directories including hidden files and directories.  |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -d     |  lists directories themselves.                                               |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -g     |  displays files and directories with group ownership.                        |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -h     |  print file sizes in human-readable formate. (Eg: 1K, 234M,2G).              |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -i     |  displays files and directories with index number.                           |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -p     |  it marks a slash in front of directories.                                   |
|--------|-----------|------------------------------------------------------------------------------|
|   ls   |    -r     |  display the reverse order of the default order of listing.                  |
|--------|-----------|------------------------------------------------------------------------------|































