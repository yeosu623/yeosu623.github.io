---
layout: post
title: "[Operating System]Chapter2. Process and Scheduling"
subtitle: "chapter2. Process and Scheduling"
categories: dev
tags: operatingsystem
comments: false
---

## Introduction
> This post gives information that how OS handle process and make schedule.

- Contents
	- [Brief see for the process](#brief-see-for-the-process)
	- [Process Image in Memory](#process-image-in-memory)
	- [Process State](#process-state)
	- [Process Control Block](#process-control-block)
	- [Process Scheduling Queues](#process-scheduling-queues)
	- [Schedulers](#schedulers)
	- 
	
## Brief see for the process
---
An operating system executes a variety of programs, for example, batch system, interactive system (time shared system), etc.

Process is **a program in execution**, and execution includes

- The unit of resource allocation
- The unit of dispatching - thread.
- Process execution progresses in sequential fashion.
- One copy of explorer program vs. several execution instances of explorer.

And process handles

- Program and data section for process image
- Stack and heap section for memory management
- Other meta data.



## Process Image in Memory

---

Process is shown as "PCB in Kernel Space + Process image itself shown as below". In case of kernel mode, entire address spaces are accessible. But in case of user mode, only user address spaces are accessible. For example, In linux kernel, 0~4G is addressable in kernel mode, but 0~3G is addressable in user mode.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c5b648bf-59b1-4b3c-ac99-41d23160b348)

Let's see the each parts of process image.

- Code
  - Program code and literal constant.
- Data
  - Data required for whole program execution.
  - Global variable, static variable,
  - Macro constant, Symbolic constant, or String constant.
- Stack
  - Data required for a certain function
  - Managed by OS (automatic allocation and deallocation)
  - Local variable, argument
- Heap
  - Data required for a certain execution
  - Managed by programmer (cause memory leak)
  - malloc(new) and free(delete).

At least, some parts of data is called *bss (block started by symbol)*, which contains uninitialized global variable or uninitialized static variable.



## Process State

---

State has 5 stage during perform process.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5dbb965f-bc9e-4234-bed7-6914ba1b12f3)

As a process executes, it changes state.

- new : The process is being created.
- running : Instructions are being executed.
- waiting : The process is waiting for some event to occur (I/O operation, Message send/receive handling, etc.).
- ready : The process is waiting to be assigned to a processor.
- terminated : The process has finished execution.



## Process Control Block

---

These informations associated with each process :

- Process state
- Program counter
- CPU registers
- CPU scheduling information
- Memory-management information
- Accounting information
- I/O status information

Process Control Block, PCB, is included in one process with many PCB.

PCB uses for directing files, ordering several processes, handling CPU scheduling, etc.



## Process Scheduling Queues

---

This has 3 types of queues. Processes migrate among the various queues.

- Job queue : set of all processes in the system
  - Processes may reside in disk or main memory
- Ready queue : set of all processes residing in main memory, ready and waiting to execute.
- Device queues : set of processes waiting for an I/O device



## Schedulers

---

Schedulers also has 3 types.

- Long-term scheduler : Job scheduler. Selects which processes should be brought into the ready queue. Ready queue contains all processes which reside in main memory. Also, the long-term scheduler controls the degree of multiprogramming, which means it control the number of processes in memory.
- Short-term scheduler : CPU scheduler. Selects which process should be executed next and allocates CPU.
- **Medium-term scheduler**
  - Why that be made? : sometimes, it can be advantageous to remove processes from memory and thus **reduce the degree of multiprogramming**.

