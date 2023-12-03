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
	- [Cache Field Sizes](#cache-field-sizes)
	- [Handling Cache Hits](#handling-cache-hits)
	- [System Bus between Cache and Memory interface](#system-bus-between-cache-and-memory-interface)
  - [Measuring Cache Performance](#measuring-cache-performance)
  - [Multilevel Cache](#multilevel-cache)
  - 
  
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



## Cache Field Sizes
---
It is the number of bits in a cache includes both the storage for data and for tags(not index!). Total cache size is data storage plus address storage.

In this chapter, we will assume 32-bit address with byte addressing.

For a direct mapped cache, which is composed of 2^n blocks, n bits are used for the index.

For a block size of 2^m words(2^(m+2) bytes), m bits are used to address the word within the block (block offset) and 2 bits are used to address the byte within the word(byte offset). 32 byte block means 3 bits are used to address a word and 2 bits are used to address a byte within the word. So, 32 byte block is 8 words (3 bits) * 4 byte for each word (2 bits).

So, what is the size of the tag field? It can be

`"32 - (n+m+2)"`

`in other words, 32 - index bits - block offset - byte offset.`

And, the total number of bits in a direct-mapped cache is then

`2^n * (block size + tag field size + valid/dirty or any control field)`

`in other words, 2^n * (data size + address size + control size).`



## Handling Cache Hits
---

### Cache hits

Read hits on cache(I cache and D cache, i.e. I$ and D$) is easy, because they have done when we want.

But, Write hits(D cache only) is quite difficult : It can be either 'write through' or 'write back'.

- Write through : require the cache and memory to be consistent.

  It always write the data into both the cache block and the next level in the memory hierarchy. Write run at the speed of the next level in the memory hierarchy - so slow! - or can use a write buffer and stall only if the write buffer is full.

  It can be used for simple hardware, which main memory is always up-to-date.

- Write back : allow cache and memory to be inconsistent.

  It write the data only into the cache block. It do the cache block to the next level in the memory hierarchy when that cache block is evicted.

  It need a dirty bit for each data cache block to tell if it needs to be written back to memory when it is evicted - can also use a write buffer to help write of dirty blocks to lower level memory.

  Write-back cache requires 2 cycles to write into the cache. In a write-back cache, because we cannot overwrite the block (since we may not have a most up-to-date backup copy anywhere), write-back requires two cycles (one to check for a hit, followed by one to actually do the write). If hit, just write. But if miss, replace the block of L1$ (this replaced L1$ line maybe most up-to-date copy and it is not reflected in L2$ yet, so if we just overwrite, then the data of L1$ line will be lost) and write back.

By comparison, a write-through cache can always be done in 1 cycle, assuming there is room in the write buffer. Reading the tag and writing the data in parallel is possible. And although tag doesn't match, it just writes and generates a write miss to fetch the rest of that block from the next level in the hierarchy, but it eventually will be overwritten.



### Cache misses

There are 3 words(3 Cs) in this concept :

- Compulsory (cold start or first reference) : First access to a block. If you are going to run millions of instruction, compulsory misses are insignificant.
  - Solution : increase block size (but, it will increase miss penalty, also very large blocks could increase miss rate).
- Capacity : Cache cannot contain all blocks accessed by the program.
  - Solution : increase cache size (but it may increase access time and cost)
- Conflict (collision) : Multiple memory locations mapped to the same cache location.
  - Solution 1 : increase cache size.
  - Solution 2 : increase associativity (but it may increase access time).

We will consider single word blocks only here.

When read misses in I$ and D$ occurred, these process happened :

- stall the pipeline (stall by cache, not hazard)

- fetch the block from the next level in the memory hierarchy,

- insert it in the cache

  - I$ : just insert (read only cache)
  - D$ : have to consider 'write back' vs 'write through'

  If write-back cache, may involve replacing a dirty block (requiring write operation to lower level memory. If clean, just insert.)

  If write-through cache, just insert (lower memory is already up-to-date).

- Then, send the requested word to the processor.

- Finally, let the pipeline resume.

When write misses in D$, it takes the same process when read misses occurred. But, how to insert that in the cache? There are two options.

- Write allocate (aka Fetch on write) : Datum at the missed-write location is loaded to cache from memory, followed by a write-hit operation. Is this approach, write misses are similar to read-misses. (read missed block is always allocated in the cache.)

  It do that write the word into the cache updating both the tag and data, no need to check for cache hit (because it is newly allocated as a correct one).

- No-write allocate (aka Write-no-allocate) : Datum at the missed write location is not loaded to cache, and is written directly to the backing store.

  It do that skip the cache write and just write the word to the write buffer (and eventually to the next memory level), no need to stall if the write buffer isn't full.

Both write-through and write-back policies can use either of these write-miss policies, but usually they are paired.

- Write-back cache uses write allocate, hoping for subsequent writes or reads to the same location, which is now cached.
- Write-through cache uses no-write allocate. Here, subsequent writes have no advantage, since they still need to be written directly to the backing store.



## System Bus between Cache and Memory Interface
---
We will see three types of bus like below figure.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a5187273-7bb3-4f05-8f03-fa569a2873de)

Let's see section a. One-word-wide memory organization.

The off-chip interconnect and memory architecture can affect overall system performance in dramatic ways;

- Assume that
  - 1 memory bus clock cycle to send the address
  - 15 memory bus clock cycles to get the 1st word in the block from DRAM (row + column cycle time), 5 memory bus clock cycles for 2nd, 3rd, 4th words (only column access time).
  - 1 memory bus clock cycle to return data.
- Cache and Memory Bus Bandwidth : the number of bytes accessed from memory and transferred to cache/CPU per memory bus clock cycle.



Section b. Wider memory, has the number of memory bus clock cycles to read DRAM is faster as the number of wider blocks.

Section c. Interleaved Memory, has the number of cycles to return data word is faster as the number of memories.



## Measuring Cache Performance

---

Assuming cache hit costs are included as part of the normal CPU execution cycle, than

<center>
    CPU time = IC x CPI x CC<br>
    = IC x (CPI_ideal + Memory-stall cycles) x CC
</center>

Memory-stall cycles come from cache misses, and can be calculated as

- Read-stall cycles = (reads/program x read miss rate x read miss penalty)
- Write-stall cycles = (writes/program x write miss rate x write miss penalty)

Than, what cache performance is affected? There are several reason.

- Faster clock rate -> required #clocks increased
- The memory speed can not be improved as fast as processor cycle time
- When calculating CPI_stall, the cache miss penalty is measured in processor clock cycles
- The lower the CPI_ideal, the more pronounced impact of cache memory stalls.

A larger cache will have a longer access time. At some point, the increase in hit time for a larger cache will overcome the improvement in hit rate, leading to a decrease system performance in a result. Instead of using Hit Time, we use Average Memory Access Time(AMAT), that is the average to access memory considering both hits and misses.

<center>
    AMAT = Hit time + Miss rate x Miss penalty
</center>

In Summary, the performance has these relationship.

- When CPU performance increased, Miss penalty becomes more significant.
- Decreasing CPI makes greater proportion of time spent on memory stalls, that is relative impact of memory stall increases.
- Increasing clock rate makes memory stalls account for more CPU cycles, that is relative impact of memory stall increases.
- Can not neglect cache behavior when evaluating computer system performance.
- Therefore, we need a policy to reduce miss rate for this memory stall.

So, we need to reduce cache miss rates by **allowing more flexible block placement**.

In a direct mapped cache, a memory block maps to exactly one cache block. At the other extreme, could allow a memory block to be mapped to any cache block(fully associative cache).

A compromise is to divide the cache into sets each of which consists of n ways(n-way set associative). A memory block maps to a unique set (specified by the index field) and can be placed in any way of that set (so there are n choices). Block address is set by modulo operation by the number of sets in the cache.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/055815e1-3496-4cb5-afba-52aeeff11dc0" alt="image" style="zoom:80%;" />

But it seems that this method takes more time and more address memory than direct-mapped method. Therefore, why we need to use this method?

Let's see how this method works. when a miss occurs, which way's block do we pick for replacement? Least Recently Used(LRU) algorithm, the block replaced is the one that has been unused for the longest time, must have hardware to keep track of when each way's block was used relative to the other blocks in the set. For 2-way set associative, takes one bit per set, so set the bit when a block is referenced (and reset the other way's bit). Therefore, the hit rate is increased, the miss rate is decreased.



## Multilevel Cache

---

Multi-word blocks can result in **false sharing**, when two cores are modifying two different variables that happen to fall in the same cache block. This problem increases cache miss rates.

So, we will use **multiple levels of cache** to solve this issue. With this, we can increase performance dramatically. Consider to design L1 and L2 caches, these are very different.

- Primary cache(L1) should focus on minimizing hit time in support of a shorter clock cycle.
- Secondary cache(L2) should focus on reducing miss rate to reduce the penalty of long main memory access time.

The miss penalty of the L1 cache is significantly reduced by the presence of an L2 cache - so L1 cache can be focused on smaller size, but check a higher miss rate. For the L2 cache, hit time is less important than miss rate. So, the L2 cache hit time determines L1 cache's miss penalty.









