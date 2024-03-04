---
layout: post
title: "[Database]Chapter7. Extended ER Model"
subtitle: "extended er model"
categories: dev
tags: database er model
comments: false
---

## Introduction
> The more deeper and extended concept of original ER model.

- Contents
	- [What is Extended ER Model?](#what-is-extended-er-model)
	- [Subclass and Superclass](#subclass-and-superclass)
	- [Specialization and Generalization](#specialization-and-generalization)
	- [Union Type](#union-type)
	
## What is Extended ER Model?
---
The Extended ER model or Enhanced ER model, EER, has more effective concept based on original ER model.

- Subclass and Superclass
- Specialization and Generalization
- Union Type
- Inheritance



## Subclass and Superclass
---
This concept is that divide the entity for multiple entities.

For employee entity, when it is divided by job, it can be divided by secretary, engineer, technician, etc. Every that entities is defined as employee's subclass, on the other way, employee entity is the superclass with their subclass.



## Specialization and Generalization
---
Specialization is the process that dividing subclass and superclass with specific criteria. For example, when employee is divided by secretary, engineer, technician, job type is the criteria for dividing. Note that specialization can be with several criteria.

Generalization is the contract to specialization. It is merging subclass for superclass. For example, when there are car, truck entity, they can be merged as vehicle entity. So, car and truck entity become subclass, and vehicle entity become superclass.



## Union Type
---
Union type is grouping the individual entities. The difference point between union type and generalization is **inheritance**. The subclass of generalization get attributes of superclass, but union type does not inherit attributes of superclass.



