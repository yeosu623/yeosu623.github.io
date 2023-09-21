---
layout: post
title: "[Software Engineering]Chapter1. introduction"
subtitle: "software engineering introduction"
categories: dev
tags: softwareengineering
comments: false
---

## Introduction
> The introduction about software engineering and explain why it is needed.

- Contents
	- [What is software engineering?](#what-is-software-engineering)
	- [Why it is needed?](#why-it-is-needed)
	- [4C in Software Engineering](#4c-in-software-engineering)
	- [Principles of SE](#principles-of-se)
	
## What is software engineering?
---
Software is a computer programs and associated documentation.(e.g. install manual, user manual, develop document, etc.) Unlike other product making process, software is invisible, more complex, and update-able. Also, it cannot be fully automated, so software developers need to set a develop pattern for more efficient developing.

The **software engineering** term is first defined 50 years ago on NATO conference. Today, it is defined one of the scientific basis of computer science by four influential person and institution.

- The disciplined application of engineering, scientific, and mathematical principles and methods to the economical production of quality software. (Watts Humphrey)

- The systematic approach to the development, operation, maintenance, and retirement of software. (IEEE Computer Society)

- Multi-person construction of multi-version software. (D.L. Parnas)

- Design, building, and maintaining large software systems. (Ian Sommerville)

  

The basic software engineering process below here :

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8e8e85c9-cee5-4d22-8c6b-2d3c2dcbd4ba)

The important parts is **Requirements Analysis, Design, and Implementation and Maintenace.**

- **Requirements Analysis** do literally analysis customer's requirements into specific features.
- **Design** makes the big picture of program on architectural design, and draw specific diagram on detailed design.
- **Implementation** do write source code consisted on the design.
- **Maintenance** do update, maintenance, and fix bugs of released software.

Of course, if customers require new features on software, developers need to start the first level of this lifecycle, requirements analysis, design, implementation... and so on by this infinite circle.



## Why it is needed?
---
So, why we need to apply this methodology? Let's rewind your memory of your first programming class or book. You may learn C, JAVA, or Python programming language, and learn these syntax and implement some simple program like calculator, virtual vending machine, or text-based rogue-like game.

But, if you need to work on your team or company, you **ABSOLUTELY** don't work alone. your team members knows different background, design skill, and so so many things are not same on you. Furthermore, your team will make more more complex software than you made it alone. So, why not to learn and apply software engineering?



## 4C in Software Engineering 
---
There are four management in software engineering.

- Complexity : The software become more complex as the time pass. Today, some problem has over 373 packages and 2698 classes! So, software developer always has mindset about how can I reduce complexity, how can I manage it, and what are the methods or techniques to manage it.
- Change : Software is evolving like a life form. Thus, changes are inevitable. So, software developers always to be adaptive for environment changes like requirements, design, people, etc.
- Cost : According to Digital Aggregates Corporation, 67% of costs consumed during **Maintenance**, and 34% for others, from set requirements to release program. So, software developers must be concerned about Maintenance during all time on developing to reduce costs.
- Communication : All people does not have a deep understanding within software developing. Business managers and customers usually don't care about developing, so software developers need to explain easily for them. Also, usual software in not made by one person. As they need to work as a team, so good communication skill is needed.



## Principles of SE
---
- Rigor and Formality : Software is a program made by creative, engineering activity of programmer's experience and knowledge. Software developing must be get in time and cost, and that program must be understood on same meaning by everyone.
- Separation of concerns : Software developing is very complex, so it is need to be divided into many simple problems. For example, software developing process can be divided into Requirement analysis, Design, Implementation and Testing. Another example is software testing process, it can be divided into unit test, integrated test, and system test.
- Modularity : Program can be assembled of the pieces of individual features. It is helpful for readability and minimum side effect for change program.
- Abstraction : Show important aspect of features and hide detailed implementation. It is better for understand program directly and show the interest.
- Anticipation of changes : Changing software is inevitable. So developers must be ready for change by, for example, modulation.
- Generality : Software should be operated by variety of platform, system environment, users, etc. It should not depend on specific hardware.
- Incrementality : Software cannot be made at one time. Many developers should make small program repeatly to increase that size.
- Documentation : The information of software should be wrote in detail and architecture to help team members for effective developing and to notice updated features.

