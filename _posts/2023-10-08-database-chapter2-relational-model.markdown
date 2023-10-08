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



- Select : Create new relation with records from relation r where condition P is true.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/23cd2840-ca04-4c97-8f2f-ebc9d562f0c6)

  Example : Select "Brighton" branch information from Account table.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e55c72c7-ef07-44ca-a643-0f53d605b6ca)

  Example : Select account that has over $800 balance from "Brighton" branch.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a84e5fa5-cf42-4ac8-b536-b633f8eae51d)

  This is the concept of select algebra. You can use select algebra to get the row line of data.

  ![image-20231008174349992](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008174349992.png)

- Project : Create new relation with attribute A1, A2, ..., Ar from relation r.

  ![image-20231008174800107](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008174800107.png)

  Example : Account Number and Balance from Account table?

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d76a51a4-ff6e-4e9f-b1f9-22a44996982a)

  Example : Account Number and Balance that has over $600 on balance from Account table?

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/58903b9c-4775-4dd7-ad64-3f66ff67d107)

  

  Below is the concept of project algebra. You can use project algebra to get the non-duplicated column data.

  <img width="327" alt="project" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/80cc94db-d5da-4531-a0c7-831b4783ed48" style="zoom:150%;" >

- Union : Create new relation where the records contained both relation r and relation s.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/28c7a8a0-505a-44e8-86db-edd1d31fed11)

  Example : All customer's name who use banks for borrowing and depositing.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4f69c5fa-cf42-4186-852f-133f0ff6c4da)

  Below is the concept of union algebra. Note that to use union algebra, you must set same numbers of attributes and attribute type for both relations.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/712536f8-2802-418f-906e-0302bf90ed54)

- Set Difference : Create new relation that relation r's records minus relation s's records.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/99dcc362-e9a6-47d0-baff-9a7924ffae21)

  Example : All customer's name who do deposit but not do borrow?

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d2f03e04-75a1-4886-a0f3-867ecdcc3bb6)

  Below is the concept of Set difference algebra. Note that to use Set difference algebra, you must set same numbers of attributes and attribute type for both relations.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/33afa5b3-6f0e-41b8-bc98-685fe920c8f0)

- Cartesian Product : Create new relation that all possible combinations with relation r and s. This is used for connect two relations that both has same attribute.

  ![image-20231008180104169](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008180104169.png)

  Example : All customer's name who borrowed from "Perryridge" branch?

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/178b4357-ba2d-4755-97d3-9956ff6819a6)

  Below is the concept of Cartesian Product.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b7999928-99ae-4c99-b050-be25720114a7)


- Set Intersection : Create new relation with all records that included both relation r and relation s.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7f459247-0e49-47a8-b452-57957dd5be52)

  Example : All customer's name that do both borrowing and depositing.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8208d7fb-d1a2-4dd3-880b-e4aac7f3c5d5)

- Join : Create new relation that combined by two relations with common attributes. There are some types of join algebra.

  - Natural Join : The algebra that combine two relation with common attributes.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c42719b2-2080-4983-a062-b7fa4c5bf41a)

    Example : The bank which customers are depositing living in Harrison?

    ![image-20231008202921017](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008202921017.png)

    Example : Find all customers who have both a loan and an account.

    ![image-20231008202945390](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008202945390.png)

    Below is the concept of Natural Join. You can find that Natural Join is similar on Cartesian Product with no duplicate values.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/2278b725-8b64-4d4d-a3aa-7ae6339cf879)

  - Theta Join : The natural join with conditional operator.

    ![image-20231008203419413](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008203419413.png)

  - Equi Join : The theta join which conditional operator is "=".

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a76b4acb-f942-421b-8dab-d9eaef255a53)

  - Outer Join : The extended natural join. If there is null value exists when natural join do, the outer join set that value with NULL. Let's see this with an example.

    - There are two relations : loan and borrower. I will combine these two relations with an one.

      ![image-20231008204028288](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008204028288.png)

    - Inner Join(Natural Join) results : 

      ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/a3bfaa20-032e-4af3-b15d-20b9d640f9e7)

    - Left Outer Join results :

      ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/cffc8f3a-5349-483b-9b3c-254c8138157d)

    - Right Outer Join results :

      ![image-20231008204227339](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008204227339.png)

    - Full Outer Join results : 

      ![image-20231008204241221](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008204241221.png)

- Division : Used for "For all" query. Get all records which relation s exists on relation r.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/52d382e6-df2c-431a-b898-86f2865cc761)

  Example : All customer's name who have accounts from all "Brooklyn" Banks.

  ![image-20231008204536802](C:\Users\yeosu\AppData\Roaming\Typora\typora-user-images\image-20231008204536802.png)

  Below is the concept of division algebra. You can easily understand with these picture.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/b86d6a89-bafc-471e-ba32-93023ab3564e)
