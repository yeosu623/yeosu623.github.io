---
layout: post
title: "[Microprocessor]Chatper2. Design and Basic operation"
subtitle: "design and basic operation of microprocessor"
categories: dev
tags: microprocessor
comments: false
---

## Introduction
> The basic description of design and basic operation of microprocessor.

- Contents
	- [Pin Description](#pin-description)
	- [Let's connect CPU to Memory](#lets-connect-cpu-to-memory)
	- [CPU Operations](#cpu-operations)
	
## Pin Description
---
Microprocessor has pins to connect for outer circuit to control. Let's see Intel 8088 to see which pins exists.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/fdfe10d0-807a-4943-ba33-2b68bcfbf13a" alt="image" style="zoom:50%;" />

<center><b>Intel 8088</b></center>

It seems to be difficult, but every microprocessor has a core pins :

- VCC : It is used for supply electric energy to microprocessor from outer source.
- GND : Ground Pin.
- A : Address pin. It is used to access instruction.
- D : Data pin.
- Others : to used for control microprocessor.

Intel 8088 has 20 Address pin and 8 Data pin, so it is 1MB microprocessor and 256B memory.



## Let's connect CPU to Memory
---
Before we are really connect CPU to memory, let's see the method of connection.

Nowadays, every computer system store a program to memory to operate it and fast-upload it for a system. This concept is based on "Von Neumann's IAS Architecture", which is made on WWII.

IAS operation do Stored Program Concept, so it can store program that you'll use to memory fast. Its process has boot, booting, and bootstrap, then can be load and stored program.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/9c404e6d-d5fe-4c3b-a04a-09558ff58349" alt="image" style="zoom: 67%;" />

- PC(Program Counter) : Start on 0, so it is started on address 0. and it is increased by one when a single instruction is executed.
- IR(Instruction Register) : Convert instruction to binary code to control circuits.
- MBR(Memory Buffer Register) : Get data from memory to operate it or for external hardware.

To read and write data from memory, you need to connect WE(Write Enable) pin or OE(Output Enable) pin to control memory.

Insturctions are operated sequencely. It has two part of binary code : Opcode(Operation code) and Operand.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/09dc4779-2b7c-4987-bf64-42a19403b0aa" alt="image" style="zoom:67%;" />

Opcode is literally the operator, and operand are data for operator. It is decoded on IR(Insturction Register) and give signal to Control circuits.

Plus, Compile do Program made high-level language(e.g. C, JAVA, etc) to Binary Code. The size of instruction is depend on your computer system.



## CPU Operations
---
CPU Operations is generally divided into 4 part :

- Fetch : Read a instruction from memory and store to IR. Then Increase PC(Program Counter) by one to be ready for get another instruction from next memory.
- Decode : Decode instruction from IR and make control signal.
- Execute : Run decoded instruction to calculate, store, read, etc. The result wil be saved on ACC(Accumulator).
- Write Back : Get results from ACC to store data for memory or register.

Once this cycle has completed, the next fetch begins and continue on. This cycles runs infinitely until the computer is turned off.