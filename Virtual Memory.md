---
title: Virtual Memory
draft: false
tags:
---
# Question
- Virtualisation is an expensive endeavour. What then is the purpose of virtualising memory? If every process can't actually have all the memory, why tell the processes that memory is completely independent?
- Does virtualisation imply that even non-contiguous addresses can be referred to in a contiguous manner?
	- Yes. Without this, there might be a situation where non-contiguous chunks of memory were available, but would not be allocated because of their non-contiguous nature. 
	- Also answers the previous question; even in an HPC setting, virtualisation is not bypassed.
- Why is the code-heap-stack order not followed at the physical level, when this arrangement and proximity is beneficial?
- Can reallocation of memory internally take place without virtual address changing? Does it?
---
- CPU registers also have access to only VIRTUAL addresses.
- Even in the virtual space, the internal order of code-then-heap-then-stack is followed. However at the PHYSICAL level, this is no longer true.
- MMU: 
	- Hardware unit which performs virtual to physical address conversion.
	- Why bother with an MMU? Why not let the OS do the computation?
		- Speed: dedicated hardware faster than CPU in this context.
		- Too much switching: every time a memory address would need to be made, the program would need to go from user to kernel mode - too much switching, too much overhead.
- Issues with physically contiguous allocation of code-heap-stack:
	- Heap and stack might expand.
	- You may never use a lot of the heap, leaving its memory forever empty a s a gap between code and stack. This could instead be used for something else.
- Alternative to contiguity: segmentation.
	- Instead of using just 2 pointers for base and bound, use 6 registers - acting as base and bound for each of the code, heap and stack segments.
	- This is now outdated because of the drawbacks of segmentation, viz. needing non-contiguity within the same segment. Paging is now used instead.
	- Another drawback: external fragmentation - the gaps between segments are too small to be used for anything else.
		- Solution - defragmentation by idling system, moving around memory elements to be contiguous. This solution is expensive and not always practical; need better ones.
- How does the MMU know which base-bound register pair to be used when a virtual address is encountered?
	- 1 approach: context - if address comes from PC, must be code segment, if it came from SP, it must be stack segment, else heap segment.
	- another approach: expanding address and using first two bits which explicitly indicate which segment is being accessed.