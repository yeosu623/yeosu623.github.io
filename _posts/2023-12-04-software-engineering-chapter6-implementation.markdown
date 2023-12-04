---
layout: post
title: "[Software Engineering]Chapter6. Implementation"
subtitle: "software engineering implementation"
categories: dev
tags: softwareengineering implementation
comments: false
---

## Introduction
> Implementation meaning in software engineering.

- Contents
	- [What is implementation?](#what-is-implementation)
	- [Coding Style](#coding-style)
	- [Use Open Source?](#use-open-source)
	
## What is implementation?
---
Implementation means writing code or programming. It is the final stage of design, and implementation includes writing code, debugging, merging, testing, etc. Note that as many member join to write implementation, each members should follow their rules about writing code.

Good software code has follow these rules :

- Easy to read
- Good comments on code
- Simple structure for code
- Flexible to change
- Easy to maintain and reuse
- Execute for the intended features correctly

Also, there are some advanced tips :

- Readable is more important than optimize.
- Build architecture first
- Consider test coverage
- Keep code simple and stupid
- Use comment for secondary tool only
- Don't trust refactoring much
- Use automation tool if you can
- Enjoy your habit
- Learn new things on your free time



## Coding Style

---
Coding Conventions are a set of guidelines for a specific programming language that recommend programming style, practices, and methods for each aspect of a program written in that language. Standards may be enforced through code reviews or may simple be suggestions. For example, ISO/IEC 9899, gives a standard for C programming language.

Coding Style is a set of rules or guidelines used when writing the source code for a computer program. It is often claimed that following a particular programming style will help programmers to read and understand source code conforming to the style, and help to avoid introducing errors. Below is the basic rules for programming.

- Naming for variables and functions differently.
- Writing source code less than 200 lines in one source file.
- Writing single line of code less than 80 characters.
- Writing function code less than 70 lines.
- Align codes if a single sentences is written over 2 lines.
- Align indent for same levels of code.
- Comment the worker's name, initial date, purpose, etc.



## Use Open Source?
---

Many projects have dependency on open source there days. Before we use these open sources, we have to consider some aspects.

- Check whether the system is suitable on open source.
- Do our project based on open source, and implement what open source cannot give on our project.
- Continuously testing during implementation, because merging open source can give you many unexpected errors.
- Have to check the license. There are many variety of license, and check the condition to use the open source.
- Consider to automation tools to manage our project.
- Open source may have continuously updates, and we need to consider during doing project.
- Open source may be difficult to use, so the project manager must give the guideline for team members.



