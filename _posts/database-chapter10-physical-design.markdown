---
layout: post
title: "[Database]Chapter10. Physical Design"
subtitle: "physical design"
categories: dev
tags: database physical design
comments: false
---

## Introduction
> Physical Design for Database.

- Contents
	- [What is Physical Design?](#what-is-physical-design)
	- [File Organization](#file-organization)
	- [Design Access Method](#design-access-method)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## What is Physical Design?
---
Physical Design for database is that design the architecture of database based on logical schema. It has the format of record, the order for saving, access directory, etc.

Note that only DBA can contribute for physical design of database.



## File Organization
---
File Organization is that...

- Save several files for database
- Save several records for file
- A record formed with several fields

For the simplest method to organize database,

- Set fixed length for record
- One file save only one record
- One relation is mapped with only one file



We will see these aspects one by one.

### Fixed length vs Variable length

- Fixed length is easy for implementing database. If some data is deleted, delete it first and save record number at file header. Then, organize empty records later.

- Variable length is general way to implement database. File header has records' offset and length to show its position in file. Records is saved from the end of file to the first of file(Depend on the way of implementation.)

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/141ca484-d7a6-480c-87ea-ec1c7aee3a0e)

  But, as the records can change its length, all other records behind must be moved to the front. So Slot(records order number.) is used instead of offset data.



### The way to save record in a file

- Sequential File Organization : save by the order of key value.
- Hashing : save by the order of hash value.
- Multi-table clustering file organization : save several relations in a one file.



## Design Access Method
---
Here are some way to design with :

- Indexing guarantee fast accessing when searching records. It is usually implemented with B+ tree. 
- Hashing uses the value to search the location of record. Only fixed value can be used for search, Not with ranged value.
- Clustering saves several related records with one space.







## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  