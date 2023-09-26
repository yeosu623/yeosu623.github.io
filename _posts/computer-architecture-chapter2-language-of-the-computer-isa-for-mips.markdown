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



(25 페이지까지 함.)