---
layout: post
title: "[Database]Chapter8. Logical Design"
subtitle: "logical design"
categories: dev
tags: database logical design
comments: false
---

## Introduction
> Learn to change ER model and EER model into relationship model.

- Contents
	- [Change ER model into relationship model](#change-er-model-into-relationship-model)
	- [Chapter2](#link-to-chapter2)
	- [Chapter3](#link-to-chapter3)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## Change ER model into relationship model
---
There are many consideration for changing ER model into relationship model. Here are 7 steps to do it :

1. Change strong entity types
2. Change weak entity types
3. Change binary 1:1 relationship
4. Change binary 1:N relationship
5. Change binary M:N relationship
6. Change multiple attributes
7. Change N-ary relationship

During changing ER model, it is good for decrease the number of tables and the number of null attributes. From now on, we will do exercise with sample ER model.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/36be1adb-3aef-4a2a-a475-98011e18245c)



#### Step 1. Change strong entity type

- Change strong entity type(E) into one table (R).
  - All attributes on E is same on table R.
  - All combined attributes' element attribute on E is same on table R.
  - when multiple keys on E, choose only one key on table R.
  - when key is combined, decompose it and choose all of it on table R.

- For Example,
  - Employee(<u>Ssn</u>, Bdate, Address, Salary, Sex, Fname, Minit, Lname)
  - Department(<u>Dnumber</u>, Dname)
  - Project(<u>Pnumber</u>, Pname, location)

Below photo is the example of decomposing combined attributes.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/f4c9637f-c78c-4762-b2a6-057454e25558)



#### Step 2. Change weal entity type

- Follow this rules with Step 1:
  - Change all attributes to the table.
  - Change all key to the table's foreign key.
  - The table's key is : (entity's key, weak entity's discriminator)
- For example,
  - Dependent(<u>Essn, Name</u>, Sex, Bdate, Relationship)



#### Step 3. Change binary 1:1 relationship

There are 3 ways to change 1:1 relationship R with table S, T.

- With foreign key : save primary key on T into foreign key on S, the completely attended table.
- Merge as one table : merge S, T into one table. Only can do this when S, T table is completely attended. If this criteria doesn't satisfied, Null attribute is made.
- Create relationship table R : get S, T's primary key as foreign key. The primary key on R is the key with completely attended table.



#### Step 4. Change binary 1:N relationship

When table S is on N relationship and table T is on 1 relationship,

- get primary key on T within table S as foreign key.



#### Step 5. Change binary M:N relationship

- Create new relationship table S.
  - get two table's primary key into table S's foreign key.
  - table S's primary key is combined with two table's primary key.
  - When attributes on relationship is existed, get it on table S.



#### Step 6. Change multiple attributes

- Create new table S with multiple attributes, A.



#### Step 7. Change N-ary relationship

- Create new table S.
  - get all entity's primary key as table S's foreign key.
  - Save attributes on relationship on table S.
  - The primary key on S is composed foreign keys.













## Link-to-Chapter2  
---
Chapter2에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter3  
---
Chapter3에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  