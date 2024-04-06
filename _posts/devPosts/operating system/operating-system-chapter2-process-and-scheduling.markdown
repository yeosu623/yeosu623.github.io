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
	- [Context Switch](#context-switch)
	- [Process Creation](#process-creation)
	- (page ? ~ 74 did not wrote. Need to write them.)
	- [First come First served Scheduling](#first-come-first-served-scheduling)
	- [Shortest Job First Scheduling](#shortest-job-first-scheduling)
	- [Priority Scheduling](#priority-scheduling)
	- [Round Robin Scheduling](#round-robin-scheduling)
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



## Context Switch

---

When CPU switches to another process, the system must save the state of the old process and load the saved state for the new process.

- System Context : Process data structure allocated by kernel. For example, PCB, Page/Segment Table, File table, etc.
- Hardware Context : Register information such as Program counter, stack pointer, etc.
- Memory Context : Memory space, a out image in disk.

Context-switch time is purely overhead; The system does no useful work while switching. But sometimes this must be used for. Alternate method is 'get a long time slice to execute' to avoid context-switching, but it may take a longer time than that.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/315a3f84-4b43-449c-a08d-da18c537f89f)



## Process Creation

---

Parent process create children processes, which, in turn create other processes, forming a tree of processes. So, resource sharing type in process hierarchy takes one of them below :

- Parent and children share all resources (especially in UNIX).
- Children share subset of parent's resources.
- Parent and child share no resources.

In execution, takes either of them.

- Parent and children execute concurrently.
- Parent waits until children terminate (especially in UNIX).

In address space,

- Child process duplicates parent process address space.
- Child's program is loaded into its duplicated address space.

Below figure is process creation diagram in UNIX environment.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1d9db745-a684-4669-b7f2-83edaa02e86e)

Let's see these commands one by one.

- fork() system call
  - Only way to increase the number of processes.
  - Create a copy of itself - logical copy of parent.
    - Copy a.out image 
    - Copy kernel data structures
  - All environment (in user mode) are inherited.
    - Such as file offset, program counter, etc.
  - Only PID differs, rest identical. Plus these may differs...
    - Lock attribute such as file lock, memory lock
    - Timer information for scheduler is reset for child
  - No sharing of memory.
  - In some systems, vfork() system call is provided. This is same as fork(), except the exclusion of memory space copy.

Simple example : 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a6721e37-d802-4f51-a175-b467e78572cd)

Answer : 

Hello, I am child!

Hello, I am parent!

- exec() system call
  - Retrieve a file from disk. 
  - Overlay on old a.out image.
  - Jump to start location.

Simple example :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/97a4e66b-8967-4773-807d-d0accb994aca)

Answer :

before executing ls -l

0

(Print end, because 'bin/ls' code take replace all main() code.)

- wait() system call
  - If Pa process invokes wait() -> then kernel block Pa.
    - Until child terminates. 
    - When child terminates, kernel wakes up the parent.
    - Kernel puts the parent into ready queue
    - Parent is dispatched later.
  - wait() system call handles 3 return codes of child process.
    - (1)PID, (2)exit status, and (3) the CPU usage.



In summary, fork() can only create same process, but exec() can create different process. And, forking process does not terminated through fork, but execing process terminated through exec (parent process image is over-written). In UNIX, by combining fork and exec, different process can be created without any process termination.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/96569b90-a96c-4dac-80ee-e4e154cf884b)







page ? ~ 74 did not wrote. Need to write it.





## First Come First Served Scheduling

---

First-Come, First-Served (FCFS) Scheduling is implemented with one queue. It is known  as FIFO scheduling, and has the simplest scheme among other scheduling.

- Processes dispatched according to arrival time
- Non-preemption policy : Even IO burst, no more scheduling decision
- Rarely used as primary scheduling algorithm

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/19e3a198-f816-4e38-8e26-a69b4f945d09)

Suppose that the processes arrive in the order: P1, P2, and P3, and its burst time is 24, 3, 3, respectively. The Gantt Chart for the schedule is :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3699b90f-981b-4b3a-8103-66809d597f31)

- Waiting time for P1 = 0, P2 = 24, and P3 = 27
- Average waiting time : (0 + 24 + 27) / 3  = 17

Another example, suppose that the processes arrive in the order : P2, P3, and P1. The Gantt Chart for the schedule is :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/81137097-ca41-465e-bfe1-d5fa69e97903)

- Waiting time for P1 = 6, P2 = 0, and P3 = 3
- Average waiting time : (6 + 0 + 3) / 3 = 3

That is much better than previous case. This is called of **"Convoy effect"**, which means that "short process behind long process". This effect can make a wide variation of average waiting time.



## Shortest Job First Scheduling

---

Shortest-Job-First (SJF) Scheduling offsets the cons of the previous scheduling policy.

This associate with each process length of its next CPU burst, and use these lengths to schedule the process with the shortest time.

This has two variations :

- non-preemptive : once CPU is given to the process, it cannot be preempted until completes its CPU burst.
- preemptive : if a new process arrives with CPU burst length less than remaining time of current executing process, then preempt it. This scheme is known as the Shortest-Remaining-Time-First (SRTF).

Consider this case. What is the average waiting time that using SJF (non-preemptive) scheduling policy?

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0.0          | 7          |
| P2      | 2.0          | 4          |
| P3      | 4.0          | 1          |
| P4      | 5.0          | 4          |

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/32423de5-cd45-4a49-b670-cf6f3806b8ad)

The average waiting time is : (0 + 6 + 3 + 7) / 4 = 4



And, what is the average waiting time that using SJF (preemptive) scheduling policy, with above same case?

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5caa49c8-8e3a-412e-920d-2793fef40c6d)

The average waiting time is : (9 + 1 + 0 + 2) / 4 = 3



This policy seems much better than previous thing. Let's see its pros and cons.

- Pros
  - SJF is optimal : gives minimum average waiting time for a given set of processes.
- Cons
  - Difficult in real world : how do we know next burst of CPU?

To predict burst times, scientists make a thought that exponential average, which means that predicting next CPU burst based on previous CPU bursts with exponential average.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8a9044f9-d428-4d9b-b7ae-90879a936c38)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1faf9cb1-fab4-4c3e-9208-29743be38c75)



## Priority Scheduling

---

A priority number is associated with each process. So, the CPU can be allocated to the process with the highest priority, preemptive or non-preemptive. Also, SJF can be treated as a priority scheduling, where priority is the predicted next CPU burst time.

However, this policy can cause **"Starvation"**, which means that low priority processes may never execute. So, some policy **"Aging"** these process. As time progresses, system increases the priority of the process.

One of the priority scheduling with aging is called as **"Highest Response Ratio Next (HRRN) Scheduling"**.

- Response ratio = (waiting time + required CPU time) / required CPU time
- Waiting time increases response ratio
- The impact of waiting time is different to each required CPU time
  - Same waiting time vs. different required time, with respect to response ratio.
  - Example : (5 + 2) / 2 = 3.5 vs. (5 + 10) / 10 = 1.5

Plus, non-preemptive priority scheduling can cause **"Priority Inversion"**, so average waiting time may increase.



## Round Robin Scheduling

---

Round Robin (RR) Scheduling is based on FIFO. Processes run only for a limited amount of time, called a time slice or time quantum. It is preemptible, and requires the system to maintain several processes in memory.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/86204692-9596-415e-a3d4-8af5bfcf895a)





