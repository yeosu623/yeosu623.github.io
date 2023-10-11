---
layout: post
title: "[Database]Chapter4. Advanced SQL"
subtitle: "chapter4 advanced sql"
categories: dev
tags: database sql
comments: false
---

## Introduction
> The more advanced concepts of SQL.

- Contents
	- [SQL Datatype and Schema](#sql-datatype-and-schema)
	- [Integrity Constraints](#integrity-constraints)
	- [Chapter3](#link-to-chapter3)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## SQL Datatype and Schema
---
How SQL store data? in programming, there are integer, decimal, array and user-defined type(e.g. struct, instance) to store data. Likewise, database has integer and decimal type, and image, video, sound.

- Integer, Decimal : Number

- Character, String : Char(static length), Varchar(Dynamic length)

- Time : Date, Timestamp, Timestamp with time zone

- Binary data : Raw

- Row ID : RowID

- Image, Video : CLOB(Character Large-Object), BLOB(Binary Large-Object)

  

There are three-level hirearchy to construct database. (Oracle didn't support relations and views concept)

- Catalog : Database. Composed with several schema.
- Schema : Composed with relations and views.
- Relations and Views : have a real-data

To indicate unique relation, you can use  naming rule like this :

- catalog5.bank_schema.account

In oracle, there are no relations and views concept. So, use naming rule like this

- scott.student
- system.help



## Integrity Constraints
---
- Object Integrity : Null or duplicated values cannot stored in primary key.

- Domain Integrity : Restrict value which attribtes can have.

  - You can use `CHECK` statement to set restrict condition when you `CREATE TABLE`.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6d78805d-deb4-45b9-99d5-3e317ff09921)

  - You can use `Disable Constraint` or `Enable Constraint` to configurate restrict option when you do `ALTER TABLE`.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/32c2177e-c9ed-49d0-bbda-e76828fd04ee)

  - There are two way to make constraint : Column Constraint and Table Constraint.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/17eff2e1-92e0-481a-a0c6-a5ab99e0c391)

- Reference Integrity : Assume there is foreign key K about relation S in relation R. Then, foreign key K must be defined in relation S and must have only one value.

  - To define reference integrity, use `REFERENCE` statement when do `CREATE TABLE`.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/6cbeca9e-e5cf-46bd-995e-705f2f4c1465)

    (Tips : you can set `REFERENCES Department(DeptNo) ON DELETE SET NULL` instead.)

- Assertions : higher concept of domain integrity and reference integrity. Because Column constraint only can reference single column. And Table constraint can reference several columns only within its own table, cannot to reference another table's column. So, Assertions use `Trigger` statment to overcome `CHECK` statement's limitation.

- Trigger : It is automatically executed when data get a change. It can use for handle errors and conditional run.

  There are 12 types of trigger : Before/After, Insert/Delete/Update, Row/Statement, etc.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ccd4fb96-96b0-4125-8376-e8b2008e7b52)

  

  

  







## Link-to-Chapter3  
---
Chapter3에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  