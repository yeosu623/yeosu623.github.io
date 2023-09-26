---
layout: post
title: "[Software Engineering]Chapter2. Software dev life cycle"
subtitle: "software dev life cycle"
categories: dev
tags: softwareengineering
comments: false
---

## Introduction
> Learn the entire of software development life cycle.

- Contents
	- [What is software process model?](#what-is-software-process-model)
	- [Software process model](#software-process-model)
	- [Types of software process model](#types-of-software-process-model)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## What is software process model?
---
In 1988, one of the legendary software developer Boehm says "determines the order of stages involved in SW development and evolution, and to establish the **transition criteria** for progressing one stage to the next. These include completion criteria for the current stage plus choice criteria and entrance for the next stage."

Thus, a process model addresses the following SW project question :

- What shall we do next?
- How long shall we continue to do it?

Therefore, process models have a 2-fold effect :

- They provide **guidance** to software engineers on the order in which the various technical activities should be carried out within a project.
- They afford a framework for **managing development and maintenance**, in that they enable us to estimate resources, define intermediate milestones, monitor progress, etc.

Processes are important because industry cares about their intrinsic qualities, such as <u>uniformity of performance across different projects and productivity</u>, with the aim of improving time to market and reducing production costs.



## Software process model
---
It is a description of the sequence of activities carried out in an SE project, and the relative order of these activities. It is needed for build quality software products, like produce the products in factory.

There are some roles of software process model :

- Building basic framework : to construct basic architecture of the project
- Scheduling : to plan for the project
- Cost estimation : to set developing cost, furthermore, distribute variety of resources (e.g. human resource, cost, data)
- Communication : to set the standard for developing process.
- Standardization of terminology : to remove the ambiguous specific words.
- Clear understanding of development progress : to recognize the process of the project even if there are changes on the project.

**CASE(Computer-Aided Software Engineering) Tool** is the tool for automating tasks of software engineering. It gives developers the graphic tool when they write some document. For example, It can diagram easily for a resource flow or a business process. Or, famous IDE(e.g. Eclipse, Intellij, Visual Studio) also gives detailed error of the program for developers.



## Types of software process model
---
Let me introduce some famous software process model :

- Build and Fix : Develop software with **no detailed guideline or process**. Just write code and if there are some error, just write code and fix error, infinitely do until the program can be run.

  It can be did when just one programmer make a simple software. But, it must not to do when someone make a large software or when someone develop within a team. Because it is very hard to maintenance, hard to make a good software, cannot recognize where the process is, and especially, it's software got a lot of instant change, so it's architecture will be very awful.

- Waterfall model : It is followed by these process : **Requirement, Design, Implementation, Verification, and Maintenance**. Note that each stage are performed by different teams and cannot be back on previous stage. This is why it is named as waterfall model.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/4119ec94-571b-45f3-b72c-51ff0824db00)

  It is popularized in 1970's, of course this is one of the standard industrial practices these day. Below is the example about the documents of waterfall model.

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0ffb60f7-adbe-4036-8247-dee53ae06f4f)

  There are detailed stage of waterfall model :

  - Requirement : Identify the qualities required for the application. It must be stated what to do, <u>not how to do</u>. It's document contains the definition of the problem, alternative solutions and their expected benefits, and required resources, costs, and delivery date in each. Then, SRS(Software Requirements Specification) document is released.
  - Design : Propose a solution to the problem, and decompose the system into modules. It specify the relationships among modules, and design each module. Design can be divided into high-level language(preliminary, architectural), low-level(detailed), and user interface. Then, SDS(Software Design Specification) document is released.
  - Implementation : Transform design into code.
  - Verification : Test program. It has variety of testing - Unit testing, Integration testing, System testing, Acceptance testing, etc...
  - Maintenance : 



## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  