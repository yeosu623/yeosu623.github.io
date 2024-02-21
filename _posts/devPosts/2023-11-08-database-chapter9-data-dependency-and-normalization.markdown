---
layout: post
title: "[Database]Chapter9. Data Dependency and Normalization"
subtitle: "data dependency and normalization"
categories: dev
tags: database dependency normalization
comments: false
---

## Introduction
> About data dependency and data normalization.

- Contents
	- [Possible problem for relational database](#possible-problem-for-relational-database)
	- [Decomposition](#decomposition)
	- [Functional Dependency](#functional-dependency)
	- [Normalization by Functional Dependency](#normalization-by-functional-dependency)
	
## Possible problem for relational database
---
When they relational database create, two general possible problem are occurred : Data duplication, and Cannot show the specific data.

Consider this example.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d4860914-8aaf-4ad2-942b-950024f7f7c7)

Data duplication occurred in every attributes, so they cannot set what attribute is the key.

Also, some data cannot be showed. For example,

- Insert Anomaly : How branch data can be inserted, which has no Loan-number?
- Delete Anomaly : Will guarantee Delete L-29 Loan number means that delete Pownal Branch-name?
- Update Anomaly : How to update assets, which placed in Downtown Branch?
  

So, we will do decomposition for this table.



## Decomposition
---
The one way to solve data duplication and data anomaly problems. This method is that decompose the relation, but wrong decomposition can loss some information. For example, when decompose this table with customer-name, some duplication data can be connected with several data, so it cannot connected correctly.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6e6d910c-c485-42d0-975a-9ed852887073)

To avoid that issue, check the lossless join decomposition condition.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/2abc71b3-7a40-4c89-a163-c89e02eb2720)



## Functional Dependency
---
This is wrote as **a->b**.

When the attributes **a** and **b** in table r, and two records t1 and t2 in table r.

Then, functional dependency is approved when t1[a]=t2[a] then t1[b]=t2[b].

For example, when there is the attributes

<center>Loan = (branch-name, loan-number, customer-name, amount)</center>

Then, this can be functional dependency.

<center>
    loan-number -> amount (O)<br>
    loan-number -> branch (O)<br>
    loan-number -> customer-name (X)
</center>



And, there are some set closure for function dependency.

set F's functional dependency closure is wrote as **F+**.

This is set of all functional dependency that are induced logically by set F.

- Trivial Dependency : When attribute a contains attribute b. Wrote as a->b.
- Partial Dependency : When correct a->b, and attribute r is contained in a and r->b is correct, so that b has partial dependency on a.
  - Example : (Branch-name, Branch-address) -> Postal number



Partial Dependency is expended onto the **Armstrong's rule**.

When there are attributes a, b, r, and e,

- Basic rules
  - Reflexivity : a->b for (b is contained in a).
  - Augmentation : If a->b and (r is contain in table R), then ra->rb
  - Transitivity : If a->b and b->r, then a->r
- Expended rules
  - Union : If a->b and a->r, then a->br
  - Decomposition : If a->br, then a->b and a->r
  - Pseudotransitivity : If a->b and br->e, then ar->e



Also, there is attribute set closure, a+.

This is set of all attributes which have functional dependency on attribute a.

For example, there is schema and function dependency :

<center>
    R = (A, B, C, G, H, I)<br>
    F = {A->B, A->C, CG->H, CG->I, B->H}
</center>

And induced dependency on F+ is :

<center>
    A->H<br>
	CG->HI<br>
	AG->I
</center>

Then, closure a+ can be defined as

<center>
    A+ = ABCH<br>
	(AG)+ = ABCGHI (Candidate key on table R.)
</center>



Lastly, there is Canonical Cover the helping implementation.

FD(Functional Dependency) is one of the condition for integrity restriction. And FD is needed to be checked when change the DB. But it is difficult to check all FD, so they found the implementation method that when same closure exited for several FD, choose the most simple FD for implementation.

To do the canonical cover, we need to know the extraneous attributes. This is defined as :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8a5d0cf5-99a5-41a7-9a22-1c964fbcc42d)

Then, Canonical Cover(Fc) for the set of functional dependency F, is defined as

- Fc -> F and F -> Fc
- All dependency on Fc has no extraneous attributes.
- If a1->b1 and a2->b2 in Fc, then a1 != a2
  - This means that merge a1->b1 and a1->b2 to a1->b1b2.



Here is the example. When the schema is

<center>
    R = (A, B, C)<br>
    F = {A->BC, B->C, A->B, AB->C}
</center>

Then, Canonical Cover can be calculated like this:

- Change (A->BC and A->B) into A->BC
- A is extraneous in AB->C : Change AB->C into B->C
- C is extraneous in A->BC : Change A->BC into A->B

Finally, Canonical Cover is A->B, B->C.



## Normalization by Functional Dependency

---

Before to do actual normalization, let's see the conditions for normalization.

For a good decomposition, it satisfy two conditions.

- Lossless Join Decomposition : When there are R1 and R2 tables, this condition is satisfied when (R1 intersect R2) -> R1 or (R1 intersect R2) -> R2 is satisfied.
- Dependency Preserving Decomposition
  - When we need to check functional dependency and to do it by join operation, it is very confused.
  - So, Dependency Preserving Decomposition is defined :
    - When F is the set of functional dependency on table R
    - R1, R2, ..., Rn is the decomposed on table R
    - Fi is the set of functional dependency on table Ri
    - And F' = F1 union F2 union ... union Fn.
    - When F'+ = F+, the dependency preserving decomposition is satisfied.



So, what is normalization, and why is it needed?

Normalization is the process that classifying relations by some criteria. It should be done because some table is needed to decompose some problem relations, so normalization is the process that decomposition as no information loss, by lossless join decomposition and dependency preserving decomposition.

But, normalization has multiple level and it should be done by proper level, because as the normalization is done more, the more tables is decomposed. This means that join operation should be done much more, so performance of DB is dramatically decreased.

Here are multiple levels of normalization :

- 1st Normal Form(1NF) : This is when all attributes has atomic value. In other word, all relations is formed by single attribute.
- 2nd Normal Form(2NF) : 1NF has the problem that it has partial dependency. So, 2NF is that 1NF's all attributes besides primary key have dependency on the primary key.
  - Dependency a->b satisfy one of them below.
    - simple and single dependency
    - a is super key of table R
    - a doesn't included in any other candidate key
    - b is included in primary key
  - The method to do lossless join decomposition to transform into 2NF
    - Suppose a->b, where a is included in P(the set of attributes included primary key), and b isn't included in P.
    - Then, decompose R as R1 = (a,b) and R2 = (R - b).
- 3rd Normal Form(3NF) : 2NF has the problem that it has transitive dependency. So, 3NF is that 2NF's all attributes besides primary key don't have transitive dependency on the primary key.
  - Dependency a->b satisfy one of them below.
    - simple and single dependency
    - a is super key of table R
    - b is included in primary key
  - The method to do lossless join decomposition to transform into 3NF
    - Suppose a->b, where a is not a super key for R and b is not included in the candidate key.
    - Then, decompose R as R1 = (a,b) and R2 = (R - b).
- Boyce-Codd Normal Form(BCNF) : 3NF has the problem that it has some attributes besides primary key has functional dependency for some of attributes of primary key. So, BCNF is that 3NF's all discriminator for function dependency transform as candidate key.
  - Dependency a->b satisfy one of them below.
    - simple and single dependency
    - a is super key of table R
  - The method to do lossless join decomposition to transform into BCNF
    - Suppose non-trivial dependency a->b, where a is not a super key for R.
    - Then, decompose R as R1 = (a,b) and R2 = (R - b)

