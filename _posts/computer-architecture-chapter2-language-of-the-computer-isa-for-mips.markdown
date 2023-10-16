---
layout: post
title: "[Computer Architecture]Chapter2. Language of the Computer, ISA for MIPS"
subtitle: "isa for mips"
categories: dev
tags: computerarchitecture isa mips
comments: false
---

## Introduction
> Let's see one of the ISA(Instruction Set Architecture), the MIPS.

- Contents
	- [Instruction Set](#instruction-set)
	- [MIPS 32 ISA](#mips-32-isa)
	- [MIPS Arithmetic Instructions](#mips-arithmetic-instructions)
	- [MIPS Instruction Fields](#mips-instruction-fields)
	- [MIPS Register File](#mips-register-file)
  - [MIPS Data Types](#mips-data-types)
  - [Dealing with Constants](#dealing-with-constants)
  - [Shift Operations](#shift-operations)
  - [Logical Operation](#logical-operation)
  - [Decision Making](#decision-making)
  - [Compiling While Loops](#compiling-while-loops)
  
## Instruction Set
---
Different computers have different instruction sets. But many aspects in common, so many early and modern computers have simple instruction sets. We will see in detail about one of the instruction set, the MIPS, made on Stanford University.

RISC, Reduced Instruction Set Computer, is now used in modern computers, because this is more efficient on compilers. And this is more simple and have small operations than other instruction sets.

## MIPS 32 ISA
---
Now, let's see in detail about MIPS-32 ISA. This is organized of these instructions:

- Computational
- Load/Store
- Jump and Branch
- Floating Point
- Memory Management
- Special

MIPS-32 ISA has 32-bit register, and has 3 instruction formats. All formats fixed 32-bit wide.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ef19ebcf-3c85-4118-a4e9-54700aa09a71)

This is satisfied on the four design principles :

- Simplicity favors regularity.
  - fixed size instructions.
  - small number of instruction formats.
  - opcode(operation code) is always the first 6 bits.
- Smaller is faster.
  - limited instruction set.
  - limited number of registers in register file.
  - limited number of addressing modes.
- Make the common case fast.
  - arithmetic operands from the register file (NOT from memory), called load-store machine
  - allow instructions to contain immediate operands.
- Good design demands good compromises.
  - limited "three" instruction formats.

## MIPS Arithmetic Instructions
---
This is MIPS assembly language arithmetic statement.

```assembly
add $t0, $s1, $s2
sub $t0, $s1, $s2
```

Each arithmetic instruction performs one operation, and each specifics exactly <u>three</u> operands that are all contained in the datapath's register file. (e.g. $t0, $s1, $s2)

This assembly language code is put on instruction format like this :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/12cde05f-93a1-4271-8932-5a686d59c0c6)

Then, how MIPS can calculate more complex expression like this?

```c
h = (b - c) + d
```

Assuming variable b is stored in register $s1, c is stored in $s2, and d is stored in $s3 and the result is to be left in $s0. Then the assembly code can be formed like this :

```assembly
sub $t0, $s1, $s2
add $s0, $t0, $s3
```



## MIPS Instruction Fields
---
MIPS fields are given names to make them easier to refer to : 

| op     | rs     | rt     | rd     | shamt  | funct  |
| ------ | ------ | ------ | ------ | ------ | ------ |
| 6-bits | 5-bits | 5-bits | 5-bits | 5-bits | 6-bits |

- op : **op**code that specifies the operation
- rs : **r**egister file address of the first **s**ource operand
- rt : **r**egis**t**er file address of the second source operand
- rd : **r**egister file address of the result's **d**estination
- shamt : **sh**ift **am**oun**t** (for shift instructions)
- funct : **funct**ion code augmenting the opcode

Therefore, R-type Instruction format is in total 32-bits.



## MIPS Register File
---
MIPS Register file holds 32-bit register with two read ports and one write port.

<img width="217" alt="20230926_131213" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/052e26b5-2293-453b-8c81-d9af285325a2" style="zoom:150%;" >

Registers' characteristics are :

- Faster than main memory. Note that register files with more location are slower. For example, a 64 word file could be as much as 50%  slower than a 32 word file.
- Easier for a compiler to use register file, compared to stack. For instance, (A x B) - (C x D) - (E x F) can do multiplies in any order in register file, not on stack memory.
- Can hold variables with improved code density. Because register are named using fewer bits than a memory location. In MIPS, 5 bits to locate the position in register file.

Here are the MIPS Register Convention :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1c8ddb21-72d0-4022-859e-5365b6f4faeb)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e2a72f0a-c418-4cb6-84b9-a80c51651765)

But, there are so many variables in running program. How register handle with a lost of variables?

Memory compacted as a large, single-dimensional array. So, an address acts as the index into the memory array.

MIPS has two basic data transfer instructions for accessing memory, `load` and `store`.

```assembly
lw $t0, 4($s3) #load word from memory
sw $t0, 8($s3) #store word to memory
```

Let's see how <u>load</u> instruction works. Consider the load-word and store-word instructions.

For data transfer instructions, MIPS use I-type format.

| op     | rs     | rt     | immediate |
| ------ | ------ | ------ | --------- |
| 6-bits | 5-bits | 5-bits | 16-bits   |

And here are the example for load instruction for `lw $t0, 24($s3)` :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/abd54af1-1c13-4bb1-b7d1-f2680535f20c)

Note that A 16-bit offset means access is limited to memory locations within a range of +2^13-1 to -2^13 (~8,192) words. In other word, +2^15-1 to -2^15 (~32,768) bytes. (1 word = 4 byte in MIPS. Word is a unit for store single data.)

So, that load instruction works like this :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4f067d48-5fc3-4d1f-af51-fd9022baaef8)

Note that the memory address is formed by summing the constant portion of the instruction and the contents of the second (base) register.



Let's see the applied example.

Example 1 : Assuming variable b is stored in $s2 and that the base address of array A is in $s3, what is the MIPS assembly code for the C statement? Assume array A is 4-bytes.

```C
A[8] = A[2] - b
```

Answer :
```assembly
lw  $t0, 8($s3) # 8 means address of A[2]
sub $t0, $t0, $s2 # variable b is stored in $s2
sw  $t0, 32($s3) # 32 means address of A[8]
```

Example 2 : Assuming that the base address of array A is in register $s4, and variable b, c, and i are in $s1, $s2, and $s3, respectively. what is the MIPS assembly code for the C statement? Assume array A is 4-bytes and array A starts on address 0.

```C
c = A[i] - b
```

Answer : 

```assembly
add $t1, $s3, $s3  # array index i is in $s3
add $t1, $t1, $t1  # temp reg $t1 holds 4*i
add $t1, $t1, $s4  # address of A[i] now in $t1
lw  $t0, 0($t1)    # load A[i]
sub $s2, $t0, $s1  # A[i] - b
```



## MIPS DATA TYPES

---

Basically, there are some types to explain the architecture :

- 4 bits is a nibble
- 8 bits is a byte
- 16 bits is a half-word
- 32 bits is a word
- 64 bits is a double-word

MIPS use byte type(8 bits) to store data, use ASCII to decoded to character, and use 2's complement to represent integer.

Also, MIPS aligned data as word type(32 bits).

And, MIPS use **Big Endian** to store data as byte. Big Endian store data from lower address to higher address, and Little Endian store data from higher address to lower address.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0f57d1ca-33dd-4988-ac85-b57b50f2140c)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/bfa3d8c7-068b-4653-ae60-57a43eb44748)

Loading and Storing data as byte in the instruction field, MIPS use I format to operate it.

When a byte(8 bits) get loaded and stored,

- load byte places one byte from memory to the **rightmost 8 bits** of the destination register.

  If other bits remain in the register, **zero-extends** it and loads it into the register. As MIPS use 2's complement, **sign-extends** to remaining bits for minus integer.

- Store byte takes one byte from the **rightmost 8 bits** of a register and writes it to a byte in memory.

  If other bits remain in the memory word, store byte leaves the other bits in the memory word **intact**.(leaving the other bytes in the memory word unchanged)

When a half word(16 bits) get loaded and stored,

- Load byte process is same when a byte get loaded, only difference is 8 bits to 16 bits.
- Store byte is too.



## Dealing with Constants

---

Small constants are used quite frequently in a common programs. May 50% of operands in many common programs.

```C
A = A + 5;
B = B + 1;
C = C - 18;
```

There are some solutions to solve this issue :

1. Put "typical constants" in memory and load them.
2. Create hard-wired registers (like $zero) for constants like 1, 2, 4, 10, ...
3. Include constants inside arithmetic instructions.

What is the best solution? 

1. Load data from memory is slow, so solution 1 is not good.
2. Load data from register is faster than memory. So solution 2 might be good. But...
3. It is the fastest way to operate arithmetic instructions, because instruction has constant so load process isn't needed.

So, MIPS architecture select solution 3 to solve this issue. Therefore, MIPS offer **immediate instructions** for solution 3 :
```assembly
addi $s3, $s3, 4   #$s3 = $s3 + 4
slti $t0, $s2, 15
# "Set less than" command.
# $t0 = 1 if $s2 < 15
```

But, how about larger constants? When there are 32 bit constant to load into a register, we must use two instructions (lui + ori).

- **lui** : "load upper immediate" instruction to store higher order bits.

  ```assembly
  lui $t0, 1111111111111111
  ```

- Then, must get the lower order bits right, use **ori** instruction.

  ```assembly
  ori $t0, $t0, 0000000000000000
  ```

  Finally, we can get 1111111111111111 0000000000000000 within a register.



## Shift Operations

---

There are shamt(shift amount) section in R-type format. What does it?

Shift operation is used for packing and unpacking 8-bit char/number/data into 32-bit words.

- Below is the logical operation commands.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d85b5ae7-f7f4-4d25-ba79-56803809097d)

Note that the empty bit space after shift operation is filled with zero.



- An arithmetic shift(`sra`) maintain the arithmetic correctness of the shifted value. A <u>shifted right</u> one bit should be <u>1/2</u> of tis original value, and a number <u>shifted left</u> should be <u>2 times</u> its original value. 

  `sra` uses the most significant bit (sign bit) as the bit shifted in. There is no need for a `sla`, because `sll` works for arithmetic left shifts.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/098add25-88e7-4698-809e-47dc304719a5)



## Logical Operation

---

- There are a number of **bit-wise** logical operations in the MIPS ISA.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/adaccd73-05f4-47b1-9da5-820c72d79af7)



- AND operation is used to mask bits in a word. 

  It select some bits and clear others to 0 for mask.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8e48db77-c5e0-4e87-810c-e92372936ad5)

- OR operation is used to include bits in a word. 

  It set some bits to 1, leave others unchanged.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b7eebc47-cf64-405d-a3bd-729dce8bdf00)

- NOT operation is sued to invert bits in a word. Also, NOT operation is used to implement NOR. Note that there are NOR operation in MIPS instead of NOT.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ec589471-41e5-4b2b-948b-44a4a374f0ee)



## Decision Making

---

It is alternative of the control flow like if statement.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/28785727-bf8e-4b60-b4af-d4ac9fc7e371)

Note that opposite condition is used in assembly language. if you check equal for some variable, you should bne(branch not equal) keyword to make the decision.



bne/beq uses I format instruction.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4afbf1ae-9312-4582-9b3d-d00369450b04)

offset field is used to various uses,

- Memory address offset for lw & sw
- Immediate constant value(which is contained in instruction itself)
- Branch offset for target (branch distance)

Also, these 3 cases are used for sign extension.



In this case, it is used with the register and add its value with 16-bit offset (branch distance).

The register is named as **Instruction Address Register**(i.e., **PC register**), its use is automatically implied by instruction. PC gets updated (PC+4) during the fetch cycle so that it holds the address of the next instruction.

The branch distance has limit between -2^15 to 2^15+1 instructions (**word, not byte!!**) from the branch instruction. It is made by concatenating two low-order zeros to make it a word address, and then sign-extending with those 18 bits.

However, is it necessary for concatenating two lower order zeros? Why not just store the word offset in the 16 bit immediate field? If two low order zeros does not to be concatenated, would limit the branch distance to -2^13 to 2^13+1, so it is necessary to extend more branch distance size. Also, it doesn't make more complex for its circuit.



From now, we have learned `beq, bne`, but what about other kinds of branches(e.g., branch-if-less-than)? For this, we need another instruction, `slt`.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1df22842-45c5-4f29-9801-d2ac26be0863)

There are alternative versions of `slt`.

- Since constant operands are popular in comparisons, MIPS also has `slti`.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/006c0383-373c-4d7c-a715-acb1b5965d8c)

- We can use `slt, beq, bne` and the fixed value of 0 in register `$zero` to create other conditions. Note that blt, ble, bgt, bge is pseudo-branch instruction, not the real instruction.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b62ae3c2-98bf-47e8-a1f6-176d093e3ef0)

  blt, ble, bgt, bge are not included in the ISA, because its too complicated. It would stretch the clock cycle time or it would take extra clock cycles per instruction.



MIPS also has an **unconditional branch** instruction or **jump** instruction, `j`.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/247bb25d-c02d-4b99-92c2-e3758d106448)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5a908684-bebd-41b7-a50c-5ba4fb299d25)

`j`, jump instruction use J format. How is the jump destination address specified?

1. concatenating 00 as the 2 low-order bits to make it a word address.
2. concatenating the upper 4 bits of the currently updated PC(i.e., PC+4) to 32-bits address.

And, if the branch destination is further away than can be captured within 16 bits in I format, you can solve this by using J format unconditional branch, so branching can be much more far away.

For example,

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/06a686f7-98e1-43c1-bfd5-0528d261897d)



## Compiling While Loops

---



