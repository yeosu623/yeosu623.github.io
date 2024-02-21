---
layout: post
title: "[Database]Chapter6. Data Modeling with ER Model"
subtitle: "data modeling with er model"
categories: dev
tags: database modeling er
comments: false
---

## Introduction
> Learn to make the data model through ER model.

- Contents
	- [The process to design the database](#the-process-to-design-the-database)
	- [Example COMPANY Database](#example-company-database)
	- [The concept of ER model](#the-concept-of-er-model)
	- [The consideration for ER model](#the-consideration-for-er-model)
	
## The process to design the database
---
The process takes **the conceptual design** to make the database.

- **Conceptual Design** represent the entity and relationship, and attributes to show the entire of system.
- **Logical Design** changes a conceptual schema to logical schema which on DBMS.
- **Physical Design** forms database in a real world with logical schema. It handles the format of record, the order of record, the path to access, etc. Only DBA can take the physical architecture.



## Example COMPANY Database
---
This is the requirements for example company database.

- COMPANY database is manage employee, department, and project 
- company is formed with multiple department.
  - A department has name, department number, and the manager.
  - Need to be saved with manager's hire date
  - A department has multiple branches.
- A department operates multiple projects.
  - A project has name, project number, and places.
- An employee has name, employee number, address, salary, gender, and birthdate.
  - An employee is joined in one department, and takes multiple projects.
  - Need to be saved how much times did with the employee one by one.
  - An employee has direct manager.
- An employee has multiple dependent(family).
  - dependents has name, gender, birthdate, and the relation with the employee.



## The Concept of ER Model
---
There are many concept to represent ER model.

- Entity is the object or concept to present in DB.

- Attribute is used to present the entity.
  - Simple/Composed Attribute : Cannot be divided into another attributes/or can.
  - Single/Multiple Attribute
  - Null Attribute : has no value.
  - Dependency Attribute : Can be made the value by another attribute.

- Key is used to recognize the entity in one attribute. The key must has uniqueness and minimality.

  - Super Key : The attribute set which has uniqueness. It might has dummy attribute. ex) ID number, ID number + name
  - Candidate key : the super key without dummy attribute. ex) ID number
  - Primary Key : One of the Candidate key. ex) employee-employee number, ID number-citizen

- As the initial stage to design the COMPANY database, just write all of the attribute and connect it.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d74648ed-3162-4e16-ac47-b53e6857f04c)

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/52a4ddac-68df-4672-9e18-47fb37c02f58)

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/82e4c80e-e189-4212-b2f5-b07ca541a4bf)

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a5b6e94f-23b7-4f97-8268-e3129dba2bdc)

- Then, think about the relationship.

  ![image-20231018173220383](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231018173220383.png)

  - you can represent relationship with line.
    - 1 and N show cardinality.
    - single line show total relationship, while double line show partial relationship.

- Plus, there are the **Weak Entity Type** for special use. It is the entity that has no key attribute, contrary to the Strong Entity.

  For example, Dependent(name, gender, birthdate) is the weak entity, because it has no unique attribute for key. To recognize weak entity uniquely, it should get key from other entity, called as Owner Entity Type.

  The relationship that connected between weak entity and owner entity is called as "Identifying relationship".

  The key that get from owner entity type is called as "Discriminator" or "Partial Key".



After we added the entities, and next step is connect among entities with specific relationship.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/797d67c3-c3aa-4381-9ab6-434a28c454dd)

Then the final ER Diagram is completed :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d1963700-04cf-40d6-9add-aae8c3a32ffe)



## The consideration for ER model
---
There are the basic tip for make ER model.

- The basic method for recognize entity, relation, attribute
  - Entity : noun
  - Relationship : verb
  - Attribute : The noun for modifying entity
- The basic tips
  - Improving the prototype ER model is better than making ER model at once perfectly.
  - When attribute is referenced by other entity, change it to relationship.
  - When the attribute is showed by several entities, consider change it to entity, and vice versa.



