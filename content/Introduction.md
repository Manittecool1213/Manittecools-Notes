---
title: Introduction
draft: false
tags:
---
---
-  What is the kernel?
	- Core functionality of OS.
- Microkernels v/s Monolithic kernels:
	- Monolithic kernels, such as Ubuntu, will load all their functionality at once.  There is one large kernel executable.
	- Microkernels are extremely modular, and will load functionality as and when required.
- Responsibilities of the OS:
	- Making it easy to **run** programs.
	- Allowing programs to **share** memory.
	- Enabling programs to **interact** with devices.
--- 
# Shell
- What is the shell?
	- A program that takes user commands, sends them to the OS and shows you the results.
	- It's called the 'shell' because it is the outer layer that the user interacts with.
	- While the kernel forms the 'heart' of the OS (managing CPU, memory, etc.), the shell is a friendly interface for humans to give it instructions.
--- 
# Virtualisation
- Broadly, virtualisation is the illusion that every process is the only one running, and has access to all available resources.
- The OS takes a physical resource and transforms it into a virtual form of itself.
	- Physical resource: processor, memory, disk, etc.
	- The virtual form is more general, powerful and easy to use.
	- The OS is sometimes referred to as a virtual machine.
- With virtualisation, a single CPU can be converted into a seemingly infinite number of CPUs, allowing many programs to seemingly run at once.
- Concurrent execution:
	- The CPU can run multiple programs concurrently with context switching.
	 ![[Screenshot 2025-08-12 at 3.12.07 PM.png]]
	- Flow:
		- Run user code for process A for some time.
		- Pause A, save context of A, load context of B (context switching)
		- Run user code for process B for some time.
		- Switch again.
	- Every process thinks it's the only process running on the CPU; saving and loading context ensures that the process sees no disruption.
### Virtualising Memory
- Through context switching, it is as though each program has its own private memory.
- There is no locking or race condition. Each program running concurrently can independently access the same memory location.
- Address spaces:
	- The OS gives each process the illusion that its memory image is laid out contiguously from memory address 0 onwards. This view is known as the virtual address space.
	- In reality, processes are allocated free memory in small chunks all over the RAM, at some physical address not made aware to the programmer.
	- (aside) Pointer addresses printed by programs are virtual addresses, not physical addresses.
	- When a process accesses a virtual address, the OS arranges to retrieve data from the physical address.
---
# Modes
- User programs run in the user (unprivileged) mode, where the CPU can execute only unprivileged instructions. The OS runs in the kernel (privileged) mode, where the CPU can execute both kinds of instructions.
- The CPU shifts from the user to the kernel mode, and executes OS code when one of the following events happen:
	- System calls: user requesting for OS services.
	- Interrupts: external events which require the attention of the OS.
	- Program faults: errors that need OS attention.
- After performing the required actions in kernel mode, the OS returns back to the user program, and the CPU returns to user mode.
---
