---
layout: post
title: "[Software Engineering]Chapter7. software testing"
subtitle: "software testing"
categories: dev
tags: softwareengineering software testing
comments: false
---

## Introduction
> Software testing in an aspect of software engineering.

- Contents
	- [Terminologies](#terminologies)
	
	- [The Four Levels of Software Testing](#the-four-levels-of-software-testing)
	
	- [Types of testing, Black box vs White box](#types-of-testing-black-box-vs-white-box)
  
    
  
## Terminologies  
---
There are some confusing terminologies in software engineering, so we need to check them before to read this post.

- Error : difference between the actual output and the correct output. Measurement of the difference between the actual and ideal.
- Fault(Bug) : A condition(potential) that causes the software to fail. Manifestation of an error in program.
- Failure : The inability of a system to perform a required function. This is produced only when there is a fault.

And...

- Verification : The process of evaluating products of a development phase to find out whether they meet the specified requirements.
- Validation : The process of evaluating software at the end of the development process to determine whether software meets the customer expectations and requirements.

Also, most of the V&V(Verification & Validation) activities can be classified as static or dynamic.

- Static : This includes reviews, program proving, and code reading. This **do not observe system behavior**, and not looking for system failures. Also, faults are directly detected.

- Dynamic : Testing (so called dynamic testing). **System behavior is observed**, determine the existence of failures, reveals the presence of faults, but not their absence. Note that no failure does not means no fault.

  Dynamic testing exercises a system or component, with defined inputs, capturing monitored outputs, and comparing outputs with specified or intended requirements. This purposes is to identify discrepancies between actual results and correct or expected behavior, and to provide high assurance of reliability, correctness, etc. Note that this activity does not includes debugging, that is the process of removing errors.



## The Four Levels of Software Testing
---
There are some stages of software testing.

1. Unit testing : The testing on minimum of software units, modules and functions.
2. Integration testing : Merging modules which passed unit testing. This stage tests the perfection of interface of modules.
3. System testing : Testing the entire system on actual hardware. This stage tests not only the feature of software, but also the performance.
4. Acceptance testing : Testing the entire system on user hardware. This stage tests like a demonstration of the system.
5. (Optional) Regression testing : The test that after correcting errors on the system. This stage performed for the operating system or updating system.

During the test, two kinds of problems to be discovered by testing.

- Invalid : The program does not do something it is supposed to do.
- Unexpected : The program does something it is not supposed to do.

Test cases must be written for invalid and unexpected, as well as valid and expected, input conditions. Test cases contain a description of input conditions, and description of expected results. Expected results should include the eye tends to see what it expects to see, thus a plausible but erroneous result can be easily interpreted as correct.



## Types of testing, Black box vs White box
---
There are many types of testing these days, and we will see the most important and most famous testing - black box testing and white box testing.



### Black box testing (Functional testing)

Black box testing does that test cases derived from examining the requirements specifications or user documents.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/85b9ea3b-843d-432e-a8e9-27f26091c378)

Test cases selected based on functional specification. That is, test data are developed from documents that specify the software's intended behavior.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/07f9715a-1ba9-4496-98ec-5d42db04cc34)

Black box Method contains : 

- Equivalence partitioning
- Boundary-value analysis
- Error guessing (Intuition and experience)
- Causes-effect graphing 

Let's see this method one by one.

1. Equivalence partitioning

   This is also known as input space partitioning. This divide the input space into equivalence class so that items in each equivalence class are treated the same. Sometimes, output space partitioning may also be considered, and **both valid and invalid equivalence classes are considered**. This need to pick at least one element from each equivalence class to test.

2. Boundary-value analysis

   This is a simple method with a high pay off in finding errors. Rather than selecting any element in an equivalence class, boundary-value analysis focuses on those elements near the boundary of the equivalence class. This need to consider boundaries in both input space and output space.

3. Error guessing

   This is based on intuition and experience. This stage tries to guess what the programmer may have overlooked, and make test cases for assumptions not mode explicit in the specifications.



### White box testing (Structural testing)

White box testing does that test cases derived from examining the actual code (software structure and implementation), the logic coverage.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/300530f4-2af6-4deb-9e42-9368c6741407)

Test cases selected based on design and implementation, and select paths to cover and generate test data to execute the path.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c58334ac-2396-4e4d-9b79-65f7a3292a62)

White box Method contains

- Statement Coverage
- Decision and Branch Coverage
- Condition Coverage
- Multiple Condition, Decision Coverage

Let's see this method one by one.

1. Statement Coverage

   This is the simplest from of logic coverage. Every statement in the program must be executed at least once. Note that this is the weakest logic coverage criterion, and have possibly undetected errors.

2. Decision and Branch Coverage

   Each branch and each entry point must be taken at least once. This stage tests these decision and branch coverages.

3. Condition Coverage

   A branch predicate may have more than one condition. This stage tests these condition coverages.

4. Multiple Condition, Decision Coverage

   At each branch statement, all feasible combinations of condition outcomes must be covered at least once. This stage tests both branch coverages and condition coverages.



