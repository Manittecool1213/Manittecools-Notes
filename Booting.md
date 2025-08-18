---
title: Booting
draft: false
tags:
---
# Questions
- Why is the hardware check necessarily performed first? Aren't there enough situations which would warrant attempting booting and THEN performing a hardware check. This would allow failing the best chance at functioning.
- Why isn't the MBR hard-coded into firmware?
	- Current answer: There is some extent of dynamism required, which would be impossible with something burnt into memory. The MBR would need knowledge of partition tables, etc. which can be modified. Being stored on the disks allows such information to be modified.
--- 
---
### Firmware
- When you initially start your PC, it will start executing some pre-existing instructions. 
- These instructions are stored on flash memory (ROM), and are referred to as firmware.
- This flash memory CAN be updated; chip no longer needs to be replaced for update.
---
### BIOS
- Expansion: Basic Input/Output System
- First thing it does: performs health check to confirm everything is in working order.
- Test performed: 
	- Power-On Self Test (POST)
	- The test will ping each device controller and expect a response.
	- This is performed even before booting.
---
### UEFI
- Replaced the BIOS.
- Backwards compatible with BIOS.
---
### Master Boot Record (MBR)
- Stores a 512 byte segment representing a predefined position of the disk.
- Why is this needed? The BIOS has no knowledge of the file system. Until the OS is loaded, there needs to be SOMETHING loaded into memory. 
- These loading instructions are located in the MBR. This then loads the boot loader.
- UEFI doesn't need the MBR; uses the GUID Partition Table (GPT) instead, which provides a lot more flexibility.
---
### Bootloader 
- Allows you to finally select which OS (kernel) you want to use.
- After this stage, the OS takes control of the hardware. It is truly the final authority. An OS failure is a complete system failure.
--- 
### Init Process
- First process which loads (with PID = 1). 
- Starts when the computer boots and ends at shutdown.
- Responsible for creating all further processes.
--- 
- Difference between restarting and shutting down and turning on again:
	- Restarting will SKIP POST - no hardware check performed.
	- If any changes have been made on the software level, a restart will suffice. But if changes are made on a hardware level, a shut down is necessary.