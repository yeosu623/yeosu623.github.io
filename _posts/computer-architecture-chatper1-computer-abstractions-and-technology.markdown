---
layout: post
title: "[Computer Architecture]Chapter1. Computer abstractions and technology"
subtitle: "chapter1. computer abstractions and technology"
categories: dev
tags: computerarchitecture
comments: false
---

## Introduction
> Let's explore the comprehensive concepts of computer.

- Contents
	- [What we will see in this category](#what-we-will-see-in-this-category)
	- [Levels of Program Code](#levels-of-program-code)
	- [What is a Computer?](#what-is-a-computer)
	- [Instruction Set Architecture](#instruction-set-architecture)
	- [Performance Metrics](#performance-metrics)
  
## What we will see in this category
---
We will have a long journey for explore the detailed computer operating mechanism and its architecture. We will see these important points later :

- How high-level programs are translated into the machine language.
- The hardware/software interface
- What determines program performance and how much?
- How hardware designers improve performance
- What is parallel processing



## Levels of Program Code
---
Have you made an question about how my source code runs? So, how programming language like C, C++ or Python codes operates on my computer?

You may heard **Compile** term on your very first programming class. Yes, the compile process convert your **High-level language** into **Assembly language** for MIPS(<u>Microprocessor</u> without interlocked pipeline stage). Then, the **Assembler** converts assembly language to **Machine code(Binary Code)** for MIPS.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c4ebf119-c904-4b4a-b644-aab71acd31cc" alt="image" style="zoom:50%;" />



## What is a Computer?
---
Computer has these components :

- processor
- memory (cache as SRAM, main memory as DRAM, disk storage as HDD or SSD)
- input (mouse, keyboard)
- output (display, printer)
- interconnection or network

We will primarily focus on the processor, the cache and memory system.



The processor is the combination of **Datapath** and **Control**. Datapath is the road for data, and control handles data.

Now, let's see how processor works.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7649d1f1-24a5-477d-9978-82e5d0a33617)

1. Input devices put data for memory.

2. Memory fetches(give 1 line of) binary instruction to control, and decode it.

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5c4aac92-6975-418a-a5b5-6419c15d23da)

3. control gives decoded instruction to datapath, and datapath executes the instruction.

4. Next, processor fetches the next instruction from memory.

   So, **Control** decides which is the next instruction and decode it, also gives signals to operate datapath components. **Datapath** executes instructions (e.g. adder) and storage location.

5. After the program completed, the data to be output by binary code.



## Instruction Set Architecture
---
**Instruction Set Architecture(ISA)**, or simple architecture - the **Abstract Interface** <u>between the highest level hardware and the lowest level software</u> that encompasses all the information necessary to write a machine language program, including instructions, registers, memory access, I/O, etc.

The combination of the basic instruction set (the ISA) and the operating system interface is called the Application Binary Interface(ABI).

- ABI = ISA + OS interface.
- ABI is like API in high level langauge between software targets above OS.



Now, let's see the overview of one of the most famous ISA, **The MIPS ISA**.

- Instruction Categories
  - Computational
  - Load/Store
  - Jump and Branch
  - Floating Point (with coprocessor)
  - Memory Management
  - Special
- 3 Instruction Formats : all 32 bits wide.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4bcb1081-a3d0-4c4f-9dc0-e334bfce77f7" alt="image" style="zoom:67%;" />

- ISA is fitted on this place :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/89a47052-c4a8-4700-9c43-19fa230c9129" alt="image" style="zoom:67%;" />



## Performance Metrics
---
How can I choose which computer has the basic performance with low cost? So, in here, we will see what factors in the architecture contribute to overall system performance and the relative importance and cost of these factors.

Basically, there are 4 important factors related on performance. We will see these one by one in detail in future chapters.

- Algorithm : Determines the number of operations executed.

- Programming language, compiler and architecture : Determines the number of machine instructions executed per operation in a certain architecture.
- Operating System : Hardware and software interface. This support program.
- Processor, memory system and I/O system : Determines how-fast, how-many each instruction is executed. Also, determines how fast I/O operations are executed.



Performance is defined as :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/85ed1ba9-f33f-429d-8e9d-fff9a3b37e08" alt="image" style="zoom: 50%;" />

If X is n times faster than Y, then :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/dec843bd-df98-4c0c-a951-586982edf895" alt="image" style="zoom:50%;" />

Simple example : If computer A runs a program in 10 seconds and computer B runs the same program in 15 seconds, how much faster A than B?
Answer : We know that A is n times faster than B if

<img src="C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20230919113907506.png" alt="image-20230919113907506" style="zoom:50%;" />

The performance ratio is 15 / 10 = 1.5, so, <u>A is 1.5 times faster than B.</u>



Execution time is defined as **CPU time** because program elapsed time is device-dependent. CPU time only has the time that CPU spends working on a task, does not include the time waiting for I/O or running other programs.

CPU execution time can be calculated as : 

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/9eca11ee-b473-404f-ac81-066a8155ccbd" alt="image" style="zoom:50%;" />

Simple examples : A program runs on computer A with a 2 GHz clock in 10 seconds. <u>What clock rate must computer B</u> run at to run this program in 6 seconds? Unfortunately, to accomplish this, computer B will require 1.2 times as many clock cycles as computer A to run the program.

Answer :

<img width="375" alt="11" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/45242def-f419-42ee-8faa-5ec80afa7977"  >



(80페이지까지 작성함.)