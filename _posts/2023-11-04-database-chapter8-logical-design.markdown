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
	- [Change EER model into relationship model](#change-eer-model-into-relationship-model)
	
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

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/536a5fed-009b-4706-88b9-a1a76c0207c3)



#### Step 4. Change binary 1:N relationship

When table S is on N relationship and table T is on 1 relationship,

- get primary key on T within table S as foreign key.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/eeaf4c54-4762-47ee-b5ee-bf44faeee2ae)



#### Step 5. Change binary M:N relationship

- Create new relationship table S.
  - get two table's primary key into table S's foreign key.
  - table S's primary key is combined with two table's primary key.
  - When attributes on relationship is existed, get it on table S.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/aee036bf-e84b-4516-92ff-a7a2b45eadf1)



#### Step 6. Change multiple attributes

- Create new table S with multiple attributes, A.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a2baafb6-2dd1-4f5b-b822-b90659544358)



#### Step 7. Change N-ary relationship

- Create new table S.
  - get all entity's primary key as table S's foreign key.
  - Save attributes on relationship on table S.
  - The primary key on S is composed foreign keys.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/228f38af-1ebd-4de0-9f73-c7bdd0d79a34)



So, here is the final results for that ER diagram.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/38e217bf-4fad-4835-b091-aa60e841ac44)



## Change EER model into relationship model
---
After takes step 1 ~ step 7, 

#### Step 8. Change Specialization and Generalization

When there are superclass C = (k, a1, a2, ..., an) and the number of m subclasses {S1, ..., Sm}, and k means key and a1, a2... mean attribute1, attribute2...,

There are four way to change their relationship.

- Step 8A. Change Superclass and Subclasses table both.
  - Create table L = (<u>k</u>, a1, a2, ..., an) for superclass C. k is stands for key.
  - Create Li = (<u>k</u>, attributes of Si) for subclasses Si.
- Step 8B. Change Subclasses only.
  - Create table Li = (<u>k</u>, a1, a2, ..., an, attributes of Si) for subclasses Si.
- Step 8C. Merge both classes into the one table, and add 1 attribute type
  - Merge tables as the one table L = (k, a1, a2, ..., an, attributes of number of m subclasses, t)
  - t : indicate subclass
- Step 8D. Merge both classes into the one table, and add m attribute type
  - Merge tables as the one table L = (k, a1, a2, ..., an, attributes of number of m subclasses, t1, ..., tm)
  - ti : the boolean type. It is true if the record is in Si subclasses.
  - Suitable for overlapping constraint



Below is the example for changing specialization and generalization.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d6a51baf-e75a-4bda-910f-b9d0dc05e01a)

When Step 8A is applied for above example,

EMPLOYEE(<u>SSN</u>, FName, MInit, LName, BirthDate, Address, JobType)

SECRETARY(<u>SSN</u>, TypingSpeed)

TECHNICIAN(<u>SSN</u>, TGrade)

ENGINEER(<u>SSN</u>, EngType)



When Step 8C is applied for above example,

EMPLOYEE(<u>SSN</u>, FName, MInit, LName, BirthDate, Address, JobType, TypingSpeed, TGrade, EngType)



#### Step 9. Change Union type

This step has simple method : use surrogate key to merge superclasses.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/f157e5dc-d16a-496a-8e4f-22f4f8d639ff)

For above example,

OWNER(<u>Owner_id</u>)

REGISTERED_VEHICLE(<u>Vehicle_id</u>, License_plate_number)



