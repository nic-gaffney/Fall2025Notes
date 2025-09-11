# Scheduling
09/11/2025

---
## Process states and transistions
### Process States
Scheduler maintains the status of each process that has been created but
not yet completed.

- **New**: The process has been created but not yet in memory
  > Happens directly after you run the command
  - PCB allocated, so it is *able* to give your process resources
- **Ready**: The process is in memory and waiting to be assigned a CPU by
the scheduler
- **Running**: The process is currently being executed by a CPU
  > The process will go between ready and running while being swapped out
  by the scheduler.
- **Blocked**: The process is waiting for some event to occur
  - IO
  - Lock aquisition
  - Timer to expire
- **Terminated**: The process has completed its execution
  - Deallocation of memory
    - Pages marked as free
  - Return PCB to list of free PCBs

> More states could exist if you can justify their existence

#### Additional states
- **Suspended** (Ready): the process is not in main memory and is not waiting for any event to occur
  > As soon as memory is available, get it back in and running again.
- **Suspended** (Blocked): the process is not in main memory and is waiting for any event to occur
  > Even if memory becomes free, keep it in secondary memory to wait for event

### Transisions
- New $\rightarrow$ Ready: The OS has allocated resources to the process including memory so it can be executed
- Ready $\rightarrow$ Running: The process has been selected for execution by the scheduler
- Running $\rightarrow$ Blocked: The process is waiting for something to happen
- Running $\rightarrow$ Ready: The process has been moved out of the CPU due to interrupt or some other reason
- Running $\rightarrow$ Terminated: The process has completed and is marked for clean up
- Blocked $\rightarrow$ Ready: The process has recieved the event or IO completion

#### Additional Transisions
- Ready $\rightarrow$ Suspended(ready): Scheduler moved process from memory to secondary storage
- Suspended (ready) $\rightarrow$ Ready: Scheduler moved process from secondary storage to memory
- Ready $\rightarrow$ Suspended(Blocked): Scheduler moved process (currently blocked) from memory to secondary storage
- Suspended (blocked) $\rightarrow$ Blocked: Scheduler moved process (currently blocked) from secondary storage to memory
- Suspended (ready) $\rightarrow$ Suspended(blocked): Process has recieved the event it was blocking for

## Scheduler components
- Long term scheduler: Decides which newly created process should be admitted for execution
- Medium term scheduler: Temporarily removes some processes from main memory
- Short term scheduler: Decides which process in memory should be assigned the CPU

Long term and medium term control the *degree* of multiprogramming

> The max number of processes that can be run

### Dispatcher
- *Context switch*: the process of changing the execution context on a CPU from one process to another
  - *saving* the execution context of the previous process
  - *loading* the execution context of the next processes
  > cannot *create* a process, simply transfers control
- *Dispatch latency*: the amount of time it takes the OS to stop one process and start another

#### Context
Execution context includes:

- Special and general purpose *CPU registers*
- Logical address translation data, including
  > Logical address relative to the process address 0x0 :exclamation:
  - Translation lookaside buffers (TLB)
  - Page tables
- Cache contents for hiding memory latency

Contents of the registers are saved in the PCB (process control blocks)

- Depending on the architecure, context switch may require flushing TLB and caches
- Some give [hardware support](https://wiki.osdev.org/Context_Switching#Hardware_Context_Switching) for such actions

#### Context switch vs Mode switch
- Mode switch involves changing the execution mode from kernel to user and vice versa
  - May save and restore only a subset of registers
  - Does not require flushing or modifying information associated with
  logical address translation or cache
  - Kernel instructions and data are shared among all processes by mapping them
  to a reserved portion of every address space
    - Avoids full context switch
    - Hardware support is *mandatory* to protext kernel instructions from misbehabing processes in user mode
- Context switching involves changing the process that the cpu is executing
  - More expensive than mode switch

### Not all Three
- Not all Operating Systems have all three components
  - Long and medium may not be supported
- Short term scheduler should be fast and incur minimal overhead
  - Much more frequently run than the other two schedulers

## Metrics for CPU scheduling
- Many different cpu scheduling algorithms have been proposed.
- A number of criteria or metrics have been identified to measure this.
### Commonly used metrics
1. **CPU Utilization**: Percentage of the time the CPU is busy
2. **Turnaround time**: the amount of time elapsed between when a process
arrives and when it completes its execution
3. **System throughput**: Number of processes completed per unit time
4. **Waiting time**: the sum of the time spent in the ready queue during the life
of the process; *time blocked is not part of the waiting time*
5. **Response time**: the amount of time elapsed between when a user submits a request and when the user sees a response
6. **Fairness**: Each process should get an equitable share of the CPU
