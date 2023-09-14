---
layout: post
title: "[Database]Chapter2. Relational Model"
subtitle: "chapter2. relational model"
categories: dev
tags: database relational model
comments: false
---

## Introduction
> The structure of relational model, and the relational algebra.

- Contents
	- [The structure of relational model](#the-structure-of-relational-model)
	- [The relational algebra](#the-relational-algebra)
	
## The structure of relational model
---
Relational database is formed of **Relations** that has unique names. All entity-relation model can be represented on relations.

**Relations is the unit for saving data in database.** Let me explain some important terms :

- Record : A row line. In other words, a line of data.

- Fields : A column line.

- Schema : A set of relation names and attributes.

- Instance : A set of records.

  ![relation model](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/62f04bf7-d99e-4fb7-93b6-e944aaced6fa)

- Attribute : A specific information of relation. All attributes must be different each other.

- Degree : A number of attributes.

  ![rm 2](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e46cb1b1-cec5-4526-9a6e-40052284e507)

- Tuple : An other words of the record.

- Cardinality : A number of records.

  ![rm3](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/21c1f46f-ee7e-4a49-bba6-3e20ac3eb11a)

- Domain : A set of values in attribute. For example, Client ID is 4 digit numbers, Client First Name is 20 maximum size of string,... etc.

  ![rm4](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e17acfb3-e6d2-4862-90d2-0aa247e5c229)

Plus, there are some characteristics of the relations.

- All records in relation must be different each other.
- The order of records is not important.
- The order of attribute is also not important.
- Relations can be changed by inserting, deleting on real-time.
- All attribute must be different each other, but its value can be same. However, its values must be single value, cannot be multiple value. (e.g. {Stewart, Jameson})



We can use query language to handle relations, and SQL is the most world-wide use for this action. We will see how to use SQL in chatper 3. But before we go to see at SQL, let's see the concept of relational model.



## The relational algebra  

---
The relational algebra is the best method to explain the relational model.

The relational algebra can do that get an single relation and create a new relation.

- The operators about input single relation : **Select, Project**
- The operators about input two relations : **Union, Set Difference, Cartesian Product**
- Other operators : Set Intersection, Join, Division



OK, let's see these operator one by one with this example Entity-Relation Diagram.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3f8b904f-08dc-4307-b239-bb43d03370e1" alt="image" style="zoom: 67%;" />

- Relations created from entities :

  <img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6c7ff26f-8cdf-42ec-a25c-c41e2e424af7" alt="image" style="zoom:67%;" />

- Relations created from relationship :

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c69e6c92-c82e-4f1f-9816-e77bca85837a" alt="image" style="zoom:67%;" />

(To learn how to convert ER diagram to relational schema, see this [tutorial](https://www.youtube.com/watch?v=OwdFzygGZqk&ab_channel=OrangeOutputs).)

