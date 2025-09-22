---
title: Translation Lookaside Buffer
draft: false
tags:
---
- TLB cache: stores virtual address - physical address map for faster access. This is a physical cache connected to the processor.
- On cache hit, the the full page table walk is no longer required, and the required physical address is instead supplied by the TLB. 
- This can then be used in conjunction with the L1/L2 caches, which would store a {physical address : data} mapping. Critically, these two are INDEPENDENT. What is stored in the cache is NOT dependent on what has been cached in the TLB. 
- Own approach: 
	- The TLB stores either a Virtual Address (VA) to Physical Address (PA) mapping OR a VA to data mapping if the element is cached. In this case, the caches become dependent. 
	- Cache is now larger because it stores data only, and not addresses.
	- Pros:
		- Larger cache.
		- Faster access of cache because one O(1) access is reduced from the pipeline.
	- Cons:
		- Dependence of caches.
		- (STILL not satisfied as to why this is so bad).
---
- OS as part of address space for every process:
	- Options:
		- OS code part of address space for every process.
		- OS is separate from this address space, stored somewhere else, but accessed by every process. This would effectively mean that the OS is an independent process.
	- Why the first is better: Faster syscall / any OS code processing, because one less context switch is required. If the OS is one common process used by every other process, there would need to be a context switch to this process before the actual kernel mode purpose could be serviced.
	- Inspite of this, the process doesn't gain access to the kernel code. Although the process's page table contains entries corresponding to kernel code, there would be some flag (likely control bit) which would indicate that the data stored there is OS code. If a process attempted to access this code, there would be a seg fault.
