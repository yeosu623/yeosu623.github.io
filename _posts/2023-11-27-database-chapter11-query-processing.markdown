---
layout: post
title: "[Database]Chatper11. Query Processing"
subtitle: "query processing"
categories: dev
tags: database query processing
comments: false
---

## Introduction
> Learn Query Processing for Database.

- Contents
	- [Overview](#overview)
	- [Catalog Information](#catalog-information)
	- [Calculate query processing costs](#calculate-query-processing-costs)
	- [Cost of Select Operation](#cost-of-select-operation)
	- [Cost of Join Operation](#cost-of-join-operation)
  - [Evaluation of Expressions](#evaluation-of-expressions)
  



## Overview
---
This figure shows that how query statement process.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/15bd973e-b201-412b-833f-80cfffd4edd6)

Query processing is optimizing, or more accurately, improving the strategy for processing a query. There are two way to optimize query : The Network/Hierarchical Model, which is applied by Application Programmer, and The Relational Model, which can be applied automatically.



## Catalog Information
---
Before to see the actual contents, let's see some statistics for Each Relation r.

- n_r : The number of records in r
- b_r : The number of blocks containing records of r
- s_r : size of a record of r in bytes
- f_r : blocking factor of r (b_r = ceiling(n_r / f_r))
- V(A, r) : The number of distinct values that appear in r for attribute A.
  - If A is a key for r, then V(A, r) = n_r
- SC(A, r) : Selection cardinality of attribute A of r. 
  - SC(A, r) = n_r / V(A, r)

Also, there are some statistics about Index i.

- f_i : The average fan-out of internal nodes of i
- HT_i : The height of i
  - B+ Tree : HT_i = ceiling( log_fi(V(A,r)) )
  - Hash Index : HT_i = 1
- LB_i : The number of  blocks at the leaf level of i



## Calculate query processing costs
---
There are some aspects to estimate costs : **Disk access time**, CPU execution time, and communication time(for distributed/paralleled query.)

Disk access time is the most important aspects for estimating cost. In this chapter, we assume that all access time is always same, and The time of recording the results on disk will be ignored.



## Cost of Select Operation
---
There are some way to operate select query, so we need to calculate it respectively.

- Algorithm 1 : Linear search. Scan all blocks to find a specific record.
  - Cost : b_r
- Algorithm 2 : Primary index, equality on key.
  - Cost : HT_i + 1
- Algorithm 3 : Secondary index(clustered), equality on non-key
  - Cost : HT_i + ceiling( SC(A, r) / f_r )
- Algorithm 4: Secondary index(non-clustered), equality on non-key
  - Cost : HT_i + SC(A, r)

For example, Imagine this attribute : Account(branch-name, account-number, balance)

- n_account = 10000, f_account = 20
- V(branch-name, account) = 50
- V(balance, account) = 500
- A clustered, B+ tree index for branch-name
- A non-clustered, B+ tree index for balance
- Assume that B+ tree index stores 20 pointers per node.

Then, how much cost this query? 

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6f686725-893e-4265-8efd-ea1df105beee)

Let's see step by step with algorithm 3.

- V(branch-name, account) = 50.
  - 3 <= LB_branch-name <= 5
- HT_branch-name = 2
- SC(branch-name, f_account) = 10000 / 50 = 200
- Therefore, Cost = 2 + ceiling(200 / 20) = **12**



## Cost of Join Operation
---
Join is one of the most expensive among SQL queries. So we must to look for this. Let's see these one by one.



### Nested-Loop Join

The very simple and most expensive way.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/132056ca-6695-46c3-9688-249d07bbdb88)



### Block Nested-Loop Join

Divide records into block unit. This way is much cheaper than Nested-Loop Join.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/788a09e1-437d-4d4d-96a1-a719094cdbdf)

### Indexed Nested-Loop Join

Do the index lookup for inner relation, instead of file scan. This method can be used when join attribute has their index.



### Sort Merge Join

Do sorting before do join operation.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/9e9e407b-e91c-4abb-994e-3feb75d38681)



### Hashing Algorithms

When there are two relations R and S, make hash table for R and save it on memory first, and then scan records for S by probing hash table.

But, there are some situation that when hash table cannot be saved in memory. So there are some partitioning algorithm to solve this issue.



Simple Hash Join has same performance with classic hashing. But overflow can be occurred often, if memory size is small.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3cd77aa0-0f1d-4fa6-9123-5f04d593ca78)

Grace Hash Join has same performance on different memory size. It always makes fixed I/O operation.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d8bcb0bf-ba80-4766-b8b9-a526cb9474a3)

Hybrid Hash Join's performance is depend on memory size. When memory is large, it is similar on simple hash join. And when memory size is small. it is similar on grace hash join.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8ff0ce58-5419-49ca-9b90-0e511295249f)





Note that when partition block is larger than the number of memory, and when data skew is existed, the partition overflow is occurred.

It can be solved with tuning. When partition overflow on disk (Grace/Hybrid Hash), it can be solved by reprocessing the partition into two or more pieces. When partition overflow in memory (Simple Hash), it can be solved by reassigning some buckets to a new partition on disk.



By the way, how n-way join can be tuning? There are some consideration to do this.

- Select Join Order for no need of Cartesian Product.
- Will we need to save join result?
  - When join result is used to outer relation, it can be used for sequenced relation.
- Any join method can be used for each join.



## Evaluation of Expressions

---

Estimation the cost of expressions contains not only the operation costs, but also the saving costs for intermediate results. But, if pipelining is implemented on DB, saving costs can be ignored for most of relational operation. (except : sort merge, etc.)

For more easy calculate costs, some equivalence rules is here.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/936da4c1-b7db-4283-87a0-a070cfc7df17)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/510e65e4-05e3-4b99-9288-e1e02d0da03e)

Expression can be transformed for tree for easy calculation. Leaf node is input relation, and internal node is relational algebra operation.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/edc30fd9-fe54-4eb2-807e-245a93794a46)



So, how we can choose the expression for minimum costs? There are two ways for that.

- Cost-Based Optimization : Collecting statistical costs for each operation to choose the minimum cost expression. But it takes a long time to make the expression.
- Heuristic Optimization : Optimize the expression by some basic rules. It can be used for previous stage of Cost-Based Optimization.
  1. **Perform selection as early as possible.**
  2. **Combine certain selections with a prior Cartesian product to make a join.**
  3. **Combine sequence of unary operations.**
  4. Look for common sub-expressions in an expression.
  5. Preprocess files appropriately.
  6. Perform projections early.
  7. Identify those sub-tree whose operations can be pipelined, and execute them using pipelining.

Below is the example for Heuristic Optimization. We can stop the Heuristic Optimization in an appropriate stage.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e4ad1d84-0a61-4188-a48e-91577ef4d317)

