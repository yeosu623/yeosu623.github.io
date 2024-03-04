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



Now, let's see how the performance can be calculated.

- Performance is defined as :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/85ed1ba9-f33f-429d-8e9d-fff9a3b37e08" alt="image" style="zoom: 50%;" />

If X is n times faster than Y, then :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/dec843bd-df98-4c0c-a951-586982edf895" alt="image" style="zoom:50%;" />

Simple example : If computer A runs a program in 10 seconds and computer B runs the same program in 15 seconds, how much faster A than B?
Answer : We know that A is n times faster than B if

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1b8ee83c-0f8f-4018-a4fc-c77b40a6c326" alt="image-20230919113907506" style="zoom:50%;" />

The performance ratio is 15 / 10 = 1.5, so, <u>A is 1.5 times faster than B.</u>



- Execution time is defined as **CPU time** because program elapsed time is device-dependent. CPU time only has the time that CPU spends working on a task, does not include the time waiting for I/O or running other programs.

CPU execution time can be calculated as : 

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/9eca11ee-b473-404f-ac81-066a8155ccbd" alt="image" style="zoom:50%;" />

Simple examples : A program runs on computer A with a 2 GHz clock in 10 seconds. <u>What clock rate must computer B</u> run at to run this program in 6 seconds? Unfortunately, to accomplish this, computer B will require 1.2 times as many clock cycles as computer A to run the program.

Answer :

<img width="375" alt="11" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/45242def-f419-42ee-8faa-5ec80afa7977"  >



- CPU clock cycles can be defined as the average time of taking times of instruction. Different instructions take different amount of execution time. For example, integer add takes 1clock, integer multiply takes 5clock, and float multiply takes 20clock time. So, CPU clock cycles must be calculated as average time of execution time.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/2a4c3a61-9375-4a98-b5c5-bda71c0431ea)

- Clock cycles Per Instruction(CPI) is the average number of clock cycles each instruction takes to execute. To measure CPI,  compare two different implementations on the same ISA.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c46a5235-56e1-4d87-8011-946e7c37bf53" alt="image" style="zoom:67%;" />

Simple example : Computers A and B implemented on the same ISA. Computer A has a clock cycle time of 250ps and an average CPI of 2.0 for some program, and computer B has a clock cycle time of 500ps and an average CPI of 1.2 for the same program. Which computer is faster and by how much?

Answer : 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6e84aca1-dc46-4986-ba84-4db3600186cd)

<img width="423" alt="dd" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/df59684e-d5fe-4114-b398-af37de813b16">

- So, CPU clock cycles can be calculated as

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6758a73f-f9a9-476e-bf17-0c8cf56d583d)

- And average CPI can be calculated as

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b222e814-8e9d-4521-a0a3-8157c74e645b)

Simple example : One program is alternatively compiled, result n two sequences of different code, using instructions in classes A, B, C. Calculate Average CPI on sequence 1 and sequence 2.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/735ab996-b4d3-4a99-a830-0bd6c29154b7)

Answer : 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/9029c916-daa3-420a-84c6-acbe54524d97)

- Finally, the basic performance of CPU equation is then

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/95702a24-96d2-415e-96e2-86af1292d4f4)

These equations separate the <u>three key</u> factors that affect performance.

- Can measure the CPU execution time by running the program
- The <u>clock rate</u> is usually given.
- Can measure overall <u>instruction count</u> by using profilers/simulators without knowing all of the implementation details.
- <u>CPU</u> varies by instruction type.

Plus, let me introduce some parts of program affect on these factors : 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e036a8ae-8c83-4c8e-9e23-9c34562e7792)

Simple example : There are some operators with some measurements. Answer these questions.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5a6419a2-65a6-4d11-ae57-4a435e146677)

1. How much faster would the machine be if a better data cache reduced the average load time to 2 cycles?

   Answer : CPU time new = IC x CPI(1.6) x CC. so 2.2/1.6 means 37.5% faster.

2. How does time compare with using branch prediction to save a cycle off the branch time?

   Answer : CPU time new = IC x CPI(2.0) x CC. so 2.2/2.0 means 10% faster.

3. What if two ALU instructions could be executed at once?
   Answer : CPU time new = IC x CPI(1.95) x CC. so 2.2/1.95 means 12.8% faster.



