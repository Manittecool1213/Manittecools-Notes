---
title: Threads and Concurrency
draft: false
tags:
---

# Questions
- If semaphores are the elements used to create locks, how are semaphores themselves locked?
---
# What are Threads?
- A thread is a light-weight process.
- Multiple threads can run within the same process. Each gets its own stack, but shares the code, data and heap segments with the other threads of the process.
- (aside) Chrome is multi-processed while Firefox is multithreaded.
- Why not have multiple child processes running the same program?
	- Too much memory consumed by identical memory images.
	- IPC required to share information across processes. This can instead be done by using the shared memory.
- How can the same code be run by multiple threads? Code is read-only, and each thread gets its own independent program counter.
- Each thread has a separate CPU context during execution.
- No notion of parents and children in threads, but 'main' is typically the primary thread from which other threads are spawned.
---
# Concurrency v/s Parallelism
- Concurrency: running multiple threads / processes at the same time, even on a single CPU core, by interleaving execution.
- Parallelism: running multiple threads / processes in parallel over DIFFERENT CPU cores.
- Concurrency is a software ILLUSION, parallelism is truly performing tasks simultaneously.
---
# POSIX Threads
- Join in threads: the spawner thread will wait for its spawned threads to finish before it stops.
- When using POSIX threads, the function called by the thread needs to return a void pointer.
- When compiling a program with threads, it needs to be linked with the `-lpthread` flag.
- The execution order of threads is not guaranteed when using the default scheduler. If the priority of threads is the same, the scheduler might pick one thread before the other.
- A thread will only execute the function it has been passed, and will then stop execution. It will NOT execute the remainder of the calling code.
--- 
# Mutual Execution and Locking
- Code segment which requires mutual execution - critical segment.
- Without mutual execution, different threads might read and write different values for the same variable.
- In order to avoid this, locks need to be used.
### Semaphores
- Various ways to implement such a lock - one of them is a semaphore.
- Two functions on a semaphore variable:
	- Sema down / wait - decrements counter by one, blocks calling thread if resulting value is negative.
	- Sema up / post - increments counter by one, wakes up any one thread that is blocked on the semaphore.
- (aside) How is atomicity achieved?
	- Before critical segment - interrupt disabled.
	- Critical segment performed.
	- Interrupt re-enabled.