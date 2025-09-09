# Multiprogramming
09/09/2025

---
## Concurrency
- Use *multiple* processes
  - Different processes run on seperate processors or seperate tasks
- Processes need to share resources
  - Use IPC

### Using processes
Solves both problems, with a hitch:

1. Needs an **explicit setup** to enable processes to share memory
2. **Creating and destroying** processes is quite *expensive*
  - Must allocate many resources
3. Switching between processes is also expensive
  - Switching between two processes requires **saving** state of one process
    and **loading** state of another
  - Especially important in a uniprocessor machine since **all processes**
    need to share the same CPU

> Suboptimal utilization of resources resulting in <br>
1. increased execution time <br>
2. higher response time for interactive apps

## Threads
- Allow *related* processes to *share* resources including address space while
also protecting unrelated processes from eachother
- Allow *multiple execution flows* within a single address space
  - Each execution flow is referred as a *thread* (initially referred to as tasks)
#### Thread specific resources
- Program Counter
- Instruction register
- Condition Code Register
- Stack Pointer
- General Purpose CPU registers
#### Process specific resources
- Address space
- code
- data
- heap
- memory
- cache

> Processes contain threads :exclamation:

### Evolution
#### Inception
Initially, neither language (C/C++) nor kernel offered support for threads.

- Multi-threaded programing was only possible with third party libs such as
POSIX (portable operating system interface)
- Kernel was oblivious to a process containing many threads

Threads were created destroyed and managed completely in user space with no help from the kernel **(User level threads, ULT)**

#### Now
As threads became more popular, more comprehensive support for multi-threaded
programming emerged.

- Popularity increased after the introduction of multi-core machines
- Kernels are now aware of multiple threads in a process
- C/C++ added built in support for multi threading in 2011
- Java supported multithreading from its inception

In many operating systems, threads are created, destroyed, and managed completely
in kernel space

- Referred to as kernel level threads
- Kernel maintains information in thread control block
  - Analogous to process control block

### Pros and cons (ULT vs KLT)
#### User level threads
- Pros:
  - Low overhead: cheaper to C,D,M than KLT
  - Flexible scheduling: Thread scheduling can be tailored on a per application
    basis.
- Cons
  - No parallelism: Only one thread can be run at a time (even with multiple
    CPUS).
  - Dependent progress: If one thread invokes a blocking operation, the entire
    process is blocked

#### Kernel level threads
- Pros:
  - Optimal CPU utilization: Each hread can be run on a seperate processor
  - Independent progress: If one thread invokes a blocking operation,
    then only that thread is blocked
- Cons
  - High overhead

### Thread abstraction models
1. Many to one (ULT): Only ULT
2. One to one (KLT): Only KLT
3. Many to many (hybrid): Process has user level and kernel level threads
  1. Very hard to implement

## Issues when implementing threads
### Semantics of fork and exec syscalls
If a thread invokes `fork`, should the new process copy *all threads*?

- Oftentimes, `fork` is called only to immediately call `exec`, which would
make it highly inefficient to create so many threads only to be destroyed

Many implementations of Unix/Linux provide both variants.

### Signal handling
Should a signal be delivered to *one* or *all* threads?

- Possible alternatives to deliver the signal to:
  - All threads
  - Certain threads
  - A single thread
  - Thre thread to which the signal applies
  > such as illegal instruction

The best choice depends on the *signal type*. In some variants of
Unix/Linux, the signal *handler* is process specific but the signal *mask*
is thread specific.
> Among all the threads that are willing to recieve the signal, one is chosen
arbitrarily to handle the signal.
### Thread cancellation
Cancel a thread if it is no longer needed

Two types of cancellation:
1. Asynchronous: Cancelled immediately
2. Deferred: Thread is notified to cancel itself by setting a flag that is
read periodically by the thread.
  > Desirable if the thread is in the middle of modifying shared data, so
    Asynchronous cancellation would corrupt the data.

### Thread-local storage
Sometimes each thread needs its own seperate copy for certain variables

- Helps reduce programming errors

## Optimizations
1. Thread pools: Create a collection of threads once and select a free thread to perform a specific task when needed :exclamation:
  1. Improves performance of applications in which new tasks arrive / are generated at runtime
  2. Eliminates overhead of creating and destroying at runtime.
2. Grand Central Dispatch (GCD): Apples implementation of thread pools with
   other enhancements for managing concurrent operations more easily and
   efficiently

> Context switch: Switching from one process to another <br>
Mode switch: User to Kernel and vice versa :exclamation:
