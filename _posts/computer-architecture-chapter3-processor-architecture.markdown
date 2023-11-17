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
	- [Clocking Methodologies](#clocking-methodologies)
	- [Datapath and Control for the Processor](#datapath-and-control-for-the-processor)
	- [ALU Control Unit](#alu-control-unit)
	- [Instruction Critical Paths](#instruction-critical-paths)
	- [Pipelining](#pipelining)
	- 



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



## Clocking Methodologies
---
Clocking methodology defines when signals can be read and when they can be written.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3e6c143f-9d01-41e5-8563-c25bb6450611)

The clocking methodology also defines when data in a state element is valid relative to the clock. State element is a memory element, such as a Register.

So, in a typical execution,

- Read contents of state elements
- Send values to combinational logic
- Write results to one or more state elements

This operation is done in one clock cycle.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/555b35a3-1671-4709-b737-19600e22c095)



## Datapath and Control for the Processor

---

Remember the general processor has datapath and control flow, and they have 3 steps to operate one instruction : fetch, decode and execute?

Almost every processor implementation is that at first, use the program counter (PC) to supply the instruction address and **fetch** the instruction from memory, and update the PC (In general, PC = PC + 4). Then, **decode** the instruction and read registers, and finally, **execute** the instruction.

All instructions we saw previously can be divided into 3 parts:

- Memory-reference instructions : lw, sw
- Arithmetic-logical instructions : add, sub, and, or, slt, ...
- Control Flow instructions : beq, j, ...

**Besides j (jump) instruction, all instructions use the ALU after reading the registers.** But, how ALU can be used for arithmetic, memory-reference and control flow? We will see these one by one.

1. Fetching instructions involves : reading an instruction from the instruction memory, and updating the PC value to be the address of the next (sequential) instruction.

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/bc88ed6a-b3ae-4c27-a91f-2fd37a18e379)

   PC is updated every clock cycle, so it does not need an explicit write control signal. Just a clock signal is enough. And, there is no need to use read control signal instruction, because it produces instruction every cycle. Of course, write control signal in register file is necessary, because the instruction's return value needs to be wrote in register.

   

2. Decoding instructions involves two operation.

   - First, sending the fetched instruction's opcode and function field bits to the control unit.

     ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/39a2a52d-d9c0-41e4-be57-c741ac899567)

   - Second, reading two values from the register file. they are Rs and Rt value, and the addresses of register file are contained in the instruction itself.

     For example in MIPS ISA, there are R format operations (add, sub, slt, and, or) and the format is this:

     ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/da6d9de3-f215-45d6-b0bb-7acc242022d2)

     Using this format, perform operation (op and funct) on values in rs and rt. Then store the result back into the register file (into location rd).

     ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1e12e10b-90bc-4b91-9587-613fe2dcc1c6)

     Note that register file is not written every cycle, so we need an explicit write control signal, RegWrite, for the register file.

     

3. Executing Load and Store Operations involves : compute memory address by adding the base register (read from the register file during decode) to the 16-bit signed-extended offset field in the instruction.

   Store value : Read from the register file during decode, written to the data memory.

   Load value : Read from the data memory, written to the register file.

   <img width="351" alt="load and store" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/402bf1e1-349a-4399-be6e-3ee0fe2f06a4" style="zoom:150%;" >

   For example, Branch operation have to

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/47affa8f-2ef7-48ae-9ead-35d5eaed61d3)

   To execute it, at first, compare the operands read from the register file during decode(rs and rt values) for equality (zero ALU output).
   
   second, compute the branch target address by adding the updated PC to the sign extended 16-bit offset field in the instruction.
   
   Plus, base register means the updated PC, and offset value in the low oder 16 bits of the instruction must be sifted left 2 bits to turn it into a word address and sign extended to create a 32-bit signed value..
   
   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/fecb8bf4-3987-4be2-a264-9c542166fc1a)
   
   By the way, how the jump operation work? It replace the lower 28 bits of the PC with the lower 26 bits of the fetched instruction shifted left by 2 bits (word offset), and concatenate with upper 4 bit in PC.
   
   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7b8efc78-e591-4950-bc90-8f6db17bd55b)
   
   <img width="378" alt="jump" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b946e6c8-8e48-4a76-a63b-74eb42d984f6" style="zoom:150%;" >

Until now, we saw how the single operation work in the circuit, and it's time to see how the datapath and control work. We will assemble the datapath segments and add control lines and multiplexor as needed.

Consider the single cycle design - fetch, decode, and execute each instructions in one clock cycle. When merged...

- Datapath resource cannot be used more than once per instruction, so some must be duplicated.
- Multiplexors needed at the input of shared elements with control lines to do the selection.
- Clock distribution to each module is also needed.
- Write control signals is necessary to control writing to the register file and data memory within single long cycle time.
- Cycle time is determined by length of this total path.

After see above consideration, we will see how the circuit can be implemented step by step.

1. Consider instruction memory, register file, ALU, and data memory. 

   Red circle means register value in R-type or immediate value in I type,

   and Blue circle means ALU result in R-type or LD to register in I-type.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/581a4262-58aa-4fdb-99ec-628a34dee1e6)

2. Add Multiplexor.

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b7efd893-0422-4f0e-8f62-5919f390b08e)

3. Add Multiplexor for Branch Portion.

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a6240a80-e1d6-47cd-9cc9-0899d6af67f7)

4. Consider clock distribution.

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1dce4eaf-606b-4657-af96-5ac4d8156cc0)

5. Add the control part. This selects the operations to perform (ALU, Register File and Memory read/write operation. etc...), and control the flow of data (by multiplexor inputs).

   ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/cc3f9cf8-c7b2-4eff-9064-64ad020995e7)

   To observe the formats,

   - op field always bits 31-26
   - Address of registers to be read are always specified by the rs field(bits 25-21) and rt field(bits 20-16) in R-type. For Load, read rs(memory) and write to rt. And for Store, read rt and write to rs(memory).
   - Address of register to be written is in one of two places - in rd(bits 15-11) for R-type instructions, in rt(bits 20-16) for lw.
   - offset for BEQ, Load, Store always in bits 15-0.

   Apply these format, the circuit has some implementation. This is almost complete single cycle datapath circuit.

   <img width="404" alt="control" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/170e9170-35af-4235-b764-e0b3f3100acd" style="zoom:150%;" >

   And this circuit is single cycle datapath with control unit.

   <img width="406" alt="control2" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/2e79de2f-44b9-4647-8a01-8b28c52ceeb0" style="zoom:150%;" >

   Finally, this circuit is complete datapath with ALU control unit.

   <img width="406" alt="complete" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6924e927-2c7a-4a81-a144-4ca972c6cc46" style="zoom:150%;" >





## ALU Control Unit

---

Let's explore ALU Control in detail.

Controlling the ALU uses of multiple decoding levels. Main control unit generates the ALUOp bits (2bits) to ALU control, Therefore input 6 bit funct field and 2 bit ALUOp to get result of 4 bits ALUcontrol to ALU.

<img width="372" alt="ALU" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1f2ade68-60d9-4177-b56b-2738388712be" style="zoom:150%;" >

Change it to ALU Control Truth Table to make ALU Control logic.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/567c82f5-2632-44d8-ad3b-7d1c43266aa9)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5470ea71-94eb-4489-a707-67241266e791)



## Instruction Critical Paths

---

Before we see the pipelining instructions, let's see how the instruction can be divided.

Generally, calculate cycle time takes 

- Instruction and Data Memory : 4ns
- ALU and adders : 2ns
- Register File access(reads or writes) : 1ns
- Ignore negligible delays(muxes, control unit, sign extend, PC access, sift left 2, wires)

Consider these aspects, general instruction takes :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/da6d52e1-ea79-44e8-a125-10f0c3d2298c)

As we can see, each instructions have different times because they have their path for each. So if we want to operate them at the same time, the standard will be 12ns. But is it ideal?

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ffcc2707-b25e-4560-b170-b05c7953b29d)

In the single cycle implementation, the cycle time is set to the longest instruction. In above example, load instruction is the longest.

Since the cycle time has to be long enough for the load instruction, it is too long for other instructions, so the last part of the cycle here is **wasted**.



So, how can we make it faster? What if it starts fetching and executing the next instruction before the current one has completed? This named as **pipelining**, and most of all modern processors are pipelined for performance.

CPU time is (Clock Per Instruction) x **(Clock Cycle Time) ** x (Instruction Count), and pipelining can reduce CC, the clock cycle time.

Under ideal conditions and with a large number of instructions, the speedup from pipelining is approximately equal to the number of pipelined stages. For example, a five stage pipeline is nearly five times faster because the CC is nearly five times faster(cc is 1/n, n is #(pipeline stages)). So, if the pipeline length is reduced to 1/n, then speedup is n times.

Another way to make processor faster is **Superscalar processing**. This means make multiple operating way for instructions. We will see this method later in this chapter.



## Pipelining

---

To pipeline instruction, we need to know what we will do to. There are five stage of Load instruction :

- IFetch : Instruction Fetch and Update PC
- Dec : Instruction Decode and Registers Fetch
- Exec : Execute R-type, calculate memory address
- Mem : Read/Write the data from/to the Data Memory
- WB : Write the result data into the register file.

After pipeline the processor, the instructions is executed like below :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/247b91a1-4cdd-4eb0-ae4a-808cb8995628)

A good point for applying pipeline is improves through put, so total amount of work done in a given time. But, instruction latency is not reduced, because latency is execution time from the start of an instruction to its completion.



So, what makes it easy in our MIPS architecture to make a pipelined processor?

Because MIPS composed as RICS features, such as...

- all instructions are the same length (32 bits)
- few instruction formats (three) with regularity across formats.
- memory operations occur only in loads and stores
- each instruction writes at most one result
- operands must be aligned in memory so a single data transfer takes only one data memory access.

And, below is the figure of MIPS datapath with each operation marked.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4e7d2448-da5e-4e52-b796-f2f2a23a490c)

We can see that state registers are inserted between the state(bar in the diagram), and the system clock is triggered to every sequential module as well as newly inserted stage register, except IM.

PC can be thought of as a pipeline register,

- the one that feeds IF stage of the pipeline.
- Unlike all of the other pipeline registers, the PC is part of the visible architecture state. So, PC is included in programmer's model.



And next, let's see now addition operations executed with state register.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c47e89c3-4152-45d0-b884-2b7de0ee62c7)

We can see that any information that is needed in a later pipe stage must be passed to that stage via a pipeline register. Register address(colored as GREEN) should continuously passed through the pipeline and feed back again.

And, the only two data flows from right to left(color as PURPLE). Loaded data from DM to RF, and then select of the next value of PC, one input comes from the calculated branch address from the MEM stage.

Later instructions in the pipeline can be influenced by these two reverse data movement. The first one(WB to ID stage for LD instruction) leads to **data hazards**, and the second one(MEM to IF for branch instruction) leads to **control hazards**. Because of these reverse movements, **HAZARDs** happen!! We will see these detail later.

