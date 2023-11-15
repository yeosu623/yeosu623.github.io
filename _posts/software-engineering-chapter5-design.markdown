---
layout: post
title: "[Software Engineering]Chapter5. Design"
subtitle: "software engineering design"
categories: dev
tags: softwareengineering design
comments: false
---

## Introduction
> The design process for software engineering.

- Contents
	- [What is Software Design?](#what-is-software-design)
	- [Types of design](#types-of-design)
	- [Design Concepts](#design-concepts)
	- [Software Architecture Model](#software-architecture-model)
	- [Software Design Quality](#software-design-quality)
  - [Characteristics of Good Design](#characteristics-of-good-design)
  - [Software Design Methods](#software-design-methods)
  
## What is Software Design?
---
A software design is a process to transform user requirements into some suitable form, which helps the programmer in software coding and implementation.

For assessing user requirements, an SRS document is created whereas for coding and implementation, there is a need of more specific and detailed requirements in software terms. The output of this process can directly be used into implementation in programming languages.

Software design is the first step, which moves the concentration from problem domain to solution domain. It tries to specify how to fulfill the requirements mentioned in SRS.

So, why software design is important? Because, design gives the place where quality is fostered. Also, design provides us with representations of Software that can be assessed for quality.



## Types of design
---
There are largely two types of design.

- Top-down design(Preliminary design)
  - Architecture design : All architectures of system(all system has its several subsystem)
  - Data design : Data structures and Database structures
  - UI design : User Interface design for give users comfortable uses.
- Bottom-up design
  - Represent detailed pseudo-code for every module.
  - Write for interface, which has description, data structure, variables type and name, etc.



## Design Concepts

---
There are basic rules for design.

- Abstraction : To focus for solving problem, ignore detail and concentrate on comprehensive informations.
- Stepwise refinement(decomposition) : Use for top-down design. Divide features into small units more and more.
- Modularization : It is a technique to divide a software system into multiple discrete and independent modules, which are expected to be capable of carrying out tasks independently. 
- Information hiding : Design decision should be hidden from the rest of the system to prevent unintended coupling.



## Software Architecture Model
---
There are some types of software architecture model.

- Repository model : Manage main data from repository. The repository has several subsystem to access main data. It is useful to handle large data, such as a bank.

- Client-Server model : It is a network distributed system. Data and its handling system is distributed both clients and servers, so it is useful for the system that has a lot of subsystem.

- Layering model : Features is placed in several layers independently. Generally, Lower layer places server and database, and Upper layer places client and application.

- Model/View/Controller Model(MVC Model) : It is data-centralized design. Because each features divided independently, each features doesn't affect other features.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ec0b1978-4c96-4069-a3af-585b5c92943d)

  - Model : Handle all data and its logic. It just give respond for a request.
  - View : UI Interface.
  - Controller : Handle view and model in middle. Give request from view to model, and respond from model to view for giving data.

- Pipe and Filter Model : Filter handle input data and output a data stream. This model has input and output, and there are data handling filters in middle.



## Software Design Quality
---
Good design helps easy maintenance. It is strongly related on adaptability, which is **high cohesion and low coupling**.

- **Cohesion** : The measure of strength of the association of elements within a module. There are levels of cohesion : Coincidental, Logical, Temporal, Procedural, Communicational, Sequential, and Functional. Functional cohesion is the best quality. It means that one module operates for only one activity or only one purpose.
- **Coupling** : The measure of the interdependence of one module to another. Low coupling minimize ripple effect, and there are levels of coupling : Content, Common, Control, Stamp, and Data. Data coupling is the best quality. It means that  All modules must give and get data through arguments and parameters, so it guarantee the complete independent modules and minimize ripple.



## Characteristics of Good Design

---





## Software Design Methods

---

