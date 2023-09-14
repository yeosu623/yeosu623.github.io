---
layout: post
title: "[Computer Architecture]Chapter1. Computer abstractions and technology"
subtitle: "chapter1. computer abstractions and technology"
categories: dev
tags: ca
comments: false
---

## Introduction
> Let's explore the comprehensive concepts of computer.

- Contents
	- [What we will see in this category](#what-we-will-see-in-this-category)
	- [Levels of Program Code](#levels-of-program-code)
	- [What is a Computer?](#what-is-a-computer)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
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



## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  