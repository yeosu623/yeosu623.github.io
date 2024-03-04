---
layout: post
title: "[Software Engineering]Chapter4. Requirement Engineering"
subtitle: "requirement engineering"
categories: dev
tags: softwareengineering requirement engineering
comments: false
---

## Introduction
> Understanding the requirements for software in detail.

- Contents
	- [Understanding The Requirements](#understanding-the-requirements)
	- [Requirements Engineering](#requirements-engineering)
	- [Specification Qualities](#specification-qualities)
	- [Nonfunctional Requirements](#nonfunctional-requirements)
	
## Understanding The Requirements
---
The ultimate purpose of software development is for satisfying users and clients with software. There are some aspects in detail :

- Time to Market : fast release for occupying market
- Flexibility : Adaptation for variable environments.
- Integration : Easy integrate with existed system.

Requirement analysis is the process of investigating and verifying your requirements for defining software requirements. This is very important of overall the entire development, because adding new features on existed software is very difficult and tasks a very long time.

But It is not easy to requirement analysis. The biggest problem is the user and client is not developer, so they don't have the domain about their software. Of course, the developer don't have a business domain as the client. **SO A LOT OF CONFLICT OCCURRED DURING THE PROJECT.** The worst problem is that client asks changing the requirements and adding new features continuously. But it is natural problem and not the client's fault, because they don't have development domain as the developer.

So, many SI company has a employee about requirement analyzer. Their role is that induce the client's complete description, and coordinating claims between stakeholders.



## Requirements Engineering
---
Requirements Engineering, RE, is emphasizes an iterative and cooperative process of

- analyze the problem (**gathering and analysis**)
- documents the resulting observations (**specification**)
- checking the accuracy of the understanding gained (**verification**)

More specifically,

- Requirements Elicitation (gathering and analysis) 

  - Understand the problem.

  - Face-to-Face method : interview, JAD

    - JAD, Joint Application Development, is the brainstorming discussion that is joined by project team, users, clients, and developers.

      Each person have a voice pairly to induce the requirements by each stakeholder. 5 days to do it in 3 week, generally.

  - Non Face-to-Face method : document analysis, survey, SNS

- Requirements Specification

  - identify the qualities required for the application. It has functional and nonfunctional both, and they must be stated **what to do**, not how to do.
  - Separate functional requirements into 3 view,
    - A model of data : Entity relationship diagrams, domain model
    - A model of function : Use case diagram, Data flow diagram
    - A model of control : Control flow diagrams, State machines, Petri nets, Sequence diagram.

- Requirements validation and verification
  - Validation : Testing final result with documents.
  - Verification : Testing next result with previous document.



## Specification Qualities
---
There are some checklist for requirement specification.

- Clear and understandable
- Unambiguous
- Consistent : Is a specification has no conflict, non-matched, or duplicated requirement?
- Complete : Is a specification doesn't omit content, not only the features, but also the performance or limitations?
- Verifiable : Is a specification helps to verity clearly that the system satisfies the requirement?
  - Wrong example : There will be no problem when a lot of person connect to our server.
  - Good example : There will be no problem when 10,000 person connect to our server.
- Easily changed : Is a specification can be easily changed? In other words, is the requirements is wrote independently?
- Traceable : Is a specification helps to trace the specific error on the system?



## Nonfunctional Requirements
---
These focuses on environment, constraint, and quality.

- Environment : hardware spec.
- Constraint : Software constraint. For example, this system must be developed with JAVA and be applied CBD developing method.
- Quality : Reliability, Security, Performance, Safety.
  - Reliability : trust to use the system. There is the term reliability rate, this means the percentage to guarantee the system operates perfectly.
  - Security : secure the system and the data.
  - Performance : This is not only operates the system perfectly, but also satisfy the customer's specific requirement. For example, searching books must be operated in 2 seconds.
  - Safety : the system must be safe to use, especially on embedded system.

