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
- Prefetching - spacial locality - swapping *in* memory locations close to one which was requested, to reduce access time in the even that it *does* get used. The philosophy of this paradigm is that the likelihood of this access pattern is high.
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

