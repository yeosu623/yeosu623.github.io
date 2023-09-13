---
layout: post
title: "[Database]Chatper1. Database Introduction"
subtitle: "chapter1. database introduction"
categories: dev
tags: database
comments: false
---

## Introduction
> The introduction of database.

- Contents
	- [What is database?](#what-is-database)
	- [The cons of file data system, and pros of database](#the-cons-of-file-data-system,-and-pros-of-database)
	- [3 layers of database](#3-layers-of-database)
	- [Schema and Instance](#schema-and-instance)
	- [Data models](#data-models)
  - [The language for database](#the-language-for-database)
  - [Transaction](#transaction)
  
## What is database?
---
Literally, database is large digital data storage. To access database, many corporates use DBMS(Data Base Management System) to manage database with SQL(Structured Query Language) to make interface for normal applications, programs, software.

From past, corporates manage data for individual files, like excel format. But it cannot be guarantee data duplication, which can be serious problem. Plus, they must access data by opening files one by one! So Oracle company made DBMS programs, which is very very expensive, over $400,000...

Here is the question. Why many companies buy this much expensive software? Without DBMS, application developers must consider data structures with complex concepts, like the combination of hashmap, binary tree, list, etc. So with DBMS, many developers can easily make application software.



## The cons of file data system, and pros of database
---
![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6e33da04-68c7-457b-b2eb-181315b0d726)

Like described above, the file data system has some disagree points.

- Data Redundancy : The files store data is independent each other, so some data could be duplicated. It causes lack of memory and hard to manage, also it makes issues for security. Almost every database find data with key value, so if someone find some data with a key and reaches for multiple data, then a person can get a very informative data.

- Data Dependency : If data structure has changed, all related program also need to be changed.

  

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/14a5315a-26bb-4b8d-8b98-3815deec27a0)

So people made more advanced data management program, which means database system. It could make us to solve issues with file data system(data redundancy, data dependency), which the DBMS solves it.

DBMS gives us lots of pros, but most of all, it gives the **STANDARD** database management system. Although DBMS is very expensive and it makes program a bit slow, this is the reason for buy and use it.



## 3 layers of database
---
DBMS has two major purposes.

- To conceal the detailed operation for saving and handing data
- To manage and handle data for efficiently

Data abstraction is related to the first purpose, so lets explore this concept.



Data abstraction has three layers :

- Physical layer : A layer for save data in real world. e.g. file location, index, sorting, field format, etc.
- Logical layer : A layer for the content and relationship of data.
- View layer : It is the viewpoint of user. So physical layer and logical layer cannot be seen.



## Schema and Instance
---
Before we see the models of database, let's brief some important terminology of database.

- Schema : the structure of database. It has largely divided into three concept:

  - Physical schema(Internal schema)  : To show how the presented data is stored.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/85826163-0561-457f-8a52-162abd9b146e)

  - Conceptual schema : To show how the data is structured. Not to see the real data.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/1dfa37c4-e100-4ccb-bc62-b4e6b16c6113)

  - External schema : To show viewpoints of real-users to see database.

    <img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0c6a4bb5-925a-4c5b-ad69-7aa2c62f4cac" alt="image" style="zoom:80%;" />

- Instance : The database state in specific time.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/157643eb-093c-4ffe-a52a-b1703fb85391)

  

## Data models

---
Now, let's see some famous data models.

Data models is the conceptual tool for represent data, the structure of data, the meaning of data, and the limitation of data. Three well-known is here :

- Conceptual model : Usually, it is used in database design level. Some DBMS might not support this model. Typical conceptual model is **Entity-Relationship Model** and Object-Oriented Model.

  - Entity-Relationship Model(ER Model) represent the real world with entity and relationship.

    Entity is a concept or a information for represent real world. For example in a bank, a account and a client can be.

    Attribute is a feature or state of entity. e.g. account balance, client name.

    Relationship is the relation among entities. e.g. client's account.

- Logical model : It is an assumption for implementation by specific DBMS. DBMS supports these models:

  - **Relational Model** : Entity and Relationship is represented by **TABLE**. It is most widely used in these days. The current supporting DBMS is Oracle, MySQL, SQL Server, Sybase, and etc.
  - Network Model : Entity is represented by graph data structure. (n : n) relationship.
  - Hierarchical Model : Entity is represented by tree data structure. (1 : n) relationship.
  - Object-oriented Model : Almost same as Object-oriented Programming(OOP) concept.
  - **Object-Relational Data model** : The advanced model of Object-oriented model. It is most well widely used in these days, and supported by famous DBMS.

- Physical model : It is the method for saving data in real world. It has some concept for a format of set record, an order for save data, an access path, an assignment data for a memory, etc.



## The language for database

---

- DDL(Data Definition Language) : To defining, modifying, and deleting database schemas.
- **DML(Data Manipulation Language)** : To searching, inserting, changing, and deleting data records.
  - To use DML, you can use **query language** to manipulate database. Then embedded query language that made by C, C++, JAVA converts your query language and operate it.
- DCL(Data Control Language) : To manage transaction and security. we will see about transaction below. 



## Transaction 

---

Transaction is a unit for logical operation. For example in bank, deposit, withdraw, transfer, check balance could be.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c815a36a-e37d-40a9-857d-f36cde76cb63)

To see above database command, the blue and red words are transactions. We will see these commands in Chapter 3. SQL.



