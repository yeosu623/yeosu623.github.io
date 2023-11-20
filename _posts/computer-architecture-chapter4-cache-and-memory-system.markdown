---
layout: post
title: "[Computer Architecture]Chapter4. Cache and Memory System"
subtitle: "cache and memory system"
categories: dev
tags: computerarchitecture cache memory
comments: false
---

## Introduction
> Explore memory hierarchy - Cache & Memory System.

- Contents
	- [Types of Memory](#types-of-memory)
	- [Memory Hierarchy](#memory-hierarchy)
	- [Chapter3](#link-to-chapter3)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## Types of Memory
---
There are two types of memory : volatile, non-volatile.

- Volatile : Random Access Memory (RAM). It's access time is the same for all locations.
  - DRAM : Dynamic Random Access Memory.
    - High Density (1 transistor cell), low power, cheap, slow
    - Dynamic means that it is needed to be "refreshed" regularly (every 4~8 ms).
  - SRAM : Static Random Access Memory.
    - Low density (6 transistor cells), high power, expensive, **fast**
    - Static means that it's content will last forever, until power turned off.
- Non-volatile : Random Flashes (SSD, EEPROM). It's access time varies from location to location and from time to time. (HDD Disk, CD-ROM).
  - Read is faster than erase/write, and finite number of erase cycles.



Let's see these memories one by one.

### Disk Storage(HDD)

It is non-volatile, rotating magnetic storage.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/172fbdec-2cf6-4077-b70e-19eb586ac30e)

Each sectors records sector ID, constant size of data(different sizse of each sector), and Error correctiong code(ECC. Used to hide defects or errors).

Access to a sector involves following overhead :

- Queuing delay(scheduling delay), if other accesses are pending
- Seeck : move the heads
- Rotational latency
- Data transfer
- Plus, Any necessary controller overhead



### Flash Storage(SSD, Solid-State Drive)

It is a non-volatile semiconductor storage. It is 100x ~ 1000x faster than disk, and it is smaller, lower power required, and moer robust. But it is more expensive than HDD and DRAM.

It can be made by two types:

- NOR flash : bit cell like a NOR gate
  - High speed memory
  - Random read/write access
  - Read/Write level : BYTE(like a DRAM)
  - Used for instruction memory in embedded systems or firmware storage
- NAND flash : bit cell like a NAND gate
  - High density memory & cheaper per GB
  - Random read/write access
  - Read/Write level : PAGE (vs. Erase level : BLOCK)
  - Used for data storage(USB memory, media storage, etc.)

Flash memory has lots of characteristic :

- Flash bits wears out after 1000's of accesses
  - Life time is usually 10,000 ~ 100,000
  - Not suitable for direct RAM or disk storage
  - **Wear leveling** : remap data to less used blocks
- Operation time of NAND flash memory : Asymmetric
  - Read : 20us, Write : 200us, Erase : 1.5,s
  - NOR flash is faster but it also has asymmetric operation time
- Two types of NAND Flash (Page vs Block)
  - Small block NAND Flash : 528byte (512byte page + 16byte spare area) * 32 = 1 block.
  - Large block NAND Flash : 2112byte (2048bype page + 64byte spare are) * 64 = 1 block.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/06538593-dc70-4cd5-820f-8cc3606df4f2)

By the way, what is **Wear Leveling** in SSD? It is the limited number of erase operations. Wear out starts from 1,000 or so, and lifetime is about 10,000 ~ 100,000.

Maintains a wear leveling table, which contains the number of erases for each block. It has 3 types of Wear Level Policies in SSD.

- Static Wear Leveling : Check all area including User data Blocks and free blocks. It doesn't includes OS area.
- Dynamic Wear Leveling(Garbage Collection) : Check among "free blocks only". Choose minimun wear level block among free blocks. Note that source block is selected by Garbage Collection.
- Global Wear Leveling : Wear Leveling among Bank level or Die level. It includes OS area.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/05a01d0a-3094-4832-94e0-b32f105f1c60)

Another notable characteristic of SSD is **Erase-before-write**. In initial state of SSD, it can be written any 1/0 values to SSD cell. Once written, you can change 1->0, but can not change 0->1. So, we have to erase first before write new value. Erase operation makes all cells to 1 again (0xFFFF). So, we say program operation, not erase operation in SSD. Therefore, overwrite is impossible, instead erase and write.

But, it makes too much overhead, because this method erase all pages in the whole block for one page write. So, the new method has come : **Out-place-Update**. This method is mark the page which has an old value as invalid and write a new value in a free page.

<img width="308" alt="1" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/14765756-aebd-46df-830c-f80311e60bcd" style="zoom:150%;" >

When there are no free page during Out-place-Update, SSD do Garbage Collection.

It does that migrate valid pages to a free block, and then earse the block and make the block free.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0e90590e-d254-412c-9b80-a2368f6b6892" alt="image" style="zoom:80%;" />

Garbage Collection Policies in SSD is this. Select minimum write overhead(migration cost) block. In other words, select the block which contains the most invalid pages.

<img width="318" alt="2" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8f2744d0-af5d-4161-9ac3-5ba9d4232d86" style="zoom:150%;" >

Or, select a block which results in maximum free pages among all blocks for garbage collection.

<img width="316" alt="3" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a60b19ee-de00-4a76-885b-1d20bf19b5ce" style="zoom:150%;" >

Another way to choose GC candidate is considering page access patterns(temporal locality). There are two types of page : hot page(frequency access) and cold page(infrequent access). If we select a hot paged block for garbage collection candidate, overall system performance could be downgraded. So we need to select a cold paged block for garbage collection candidate, and we can choose either a cold page count or a cold page ratio. We can choose either by simulating these.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a362dcb6-8a3b-4ad4-a173-c25c3322e80a" alt="image" style="zoom:80%;" />

By the way, how SSD maps its address? As we saw above, Address mapping in SSD has to translate corresponding block and page, cascadingly.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/90eecc80-3ee1-487f-9921-060101ff9f33)

So, how to use and manage the flash memory as a new storage system by Operating System, compared to traditional storages(HDD), concerning these unique feature of Flash Memory?

We can think for that problem. Option 1 is that use file systems for flash memroy, like YAFFS, FJJS, etc. It can be used for light weight software layer for embedded systems.

Option 2 is that use FTL(flash translation layer) to make flash memory as traditional HDD. Then, OS can utilize stabilized file systems above FTL. FGTL is embedded in products as a hardware, so in general, FTL exists in a software layer as a part of OS.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6c5e8fb6-54a8-4a60-b22c-d1d110050318)

Finally, let's see the one cell in SSD. The number of bit that can be stored in each cell : SLC(1 bit), MLC(2 bits,), and TLC(3 bits). As the number of bit is increased, it is increased density naturally, and decreased lifetime, because hard to control voltage level, results in high probability of error occurrence. But as the number of bit is increased, the storage of SSD is increased for same sized chip.



## Memory Hierarchy
---
The general facts that large memories are slow and fast memories are small. To overcome this, we need to implement good hierarchy and parallelism.

There are two major memory performance metrics : **Latency and Bandwidth**.

- Latency : Time to access one word.
  - Access Time : time to take a read (or write) request. Similar to response time, but note that read access time and write access time can be different.
  - Cycle Time : time between successive (read or write) requests. Usually cycle time is longer than access time.
- Bandwidth : How much data can be supplied per time unit. It means that the width of the data channel * the rate at which it can be used.

And before to see the memory hierarchy, let's see the important terminologies : 

- Block (or line) : the minimum unit of information that is present (or not) in a cache.
- Hit Rate : the fraction of memory accesses found in a level of the memory hierarchy.
  - Hit Time : Time to access data for that level, which consists of "Time to determine hit/miss + Time to access the block".
- Miss Rate : the fraction of memory accesses not found in a level of the memory hierarchy. That is "1 - (Hit Rate)".
- Miss Penalty : time to replace a block in that level with the corresponding block from a lower level, which consists of "Time to access the block in the lower level + Time to transmit that block to the level that experienced the miss + Time to insert the block in that level + Time to pass the block to the requestor."

So, there are two types of cache.

- Inclusive Cache : Lower level of cache data is a subset of higher level of cache.

  - Most Intel Processor uses this method.

  - Pros : reduces average cache access time
  - Cons : reduces cache space utilization

- Exclusive Cache : Lower level of cache data is not a subset of higher level of cache.

  - AMD K7 uses this method.

  - Pros : Increases space utilization
  - Cons : Increases average cache access time.

So, how is the hierarchy managed? It depends between them.

- Registers - Cache : Compiler, CPU
- Cache - Main Memory : Cache controller hardware
- Main memory - Disks : Operating System

At first, we will see how Cache - Main Memory communicate each other.

Imagine that inserting data x in a empty space of cache. Think about this questions.

1. How do we find a empty space?
2. How do we know if a data item we want is in the cache?

Early engineers develops a **Direct mapped** method, that means each memory block is mapped to exactly one block in the cache. Therefore, lots of lower level blocks must share blocks in the cache.

Cache uses **index and tag** to directly map address. Index use next 2 low order memory address bits, to determine which cache block (Use modulo operation.). And, the cache use tag to the high order 2 memory address bits to tell if the memory block is in the cache.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ae118fd6-042e-4cee-ae2a-1b74972804e0" alt="image" style="zoom:80%;" />





## Link-to-Chapter3  
---
Chapter3에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  