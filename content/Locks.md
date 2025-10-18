---
title: Locks
draft: false
tags:
---
- Critical section: part of code which must be accessed by only one thread at a time.
- Fine grained v/s coarse grained locking
	- Advantages of fine grained:
		- More parallelism as independent parts of code don't need to wait for each other.
	- Disadvantages of fine grained:
		- More context switching, resulting in more overhead.
		- Locks would need need to communicate with each other (UNSURE ABOUT THIS INSPITE OF BEING OWN POINT)
- Goals of lock implementation:
	- Mutual exclusion
	- Fairness: every thread should get the lock, and no thread should starve
		- Fairness is also dependent on the user program code; if user code is bad, scheduling might be unfair.
	- Low overhead
---
# Implementations of Locks
### Implementation 1: Interrupt Control
![[Screenshot 2025-10-17 at 9.26.48 AM.png]]
- Does this work - yes; for single core.
- Because interrupts are multi-core, this approach would not work for multi-core multi-threading.
- Hacking the system: never unlock, because no one has the authority to unlock you. User should not be given control of privileged instructions.

### Implementation 2: Spin Wait
![[Screenshot 2025-10-17 at 9.32.47 AM.png]]
- This scenario DOES work ^
![[Screenshot 2025-10-17 at 9.34.54 AM.png]]
- This one DOESN'T. 
	- Issue: mutual exclusion. T1 thinks it has the lock, but in fact T2 has already worked upon the data locked.
	- Both threads think they have the lock.
- Solution: hardware atomic instructions - check and update value in the same instruction - test-and-set instruction.
![[Screenshot 2025-10-17 at 9.47.46 AM.png]]
- Wait UNTIL the locked value has become 0. If it is 1, you 'change' it, but it stays 1. If it becomes 0, you now have control.
- For unlocking: just change isLocked to 0.
- Cons: this wastes CPU cycles.
- Compare and set is SLIGHTLY better than test and set because you are saving on the overhead required to set the value
- This this fair: no. It CAN be fair depending on the scheduler, but because it is scheduler dependent - no.
- Is this compute efficient - no. We are waking up the thread just to run the while loop. The thread could have yielded to the CPU, or even better just have been woken up when the lock was freed (using signals).