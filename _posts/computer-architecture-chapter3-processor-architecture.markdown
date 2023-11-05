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

5. Add the control part.



Continue on page 25...





