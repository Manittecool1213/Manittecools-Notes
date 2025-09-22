---
title: Paging Basics
draft: false
tags:
  - example-tag
---
- At the core of segmentation: each 'block' can be of variable length depending on application. Alternative approach: use FIXED size segments - pages.
- Drawback with pages - internal fragmentation.
- This then ends up becoming a balancing act to determine page size. Too large leads to too much internal fragmentation, too small leads to too much external.
- Virtual address space - block referred to as page; physical address space - block referred to as frame.
- The process is not made aware of paging; to it, the virtual address space is still contiguous. This division is made solely for the interest of and usage by the OS.
- Page table - contains page to frame mappings.
	- Simplest implementation - array - allows easy access.
	- Part of OS code, i.e., Process Control Block would need a pointer to page table.
- Address translation:
	- Say we have 4 virtual pages allocated to a process, and 8 total physical frames.
	- In this case, addressing 4 virtual pages takes 2 bits, 8 frames need 3 bits.
	- There is a translation performed from the 2 bit page address to the 3 bit frame address. The offset WITHIN the block remains the same.
- The page table needs to have metadata beyond the page-frame mapping to check validity, read/write permission, etc.
- Because the page table needs to maintain a mapping from virtual address (same range for each process, but independent, i.e. each process gets 0 to some value) to a physical address (common and dependent), EACH process's page table takes 4 MB (given 32 bit operating system, 4 kb page size).
- Because page table itself is chunked - need hierarchical paging.