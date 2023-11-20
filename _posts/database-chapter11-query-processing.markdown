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





