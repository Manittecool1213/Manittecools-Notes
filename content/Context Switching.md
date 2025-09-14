---
title: Context Switching
draft: false
tags:
---
# Questions
- How is 'privilege' decided on a hardware level? Is 'mode' decided by a pin?
	- No pin; just a logical abstraction.
- What additional security is provided by maintaining a kernel stack?
	- Just that kernel code addresses are not known.
	- The CPU knows the address of the kernel stack. If a processes attempted to access the kernel stack, the CPU would know that it needs to be in privileged mode to run it, and would accordingly not run the code.
- There might be a deeper reason behind why the OS and the microprocessor have so much overlap (interrupt vectors, etc.). Find it.
- Is a multi-core processor able to handle multiple blocking calls at the same time? 
- How does multiprocessing really work? Are there additional registers available?
---
- (aside) https://linux-kernel-labs.github.io/refs/heads/master/
- Process Control Block - struct containing information about process.
	- In order to pause a process, its *context* needs to be saved. This includes:
		- Its memory image (code, data, stack, etc.).
		- The pointers to its memory image.
	- This information is stored in the PCB.
- Once a process has been context switched in, it runs in user mode. The OS is responsible for this context switch. The OS will run again when:
	- A system call is made, requesting OS services.
	- An external devices needs attention and raises an interrupt.
	- Some fault has happened during program execution.
- All such events - called CPU traps into OS code.
- OS is **not a separate process**. It runs in the kernel mode of all existing processes.
---
# System Calls
- Each process has a kernel stack. When a system call is made, and the OS needs to be 'activated', user context is pushed onto the kernel stack (which can only be accessed in the kernel mode).
- After the kernel mode operation is complete, the kernel can use this information to continue user mode execution.
- How is the program counter updated when entering the kernel mode? Using the Interrupt Descriptor Table (IDT) or Trap Table:
	- This table is setup by the OS during boot. It is not modifiable in user mode.
	- CPU uses IDT to locate address of OS code to jump to.
- When user code wants to make a system call, it invokes a 'trap instruction' with the index into the IDT array as an argument.
- In order of operations for servicing trap: DO NOT forget CPU moving to higher privilege level - this is the FIRST thing which happens.
- The *CPU* handles trap servicing (without even using memory) because you wouldn't want any process to know IDT addresses.
---
# Context Switching
- OS scheduler needs to run in kernel mode. Servicing a trap is a good opportunity to perform scheduling. Consequently, the return-from-trap might switch back to a *different* process than the one which called it. This is how context switching takes place.
- When performing a context switch, the *kernel* context needs to be saved (the CPU is currently in kernel mode). This context is similar to a user process context; it allows resuming operations. 
- Not all system calls are atomic. While a read is going on, the CPU is free to perform other operations. However, it would eventually need to return to the processing calling the read, for which context is required.