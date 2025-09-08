# Processes
8/28/2025

---
## Intro
### What is a process?
*A program that is ready for execution or currently executing.*
- When a user runs a program, the OS creates a process to execute the program
and **the program comes alive!**
### Realizing the abstraction
- A program only occupies space on disk.
- A process needs *many more* resources
    - **CPU** to decode and execute instructions :computer:
    - **Memory** to store instructions and data :book:
    - **IO devices** to interact with the outside world :keyboard:
#### CPU
Stores a lot of info about the process it is executing.

- **Program Counter (PC)** to store *address* of instruction being executed
- **Instruction Register (IR)** to store the *actual instruction* being executed.
- **General purpose registers** to *temporarily* store operands
    - *Arithmetic Logic Unit (ALU)* can only operate on data stored in CPU. :question: $\text{\red{why?}}$
        - $\text{\green{Registers are directly connected to the CPU. Main memory is not.}}$
- **Condition code registers (CCR)** to store the *result* of the operation
    - AKA *status register* or *flag register*
- **Stack pointer (SP)** to support *function* calls
    - Pushes current PC to the stack before jumping to the function, then `return` will return the SP to that PC after the function is done.

This is important to know because the OS is in charge of scheduling and swapping programs out of and into the CPU. It is important to save the state of the CPU when running the program, so when we return to that program it keeps its state.
**The OS swaps programs in and out of memory, so we must save the state.**

#### Main Memory
Main memory is used as a store for instructions and data of the process being executed. While a program is running, its instructions and data need to reside in main memory.

- CPU **cannot** access data stored on hard disk drive directly.
- :question: $\text{\red{What is the largest process that a machine can run?}}$
    - $\text{\green{idk lol}}$

Main memory is **orders of magnitude slower** than CPU.

- Caching is used to hide the latency
- Otherwise, CPU is idle most of the time.
- Different types:
    - addess translation
    - instruction
    - data
- Different Levels:
    - L1
    - L2
    - L3
    - L4
- Caching alone is not sufficient to keep CPU busy, other techniques needed.
#### IO devices
*Several* orders of magnitude slower than main memory.

Devices used to connect to the outside world such as:

- Keyboard
- Display
- Mouse
- Microphone
## Process Evolution
### Early history of processes
- A machine could only run *one* program at a time.
- A user was given *complete* control over the computer for a period of time
- Program and input data were punched into a deck of cards using a *keypunch*
- UI was *rudimentary*, users had to accomodate compters
- A computer would:
    1. Read the program from the cards
    2. Execute the program
    3. Write output to magnetic tape or printer
- Input was at the beginning, output at the end.
### Batch processing
- Smaller, slower, and less expensive computers were used to develop programs.
- Several jobs submited to larger, faster computers for **batch processing**.
    - Would run jobs one by one without intervention from user.
### Interactive processing
- Two independent trends:
    1. CPUs were becoming faster
    2. Programs were becoming more complicated, requiring *interactive* sessions with a user
### Improving CPU utilization
- Execute multiple programs together.
- :question: $\text{\red{Can you execute multiple programs using a single CPU?}}$
    - $\text{\green{No}}$

> known as *multiprogramming*
## Multiprogramming
The ability of an OS to execute more than one program using a single processor.

- Achieved by repeatedly *switching* to another process after executing the current for some time
- *Multiple processes* can make *progress* without any one process completing
- If switching rate is faster than human response rate, it *seems like* it has multiple CPUs

*True* simultaneous execution only possible with multiple CPUS

> Event based: for example, waiting for IO<br/>
Time based: for example, when a process has used the CPU for a sufficiently long time.

### Support Multiprogramming
1. Need a mechanism to allow the OS to [*stop* a process and *resume*](#stop-and-resume) it later
    - Switching can happen at *any time*
    - Switching should be *seamless*
    - Only side effect should be a *delay* in completion time
2. Need a mechanism to [*share resources*](#fair-resource-sharing) among concurrently running processes *fairly*
    - CPU, Memory, IO
    - No one process should be able to monopolize all resources
3. Need a mechanism to [*protect*](#protection) processes *from each other*
    - A process should not be able to read or write data of another process.
    > All processes running are loaded into main memory, so we must protect them from eachother. If protections fail, *hacks happen*.

#### Stop and resume
Maintain bookkeeping record of every process being executed

- Referred to as a **Process Control Block (PCB) :exclamation:**
    - Used to save *execution context* of an interrupted process.
- Records are maintained in a table referred to as a *process table*
> Basically an array of process control blocks.
- Maximum number of processes that can be run concurrently is *degree of multiprogramming*
    - Bound by the upper size of the process table.
    - May also depend on other factors like memory usage.
> If the process table is full, process creation will fail.<br/>
The OS itself must account for itself and its many processes in this table as well.
##### Process Control Block
> big data structure containing the following:

1. Process Identifier (PID): unique descriptor for process
2. CPU Registers Contents: PC, SP, CCR, etc.
3. Process State: State of the process
> new, ready, running, waiting, terminated
4. CPU Scheduling Information: Priority, scheduling queue info, other params.
> What if some process is significantly more important than others? Priority is the answer.
5. Memory-Management Info: base and limit register info, page and segment tables.
6. Accounting information: The amount of CPU time used, time limites, account numbers, job or process numbers, etc.
> Maybe a CPU intensive process taking a lot of *time* will need a higher priority.
7. IO status info: List of IO devices allocated to the process, list of open files, etc.

#### Fair resource sharing
Processes *cannot* directly manage resources. They must request access to a resource by invoking a *system call*

1. A syscall causes the execution control to be transferred to the OS
2. OS runs the requested call and returns control to the process

Every CPU supports at least two modes of execution / protection domains: :exclamation:

1. **User Mode**: CPU can only execute a restricted set of instructions
2. **Kernel Mode** CPU can execute *any* instruction
    - Also known as unrestricted, priveleged, or supervisory mode.
    - priveleged instructions can only be executed in this mode
    - a resource can be (de)allocated to a process using a priveleged instruction only
    - an elaborate mechanism is used to ensure only trusted code is executed in this mode
    - a switch to kernel mode is accompanied by execution of trusted code from one of the entry points

*Mode switch* refers to the change in the execution mode

Switch from user to kernel is preformed by a special hardware instruction called *trap*

- Trap instruction causes a software interrupt
- interrupt typically generated by hardware device (keyboard, mouse, clock)

##### Types of syscalls
Five broad categories:

1. Process control
> fork, exit, wait
2. File management
> open, close
3. Device management
4. Information maintenance
5. Communications

> Linux provides more than 300 syscalls

#### Protection
- **Seperate modes** for trusted and user code
- To protect processes from eachother, each process has its own **address space**
    - Address space of a process refers to a block of physical memory where the
    portion of process images are stored
    - Memory references in the program aretranslated to locations in the
    address space (*logical address* as opposed to *physical address*)
    - Special hardware is used to quickly translate logical address to
    physical address at runtime, and *validate* that the physical address
    belongs to the process being executed (covered in detail in memory
    management)

##### Address Translation
- Program references generate logical addresses assuming the process image has a starting address of 0.
- Each process has *address translation data* which may consist of one of the following:
    - Base and limit registers
    - Page table
- Address translation data is used to translate the physical address and validate it at run time
- Translation data can only be modified with *privileged instructions*.

$\text{\red{Why would the kernel need to modify this data?}}$ :question: <br>
$\text{\green{Kernel needs to swap the lower priority process out}}$

##### Privileged Instructions
Can potentially be *misused* by a user to access data belonging to another
process or to monopolize one or more resources. Other examples include:

- IO
- Interrupt
- Timer control
- Special processor status-setting instruction
- Storage protection

##### Address space
- Process P:
    - Base = 256
    - P[1] = 5, Physical memory is 257
- Process Q:
    - Base = 2048
    - Q[1] = 5, Physical memory is 2049

If P[1] becomes 10, Q[1] stays 5 because they are at different locations in memory.

## Process creation in Unix / Linux
### Fork
> Check out `$ info fork` or `$ man fork`

- Creates a replica child process whos process image is *identical* to
the parent process except for PID.
    - Processes arranged in *heirarchical* manner
    - Parent and child have *distinct* address space
- How can a process tell if it is the parent or child?
    - `fork` returns the PID of the child to the parent and 0 to the child
    - examine return value
- Both parent and child process *continue* their execution from the *next instruction* after `fork`.

<details>
    <summary>Example fork code</summary>

```c
int pid = fork();
if (pid == 0) {
    // Child
} else {
    // Parent
}
// Run by parent AND child unless child killed
```

</details>

### Exec
- *Replaces* current process


<details>
    <summary>Example exec code</summary>

```c
execl("/bin/ls", "ls", "-l", NULL);
// Will not run!
```

</details>

## Inter Process Communication (IPC)
Sometimes two processes need to communicate information or data.
> An applcation needs to print a file

An operating system may support one or more of the following mechanisms:

- File
- Shared memory
- Message passing
- Pipe
- Signal
- Remote procedure call

### Files
- Advantages: Persistent data **beyond current process accessing file**
- Disadvantages: Very high overhead. Accessing a file involves **a system call** and **transferring data between main memory and hard disk**

### Shared memory
- A portion of main memory is accessible to multiple proceses
    - A change made by one process in this portion is instantly visible to all processes
- Implemented by mapping parts of the address spaces of multiple processes to the same segment of main memory.
> Its like a global variable between processes
- Advantages: Low overhead, no involvment of the OS needed after initial setup.
- Disadvantages: Vulnerable to race conditions. Correct output only guaranteed under certain interleavings of steps, requiring additional synchronization. **Hard** to design.

### Message Passing
- A process can send a message to another process *asynchronously*. This message is then stored in a message queue until the recieving process asks for it.
    - Both sending and recieving requires **system calls.**
- Message passing may be *synchronous*.
    - Both sender and reciever have to be ready
    - Sometime referred to as rendezvous
    - Sender blocked until reciever is ready and vice versa
    - Sometimes used to mean *two way*
- Third option is *neither* blocks.
    - System call invoked by reciever returns if the message queue is empty.
- Maximizes concurrency but increases burden on programmer.
    - Only use when performance is key concern

- Advantages: easier to design, analyze, test, and debug
- Disadvantages: High overhead, expensive to implement as every message exchanged requires two system calls and two copying operations

### Pipes
- Similar advantages and disadvantages to synchronous message passing
    - Natural fit for producer consumer paradigm
- Almost identical to TCP/UDP
