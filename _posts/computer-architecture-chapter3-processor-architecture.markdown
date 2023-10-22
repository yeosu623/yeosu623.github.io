---
layout: post
title: "[Computer Architecture]Chapter3. Processor Architecture"
subtitle: "processor architecture"
categories: dev
tags: computerarchitecture processor cpu
comments: false
---

## Introduction
> The principle concept for the processor and the CPU.

- Contents
	- [Introduction for article](#introduction-for-article)
	- [Simple Instruction Execution Step](#simple-instruction-execution-step)
	- [Abstract Implementation View](#abstract-implementation-view)
	- [Chapter5](#link-to-chapter5)



## Introduction for article

---

MIPS, the Microprocessor without Interlocked Pipeline Stages, is what we've learn in previous chapter. In this chapter, we will see how MIPS Processor is structured, and how pipeline can be implemented.

We already see that CPU performance has three factors : Instruction Count(IC), CPI(Count Per Instruction), and Clock Cycle Time. In this article, we will examine two MIPS implementations : A simplified version, and a more realistic pipelined version.



## Simple Instruction Execution Step
---
This is saw in chapter2, but we will see this again because it is very important in this chapter.

To execute the single instruction, Processor do : **Fetch, Decode, and Execute, and repeat these three.** During this process, the processor uses **PC(Program Counter)** to access IM(Instruction Memory) and Fetch Instruction. Also, the processor uses **register numbers** for accessing register file with register number<u>(not address)</u> and read registers.

To execute the single instruction in logic-level, the processor use **ALU** to calculate it. It can be used for arithmetic result, get memory address for load/store, get branch target address, etc.



## Abstract Implementation View
---
Below image is the basic architecture of the processor. All parts is already what we saw, so it may be easy to understand.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7f6b1ddb-b540-4f0f-8791-84b2c2578cc3)

As you see, all modules do single cycle operation, that means all modules do its own work independently. And you can see the **Instruction Memory and Data Memory are separated**, so this architecture is called as <u>**Harvard Architecture**</u>. Otherwise, **early processors have that Instruction Memory and Data Memory is combined as the one**, and this architecture is called as <u>**Von Neumann Architecture**</u>.





## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  