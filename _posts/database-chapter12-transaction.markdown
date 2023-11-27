---
layout: post
title: "[Database]Chapter12. Transaction"
subtitle: "transaction"
categories: dev
tags: database transaction
comments: false
---

## Introduction
> Brief explanation of transaction in DB.

- Contents
	- [What is Transaction?](#what-is-transaction)
	- [Transaction State](#transaction-state)
	- [Concurrent Executions](#concurrent-executions)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## What is Transaction?
---
It is a logical operation unit for users, and a concurrency control and recovery unit for system. We will see the transaction for users in this chapter, and we will see the concurrency control and recovery system in chapter 13 and 14, respectively.



Transaction has 4 important characteristic : ACID. (Reference : [wikipedia](https://en.wikipedia.org/wiki/ACID))

- Atomicity : Transactions are often composed of multiple statements. Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely or fails completely.
- Consistency : Consistency ensures that a transaction can only bring the database from one consistent state to another, preserving database invariants.
- Isolation : Transactions are often executed concurrently (e.g., multiple transactions reading and writing to a table at the same time). Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially.
- Durability : guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power outage or crash).

Note that Atomicity and Durability can be implemented by Shadow Copy Technique. 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/da0f369d-b1d0-4fca-b1d6-b1c5ebf01a2b)



The very simple transaction is below. It gives direct understanding for users.

```C
Read(A); A = A - 50; Write(A);
Read(B); B = B + 50; Write(B);
```



## Transaction State

---
Commit and Abort is not done once. DBMS do commit their data one by one(partially commit), and check whether the data is sent to database correctly or not. We will see this on detail in chapter 14, the recovery system.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/aacb21fc-2d36-4088-83e3-2e0217057b13)



## Concurrent Executions
---
It is hard to implement concurrent executions, but it has great good reasons for allowing concurrency.

- Increase system throughput : increase the usage of CPU and disk.
- Decrease average response time for transactions : Think about FIFO and Round Robin.

Concurrency Control guarantee the correct result for paralleled execution of transaction. We will see this on detail in chapter 13. the concurrency control.



(Continue on page 7... end on ???)



## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  