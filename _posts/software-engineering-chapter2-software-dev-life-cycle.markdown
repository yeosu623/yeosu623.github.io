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
  - Testing : Test program. It has variety of testing - Unit testing, Integration testing, System testing, Acceptance testing, etc...
  - Maintenance : The most costs and effort put in this phase. There are four types of maintenance in specific.
    - Corrective : 20%, fix bugs of the operating system after the software released.
    - Adaptive : 20%, to adapt software for new environment about hardware and OS.
    - Perfective : 60%, to perfect the released software by adding and upgrading features.
    - Preventive : change software for more effective future maintenance.
  - Other activities : Documentation, Verification(monitor the quality of the software at the end of each phase), Management(tailoring the process and defining policies)
  
  The waterfall model's property is **Linear, Rigid, and Monolithic**. All phases must be proceed on linear process, and all results of each phases are **frozen** before proceeding to the next. **NO CHANGES ALLOWED ON THE RESULTS OF PREVIOUS PHASE!** 
  
  Yes, the waterfall model helps for easy management, so it is suitable for the project with minimal changes. But as it is very rigid, so each phases must be performed after the previous steps are completed. It is not recommended for flexible project.
  
- Prototyping : It is the very opposite on waterfall model. Prototyping do make the very first version of software and changes it with clients. Clients asks the requirements for the prototype software and fetch it and do it again until clients satisfied. After clients makes the final requirements, then developers makes the final version of software for release.

  <img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e0210b69-243b-4574-b319-ac215dbbf0fb" alt="Phases-of-Prototyping-Model" style="zoom:67%;" />

  Prototyping model creates a requirements specification that fully reflects user needs through the repeated requirement definitions. So this model is mostly used for live-service games, because this model can fully apply with gamers' requirements. Also, it gives developers finding error early, and gives customers expecting the final results.

  Otherwise, this model has no formal process, so it is hard for estimate cost and resources, hard for management, hard for maintenance. And the worst is, **this model does not give the clear goal for you, so the project has lots of potential to fail.**

- Incremental & Iterative model : 

  ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/18cec5ab-0c9e-46aa-b641-403ae47af078)

  The combination of prototyping model and waterfall model. Developers make the prototypes within waterfall process model. So it gives better quality of prototype.

  This model's benefits are :

  - Provide the user with time to adjust to the new product.
  - Easy to accommodate changes.
  - Phased delivery does not require a large capital expenditure.

  This model's problems are :

  - Each additional build has to be incorporated into the existing structure.
  - May require more careful design (could be a benefit?)
  - Can easily degenerate into the build&fix model.

- Spiral model : 

  <img width="509" alt="spiral model" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/d13f23f3-9cb7-4d65-a150-0fc67599da72">

  This unique model seems to be very difficult, but you just start on 'Requirements plan, Life-cycle plan' in the very inner of the blue-line spiral.

  Following the blue line, you will see the Risk analysis, Prototype, Concept of Operation, and etc. The spiral has full developing process and has four types of management(written on red color) : Planning, Risk analysis, Engineering and Customer Evaluation.

  There are some examples of risk : 

  - Developer's transfer

  - Frequently changed requirements
  - Lack of costs and resources
  - Unexpected of costs and resources
  - Inexperienced team members
  - Less united teamwork
  - Lack of project management skills

  This model must analysis the expected risks carefully, so the rates of fail project is decreased. But, this model need to repeat developing, so the deadline of project can be delayed.
  
- V model : It is the extended version of waterfall model. V model is based on waterfall model, and added verification for each phases.

  ![V model](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7bdca56d-fa4d-4dbb-a8be-56147fb04294)

  It makes less error than waterfall model, but as this model based on waterfall model, it is hard to change the previous results.

- Agile software development : it is one of the most advanced software development model. In 2001, As the size of project goes bigger and larger, project managers starts to make the light-weight development process. Their goal is to balance the build-and-fix model and the detailed-specific-software model. It makes to declare the **Manifesto for Agile Software Development**.

  - **Individuals and Interactions** over processes and tools
  - **Working Software** over comprehensive documentation
  - **Customer Collaboration** over contract negotiation
  - **Responding to Change** over following a plan

  Agile software development has rapid responding on client's requirements and real-time problems. There are some specific models of agile software development.

  - **Extreme Programming(XP)** : Extreme programming emphasizes teamwork. Managers, customers, and developers are all equal partners in a collaborative team. And this model improves a software project in five essential ways : Communication, simplicity, feedback, respect, and courage.

    There are 10 to-do lists on extreme programming :

    - Incremental Planning : all planning must be selected on remaining time and priority.
    - Small Release
    - Simple Design
    - Test-first Development
    - Refactoring
    - Pair Programming : two programmers work together as an one programmer.
    - Collective Ownership : Every programmers can work on any code.
    - Continuous Integration
    - Sustainable Pace
    - On-site Customer

  - **Scrum** : Scrum is an agile framework for developing, delivering, and sustaining complex products, with an initial emphasis on software development.

  - **Dynamic Systems Development Method(DSDM)** : DSDM assumes that 80% of the solution can be developed in 20% of the time that it would take to produce the total solution. DSDM focuses on this 80%, leaving another 20% for later revisions.

  - **Lean** : this model is originated from Toyota Auto manufacturing practices. There are some main principles on this model :

    - Eliminating Waste
    - Amplifying Learning
    - Deciding as Late as Possible
    - Delivering as Fast as Possible
    - Empowering the Team
    - Build Quality In : build the environment for easy integration.
    - Optimize the Whole





## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  