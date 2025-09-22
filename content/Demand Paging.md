---
title: Demand Paging
draft: false
tags:
---
# Swap Spaces
- I have 2 GB of RAM left, but I want to allocate 4 GB (I won't need 4 GB simultaneously as in an LLM).
- I allocate the 2 GB, and keep the other 2 GB in the swap space of the disk - a contiguous stretch of the disk which can be accessed in one swipe.
- The RAM would treat the swap space as virtual memory.
- The swap space could also be divided into blocks, each assigned to different processes. All the swap space does't need to be allocated to the same process.
- The page table would need another bit - the present bit - to indicate whether or not the concerned page is present in the swap space. If the page is NOT present, the table would contain a PHYSICAL address, because the disk is going to be accessed.
---
- Smallest unit of DISK which can be accessed - block.
- Page faults:
	- MMU responsible for flagging these.
	- Reasons for page fault:
		- Valid bit not set.
		- Illegal access, e.g. writing to read-only page.
		- Valid bit set, present bit not set.
- Optimisation for eviction: dirty bit:
	- If a page has not been modified in memory, the dirty bit is 0. 
	- If this is the case, the OS can simply replace this page with something else, allowing it to be replaced. 
	- This is only applicable for pages present both in memory and on disk.
- Kinds of pages:
	- File-backed page: 
		- Part of file stored on disk, therefore present both on disk and in memory.
		- Can be replaced using 'dirty' strategy.
	- Anonymous page:
		- Not backed by any files on disk.
		- If being swapped out, need to go to swap space; cannot rely on dirty method.
		- Anonymous dirty pages: pages whose contents have changed since last read from swap.
- For file-backed dirty pages, when performing a swap, why are changes made to the original disk location, and not swap space, which would result in faster disk access (changes made to original disk location imply a full eviction; the next access of these pages would take a while)?
	- Consistency issues: two versions, one in swap space, one on disk, between which consistency would need to be maintained.
	- Multiple disk access: at some point in the future, these pages would need to be evicted from swap space and written to the original location anyway. In the aforementioned (swap space) paradigm, this would need another disk access to perform this swap. Ultimately, it would just be more efficient to make changes to the original disk location to prevent this.
- When do replacements really occur?
	- Performing RAM-to-swap-space transfers only when the RAM is truly full is very inefficient.
	- Actual systems use thresholding on amount of free space available (refer to low and high watermark).
- Thrashing: repeated page faults due to overuse of memory which results in slowdowns.