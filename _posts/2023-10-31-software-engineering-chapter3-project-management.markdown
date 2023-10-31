---
layout: post
title: "[Software Engineering]Chapter3. Project Management"
subtitle: "project management"
categories: dev
tags: softwareengineering
comments: false
---

## Introduction
> Learn how manage the projects of software developing in companies.

- Contents
	- [Definition of Project Management](#definition-of-project-management)
	- [Cost Estimation for Software](#cost-estimation-for-software)
	- [Scheduling](#scheduling)
	- [Risk Analysis](#risk-analysis)
	- [Project Organization](#project-organization)
  
## Definition of Project Management
---
Project Management is creation and maintenance of an internal environment in an enterprise where individuals, working together in groups, can perform efficiently and effectively toward the attainment of group goals.

There are 5 phases of project management : Initiation and Conception, Planning, Launch and Execution, Monitoring and Control, Project Closure.

- Project Initiation and Conception : Recognize business needs, goals, and developing requirements. This is the first activity of software development, the team define exactly what will we made and set the scope.

  After define the problem, feasibility analysis is need for economic viewpoint and technical viewpoint, to determine whether this project can be going to or not.

  One thing need to be considered is legal feasibility. There are Intellectual Property Right and Computer Program Protection Act to block copying software, so need to be careful if the company don't want to be sued.

- Project planning : Consider all about the project in this phase. Set scope for project, estimate the schedule and cost, estimate results, etc. Without planning, much more costs will be used for maintenance.

- Project execution : develop software in a range of planning.

- Project monitoring and control : monitor project during development.

- Project closure : celebrate with team members.

It seems to easy for developing software in a team, but there are many fails occurred by many reasons. Most of the reason is **unambiguous requirement**, **lack of understanding for user environment**, **lack of skills for project management**. Surprisingly, lack of skills for developing doesn't affect much for fail, because there are a lot of information to develop software.



## Cost Estimation for Software
---
Have you thought about how much is your software? How to determine the cost for the software?

Unlike the other product, software is not visual, and its process cannot be standardization. It is difficult in calculate clear development cost. But there are some estimation factors to affect software development costs :

- Programmer Skills
- Software Complexity
- Software Size
- Available Time : Note that the number of humans does not in proportion on developing time. One of the legendary developer, Boehm says "The maximum to decrease time on original planning is up to 75%.". It's not easy to decrease the planning time.
- Reliability Level
- Programming Language : Every developers is not familiar on every programming language. So it is needed to be considered.

So, how can estimate costs for software? There are some types to do that :

- Top-down Approach : Estimated by experts. It will have a high reliability, but it could be inaccuracy because it is set by their experience.

- Bottom-up Approach : Estimated by activity units, estimated line of codes, or the effort per task. But this approach could be very inaccurate, so this isn't used much.

- Mathematical Estimation Techniques

  - COCOMO : Estimate the size of SW project(estimate LOC), then apply on the prepared formula depend on the type of software.

    It is processed on

    - Estimate LOC x Weights depend on type of software = Initial P/M
    - Initial P/M x Effort Adjustment Factor = P/M(Person/Month)
    - P/M x Constants = TDEV(Total DEVelopment time)

    To calculate TDEV, we need to get Initial PM first.

    - <u>Initial PM = a x (KDSI)^b</u>
    - KDSI is stand of Kilo Delivered Source Instruction.
    - KDSI of Organic(Simple) Project is generally less than 50 KDSI, and Semidetached(Complex) is 200~300, and Embedded Project is generally over 300.
    - a, b constant of Organic Project is 2.4, 1.05, Semidetached is 3.0, 1.12, Embedded is 3.6, 1.20, respectively.

    Next, we need to multiple EAF(Effort Adjustment Factor). EAF is multiple all the factors which affect on software developing.

    For example, if this factors on red box is required on this project, the EAF is 1.15 x 1.30 x 1.24 x 1.10 = 2.04.

    After we calculated EAF, we can get P/M values by <u>a x (KDSI)^b x EAF</u>.

    ![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e3a31d23-1e8c-4ba2-a745-9ab012668f59)

    Finally, we can get TDEV values by <u>2.5 x (PM)^c.</u>

    c constant is 0.38 on Organic(Simple) project, 0.35 on Semidetached Project, 0.32 on Embedded, respectively.

    That is all about getting TDEV value on COCOMO technique. But on real world, it is difficult to estimate LOC, and as the time pass, constant values need to be different to reflect on the real software developing process. So COCOMO is evolving on these days.

  - Function Point(FP) : Estimate costs based on the amount of business functionality, not on LOC(Lines Of Codes). Note that the coefficient can be changed in the future as the technology evolve.

    Unadjusted Function Point(UFP) is divided on..

    - Unadjusted Function Point = Data Functional Type + Transactional Function Type
      - Data Functional Type = (numbers of ILF x 7.5) + (numbers of EIF x 5.4)
        - ILF : Internal Logical File. It is the object for inserting, modifying, deleting by users. Ex) Database Table, File in inner system, class
        - EIF : External Interface File. It is the object for referencing on target software. It's object is created from another software.
      - Transactional Functional Type = (number of EI x 4.0) + (number of EO x 5.2) + (number of EQ x 3.9)
        - EI : External Input. insert data into and delete data from database.
        - EO : External Output. Show data through the arithmetic logic.
        - EQ : External inQurity. Search data from database and show for user.

    After Unadjusted Function Point(UFP) is calculated, it is need to be adjusted.
    
    - Development cost before adjustment is multiplied with UFP and Unit cost/UFP. In 2021, Unit cost/UFP is set as 553,114 won in Korea by The guide of SW business cost estimation.
    
    - Development cost after adjustment is formed by several affects.
    
      - Scale adjustment is the adjustment to apply the rate of development following by the business size has changed.
    
        The default formula is 0.4057 * (ln(FP) - 7.1978)^2 + 0.8878.
    
        In short, apply 1.2800 if FP is less than 500, and apply 1.1530 if FP is over 1.1530.
    
      - Adjustment by application type has some parts of it.
    
        - 'Connected by Another companies' Complexity Level. no connect is 0.88, 1~2 connect is 0.94, 3~5 is 1.00, 6~10 is 1.06, respectively.
        - Performance level. no requirement is 0.91, some requirement is 0.95, requirement on peak time is 1.00, requirement on all time is 1.05, rigid requirement is 1.09, respectively.
        - OS Compatibility. no requirement is 0.94, requirement on same OS is 1.00, requirement on similar OS is 1.06, requirement on foreign OS is 1.13, and rigid requirement is 1.19, respectively.
        - Security. It has encryption, checking web security, secure coding, defend personal information, etc. 1 requirement is 0.97, 2 requirement is 1.00, 3 is 1.03, 4 is 1.06, over 5 is 1.08, respectively.
    
      - Finally, Development cost after adjustment is calculated as '(Development cost before adjustment) x (Scale adjustment) x (Connected by Another companies Complexity level) x (Performance level) x (Os Compatibility) x (Security)'. It is the final cost for the program.



## Scheduling
---

After estimate costs, it's time to schedule the project. That means spread out all the works and show it by relation and orders. Specifically to write the schedule, it need to be included ID, Tasks, Days, Predecessor, Workers(R&R - Roles and Responsibilities), Status, etc.

WBS, Work Breakdown Structure, is the one for schedule the project. It is the layered structure divided by workouts for developing teams.

To represent WBS,

- Gantt chart(Time-Line Chart) : a type of bar chart that illustrates a project schedule, named after its inventor. Created by Henry Gantt.
- PERT chart(Program Evaluation and Review Techniques chart) : a type of chart that illustrates the relationship of tasks. The tasks contain the brief explanation and the duration of task. Note that the longest duration to complete the task is said as Critical Path.

The good points of WBS,

- Good communication tool between users and developers
- Good for visualization to project tasks, so it is useful for management.
- Good for unambiguous R&R(Roles & Responsibility)
- The basis for plan workers and a project.
- The basis for cost estimation.
- The standard for measuring and modifying one's performance.




## Risk Analysis
---
There are four basic step to risk analysis : Risk Identification, Risk Analysis, Risk Planning, and Risk Monitoring.

- Risk Identification : Literally, it is identify potential risks during the project. Remember the **<u>Brooks law : If the current project inputs new members for the project, the development duration can be more longer. Because they need to learn about the project, and communicate about it.</u>**
- Risk Analysis : Analysis the possibility and the impact for risks one by one.
- Risk Planning : Plan the solution when the risk is really happened.
- Risk Monitoring : Monitoring if the risk plan is realistic, and if the risk is really happened during the project.



## Project Organization
---
There are many roles for the project these days :

- Project Manager(PM) : Manage the project overall.
- Project Leader(PL) : Execute the project as the project leader.
- Team Leader(TL) : Execute the project as the team leader, when the project has many teams.
- Program Engineer(PE) : Developer.
- Configuration Manager(CM) : Manage the prototype results and change requirements.
- Quality Engineer(QE) : Check the results, review it, and test it.
- Liaison Group : Communicate with business groups.



