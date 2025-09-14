# Questions
- Is there some way to make a child process wait for a parent process to complete certain instructions? Say for example, all children need to wait before the parent has created 3 children.
- Why do we have separate fork() and exec() calls? Why not just have a single forkexec() call? Fork performs a memcopy, to duplicate the parent's code. Exec then replaces all this copied code. So why not directly make the parent copy the executable into a new block?
- What are cons of background processes?
	- What's the difference between multiple cmd ws and a single cmd q on a browser?
- Is pipe a syscall or an executable?
---
# Exec
- A fork will create a child with the exact same code as the parent. It isn't always practical to make the child do exactly what the parent does.
- The exec() system call allows a process to switch to running a different executable.
- It takes another executable as an argument.
- After the passed executable has completed its execution, context is switched *back* to the original process. However, this is to the PARENT, not the child. Any instructions after an exec() call are not going to be executed.
- To read up: what happens if exec is unsuccessful within the child?
- Todo: write code for output redirection ('>').
---
# Process Control
- signal() and signalaction() calls - define what a process does when it receives a kill signal.