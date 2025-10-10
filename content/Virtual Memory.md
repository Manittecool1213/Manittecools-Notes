---
title: Virtual Memory
draft: false
tags:
---
# Notes
- [[Introduction and Basics]]
- [[Paging Basics]]
- [[Paging Optimisations]]
- [[Translation Lookaside Buffer]]
- [[Demand Paging]] 
---
# Cache Eviction Policies
- LRU - temporal locality.
- Prefetching - spacial locality - swapping *in* memory locations close to one which was requested, to reduce access time in the even that it *does* get used. The philosophy of this paradigm is that the likelihood of this access pattern is high.fj
---
# Computing Effective Access Times
- Information given:
	- Memory Access Time: x
	- TLB Access Time: y
	- TLB Hit Rate: z
- Assumptions:
	- Single level page table
	- No caches
- Effective Access Time = (z) (y + x) + (1 - z) (y + 2x)
	- Justification:
		- If there is TLB hit, TLB access takes y time followed by memory access with x time
		- If there is a miss, there has already been one TLB access with y time. There is then one memory access into the larger page table with x time, followed by another x time access to actually access the required page itself.
	- How things change with a multi page table:
		- Second part of expression gets more '+x's ((y + 3x) for 2 level page table and so on).
		- This is because you now have to access memory more times to get to the final level of the page table which would give you the memory address of the required page.
---
# Memory Allocation from User PoV
- brk and mmap syscalls:
	- Both allocate some memory in virtual address space (valid bit becomes 1). This does not guarantee that the memory will be present on RAM (i.e., present bit not necessarily 1), but the valid bit DOES become 1.
	- brk: changes the location of the program 'break', which defines the end of the process's data segment. 'Increasing' the break allocates more memory, 'decreasing' it de-allocates it.
		- Variant: sbrk: increases break by number of bytes passed as parameter.
	- brk, sbrk function only to change the bounds of allocated virtual memory. It can expend or shrink the limit of in-use memory.
	- mmap: allows non-contiguous backend allocation; an mmap call for a large chunk will possibly be serviced by smaller non-contiguous pieces which collectively make up the entire space.
		- Used to handle file reads and writes.
- Ultimately, malloc and free aren't themselves syscalls, but make syscalls.
### Allocators
- Can be specific (more efficient, fixed size) or general purpose (variable size).
- Read up on: slab allocation algorithm.
- Fixed size allocators:
	- In this approach, you have lists for chunks of specific sizes.
	- There would then be pages which are supposed to store only chunks of a specific size. 
	- There would be no coalescing algorithm in this approach. Even if additional contiguous space was available, two contiguous chunks would not be combined, because the goal was to store discrete chunks of that particular smaller size.
- Buddy system in variable size allocation:
	- Keep creating smaller chunks in powers of until you reach the power of two closest to the space you want to allocate.
	- This makes merging to larger blocks easier upon freeing.
	- Con: what if you have a chunk JUST larger than a power of two? You would use the next power of two, wasting a LOT of space.
- Read up on 
### Free List
- Data structure to keep track of free space in heap.
- Splitting: divide one contiguous chunk into smaller chunks, one of which might get allocated.
- Coalescing: combining consecutive contiguous chunks into one chunk.
- One possible implementation - embedded free list:
	- Each page has its own free list. If you wanted to allocate memory, you would need to go through the free list of each page to determine whether or not there is enough contiguous space available.
	- Every 'chunk' (collection of bytes) gets a header containing the size of the chunk and either the next chunk header (free list) or magic number / checksum (allocated list). 
	- How this creates a free list: Head of free list points to first free chunk. Within this chunk, you have a pointer to the next free chunk. The head of the free list would need to be stored somewhere.
	- This means that even if you want to allocate 10 bytes, you would need 18 bytes (4 more for int, 4 more for magic number) of contiguous space.
- Alternate approach: you maintain a cross-table free list, which serves as an external map.
- Pros and cons of header approach v/s external map approach:
	- With headers, a con is that you are increasing the requirement of contiguous space required, when this was already a pain point.
	- With a separate mapping of allocated space, a con is latency. You would need to access a separate page to determine which specific bytes have been allocated, and then work with them (think about how a free call would work to deallocate memory).
---
# Design Problems Discussed
![[IMG_7833.heic]]
- Read up on: 2Q (2 tier cache?)
- Read up on: real time operating systems
- More context on fragmentation:
	- Fragmentation within a node of a free list - internal.
	- Across nodes - external.
	- NEED MORE CLARITY ON THIS.
- Memory allocation strategies:
	- Best, worst, first fit.
	- Best: closest empty space available to fit required data.
	- Worst: biggest space available.
		- Advantage: remaining space after allocation can be used to fit something else.
		- Disadvantage: taking away largest chunk which would otherwise have been useful for a larger element.
	- First: self explanatory
- RTOS memory design options:
	- Multiple queues: one for latency sensitive elements, another for non-sensitive ones, with some sort of hint to the OS (this does not need to be per page; can instead be per process).
	- Larger pages to make page table walks faster.
	- Increase size of working set.
- Working set: for each process, a fixed number of pages NEED to be in RAM. 
- Computing access time in case of page fault:
	- 1 TLB time for search
	- 1 memory access time to check full PT (assuming TLB MISS; there IS a possibility of TLB hit even for block addresses, in which case you wouldn't need the memory access time)
	- 1 disk access time to actually get the page from disk
	- 1 memory access time to update PTE (assuming no parallel updation)
	- 1 TLB time to update TLB (assuming no parallel updation)
	- In case of parallel updation, these two above can be done while disk access is taking place. So, as long as disk access takes longer, even at same order of magnitude these need not contribute to total access time.
	- 1 memory time to now actually read correct location
- Revise: MLFQ
- Only problem with zombie processes: PID still present, you run out of PIDs.
	- Read up more on zombies; this is still unclear.
---
# Questions
### General
- Virtualisation is an expensive endeavour. What then is the purpose of virtualising memory? If every process can't actually have all the memory, why tell the processes that memory is completely independent?
- Does virtualisation imply that even non-contiguous addresses can be referred to in a contiguous manner?
	- Yes. Without this, there might be a situation where non-contiguous chunks of memory were available, but would not be allocated because of their non-contiguous nature. 
	- Also answers the previous question; even in an HPC setting, virtualisation is not bypassed.
- Why is the code-heap-stack order not followed at the physical level, when this arrangement and proximity is beneficial?
- Can reallocation of memory internally take place without virtual address changing? Does it?
### Paging
- Paging just reframes the problem to segment level - you might still have fragmentation across pages.
- Are there any benefits to having page size ≠ frame size.
- Why are variable page sizes not used anymore?
	- Hint: memory manager becomes complex.
- What are the cons of a virtually addressed cache.
### FS
- What is the SSD equivalent of the 'swipe' access pattern, if one exists at all?
	- Ans: Need to lookup, but sequential access in disks IS faster than random access.

