---
layout: post
title: "[Operating System]Chatper1. Introduction"
subtitle: "chapter1. introduction"
categories: dev
tags: operatingsystem
comments: false
---

## Introduction
> The introduction of operating system.

- Contents
	- [What is an Operating System?](#what-is-an-operating-system)
	- [How a computer starts?](#how-a-computer-starts)
	- [Computer System Organization](#computer-system-organization)
	- [Interrupt](#interrupt)
	- [Storages on a Computer](#storages-on-a-computer)
	- [Operating System Structure](#operating-system-structure)
	- [Process Management](#process-management)
	- [Memory Management](#memory-management)
	
## What is an Operating System?
---
This is a program that acts as an intermediary between a user of a computer and the computer hardware. The goal is for two : Common user's perspective, which means that executing user programs and making solving user problems easier, and System's perspective, which means resource manager and control program. These shorts into two words : **Convenience**, make the computer system convenient to use, and **Efficiency**, use the computer hardware in an efficient manner.

Back to the main point, OS uses for

- OS is a **resource allocator**.

  - Manages all (physical and abstracted) resources.

  - Physical Resource : CPU, Memory, HDD, Terminal, Network, etc.
  - Abstracted Resource : Task, segment/page, file system, terminal driver, communication protocol, etc.
  - OS decides between conflicting requests for efficient and fair resource use.

- OS is a **control program** : Controls execution of programs to prevent errors and improper sue of the computer.

- No universally accepted definition.

- The one program running at all times on the computer is the **kernel**.

  - Everything else is either a system program (ships with the operating system) or an application program.

In this class, we will see how design and implement operating system.

- Design and Implementation of OS is not "solvable", but some approaches have proven "successful".
- Internal structure of different Operating Systems can vary widely.
- Start by defining goals and specifications.
- Affected by the choice of hardware, type of system.
- User goals and System goals
  - User goals : Operating System should be convenient to use, easy to learn, reliable, safe, and fast
  - System goals : Operating System should be easy to design, implement, and maintain, as well as efficient, flexible, reliable, and error-free.
- Important principle to separate : **Policy** and **Mechanism**.
  - Policy : What will be done?
  - Mechanism : How to do it?
- Mechanisms determine how to do something, policies decide what will be done.
  - The separation of policy from mechanism is a very important principle, it allows maximum **flexibility**.
  - Policy is likely to change across places or over time.
  - A general mechanism insensitive to changes in policy would be more desirable.
- Example : CPU timer construction
  - Policy : How long is the timer to be set?
  - Mechanism : Detailed various timer construction methods.
- Example : Priority Management
  - Policy : Priority level decision
  - Mechanism : Detailed Control method for handling priority



## How a Computer Starts?

---

Now, let's see how a computer start-up.

- **Bootstrap program**, (or **Bootstrap loader**) is loaded at power-up or reboot.
  - Typically stored in ROM or EEPROM, generally known as **firmware**.
  - Initializes all aspects of system, from CPU registers to device controllers.
  - Must know how to load operating system kernel and starts execution.
  - Some computer systems, such as PCs, use **two step** process.
    - Simple bootstrap loader in BIOS ROM fetches a more complex boot program in boot sector from disk, which in turn loads the kernel.
    - followed on BIOS -> boot sector -> OS location.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7954b263-8d02-4841-87e3-d7ee69bf7402)



## Computer System Organization

---

In Computer System Organization,

- One or more CPUs, device controllers are connected through **common bus** providing access to shared memory.
- Concurrent execution of CPUs and devices are competing for memory cycles.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/24e322e2-d85e-4183-9e69-66fbbeb4c18b)

- General Operation : 
  - CPU and I/O devices can execute concurrently.
  - CPU moves data from/to main memory to/from local buffers.
  - I/O moves data from the device to local buffer of controller. 
  - Device Controller
    - Each device controller is in charge of a particular device type. 
    - Each device controller has usually a local buffer.
    - Device controller informs CPU that it has finished its operation by causing in **interrupt**.



## Interrupt

---

By the way, what is an interrupt?

- Interrupt transfers control to the *interrupt service routine* generally, through the *interrupt vector*, which contains the addresses of all the *service routines*.
- Interrupt architecture must save the address of the interrupted instruction.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0e49a9e5-dfbe-4ab6-a3bf-7ea224fef3c9)

- Incoming interrupts are disabled while another interrupt is being processed to prevent a lost interrupt.
- A **trap** is a software-generated interrupt caused either by an error or a user request. This interrupt is generated by hardware, similar to Exception Handling, for example, divide by zero, segmentation/page fault, system call, etc.
- An operating system is interrupt driven.

An interrupt has two types :

- External interrupt : asynchronous, generated by external hardware device.
- Internal interrupt
  - Fault : save current instruction -> ISR -> return to faulted instruction.
    - ex) page fault, memory space fault
  - Trap : save current instruction -> ISR -> return to next instruction of trapped instruction.
    - ex) system call, exception handling
  - Abort : ISR -> just abort current task because it is critical.
    - ex) divide by zero

So, how handle interrupts?

- The operating system preserves the state of the CPU by storing registers and the program counter.
- Determines which types of interrupt has occurred:
  - **Vectored interrupt** system, which we saw earlier.
  - **Polling system**, contrary of interrupt system. It determines state of device through handshaking, busy waiting.
    - Pros : fast response, no context switching overhead.
    - Cons : waste of CPU cycle.
    - Requirement : fast I/O device, shorter I/O routine, and should happen rarely.
- Dedicated code segments determine what action should be taken for each type of interrupt -> called Interrupt Service (Handling) Routine, ISR.



## Storages on a Computer

---

And then, let's see what storages is composed on a computer.

- Main Memory : Large storage media that the CPU can access directly.
- Secondary storage : extension of main memory that provides large nonvolatile storage capacity.
- Magnetic disks - rigid metal or glass platters covered with magnetic recording material.
  - Disk surface is logically divided into tracks, which are subdivided into sectors. The disk controller determines the logical interaction between the device and the computer.
- Electronics disks - flash memory.

Storage systems organized in hierarchy. That considered with speed, cost, size, and volatility.

Also, storage system has its cache - copying information into faster storage system. Main memory can be viewed as a last cache for secondary storage.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c6b27e70-2773-4e78-adc3-abe5eded0c45)



## Operating System Structure

---

OS use **multi-programming** for efficiency.

- Single user cannot keep CPU and I/O devices busy at all times.
- Multi-programming organizes jobs (code and data), so CPU always has one to execute.
- A subset (rest) of total jobs in system is kept in memory.
- One job is selected and run via **job scheduling**.
- When it has to wait (for example, I/O completion), OS switches to another job.
- **Timesharing (Multitasking)** is logical extension in which CPU switches jobs, so frequently that users can interact with each job while it is running.
  - **Interactive System**
    - **Response time** should be short, typically less than 1 second.
  - **Process** : Each user has at least one program executing in memory
  - **CPU scheduling** : If several jobs ready at the same time
  - **Swapping** : If processes don't fit in memory, moves them in and out to run.



## Process Management

---

- A process is a program in execution. It is a unit of work within the system. Program is a **passive entity**, process is an **active entity**.
  - One copy of program and several copies of process.
- Process needs resources to accomplish its task.
  - CPU, memory, I/O, files, initialization data. 
- Process termination requires (total) reclaim of any reusable resources.
- Typically system has many processes, some operating system is running parallelly on one or more CPUs.
  - Parallelism by multiplexing the CPUs among the processes.

The operating system is responsible for the following activities in connection with process management :

- Creating and deleting both user and system processes
- Suspending and resuming processes
- Providing mechanisms for process synchronization
- Providing mechanisms for process communication
- Providing mechanisms for deadlock handling.



## Memory Management

---

Finally, let's see how OS manage memory.

- All **data** in memory before and after processing.
- All instructions in memory in order to execute.
- Memory management activities
  - Keeping track of which parts of memory are currently being used and by whom.
  - Deciding which processes (or parts thereof) and data to move into and out of memory.
  - Allocating and deallocating memory space as needed.
- OS provides uniform, logical view of information storage.
  - **File** : Abstracts physical properties to logical storage unit 
  - Each medium is controlled by device driver (disk drive, tape drive, etc.) They have varying properties : access speed, capacity, data-transfer rate, access method (sequential or random).
- File-System management do:
  - Files usually organized into directories.
  - Access control on most systems to determine who can access what.
  - OS activities include (in terms of file systems)
    - Creating and deleting files and directories
    - Primitives to manipulate files and directories
    - Mapping files onto secondary storage
    - Back-up files onto stable (non-volatile) storage media



