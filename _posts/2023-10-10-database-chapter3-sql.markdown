---
layout: post
title: "[Database]Chapter3. SQL"
subtitle: "chapter3 sql"
categories: dev
tags: database sql
comments: false
---

## Introduction
> Introduction to SQL and how to use it.

- Contents
	- [What is SQL?](#what-is-sql)
	- [Database Retrieval](#database-retrieval)
	- [Modify Database](#modify-database)
	- [Defining Table](#defining-table)
	- [Security for Database](#security-for-database)
  
## What is SQL?

---
SQL, Structured Query Language, is a complete data access and manipulation language. It is defined for relation DBMS and an industry standard for relational DBMS. It is also a non-procedural langauge, which has no statement for `go to, perform, do loop, open file, close file, end of file`.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3cd4ac38-81ca-4d2b-8738-0ce48ed8bfc7)

<center><b>With SQL, you can set group of data like above.</b></center>

SQL Functions has some type :

- Data Definition Language(DDL) 
  - CREATE : Define a new table, index, view
  - DROP : Remove a table, index, view definition
  - ALTER : Change the table schema
- Data Manipulation Language(DML)
  - SELECT : Perform relational query functions
  - INSERT : Place a new row into a table
  - UPDATE : Modify values in an existing row
  - DELETE : Remove a row from a table
- Data Control Language(DCL)
  - Authorization
    - GRANT : Give users' privileges
    - REVOKE : Remove users' privileges
  - Transaction Management
    - COMMIT : Commit transaction's effect
    - ROLLBACK : Abort transaction's effect
  - Integrity Constraint
    - TRIGGER : Define side effect of database update
    - ASSERTION : Define domain constraints



From now on, we will see how to use SQL one by one by writing these commands on your DBMS. Here are the sample database schema and tables for this practice :

- **SCHEMA**

<img width="408" alt="schema" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/83a6ee06-de4c-4a02-a11f-300401b742c8" style="zoom:150%;" >

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/cced8e57-2209-4a61-8d39-d3c74d74a4bc)

- **TABLES**

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/436857bb-7390-40c0-8417-7bbfd4bdfc3e)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7e61e46b-c9c6-449e-8da1-62e4cf5d7e7e)

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/5d039896-a686-4120-9a6b-f3fe28935b0d)

- **SQL Language for create table and insert data**

```SQL
create table DEPARTMENT (
	deptno number(2) not null primary key, 
	dname varchar2(20), 
	college varchar2(20), 
	budget number(8)
); 

create table PROFESSOR (
	pid number(3) not null primary key, 
	pname varchar2(10), 
	deptno number(2) references DEPARTMENT(deptno), 
	major varchar2(10), 
	hiredate date
);

create table STUDENT (
	sid number(4) not null primary key, 
	sname varchar2(10), 
	deptno number(2) references DEPARTMENT(deptno), 
	advisor number(3) references PROFESSOR(pid),
	gen varchar2(2),
	addr varchar2(10), 
	birthdate date, 
	grade number(3,2) check (grade between 0.0 and 4.5)
);
```

```sql
insert into department
	values(10, 'Computer', 'Engineering', 10000000);
insert into department
	values(20, 'Mechanical', 'Engineering', 20000000);
insert into department
	values(30, 'Physics', 'Sciences', 10000000);
insert into department
	values(40, 'Korean Language', 'Liberal Arts', 8000000);
insert into department
	values(50, 'General Education', 'Basic Studies', 8000000);

insert into professor
	values(101, 'Codd', 10, 'Database', to_date('1995-12-25', 'yyyy-mm-dd'));
insert into professor
	values(102, 'Turing', 10, 'Compiler', to_date('2002-06-11', 'yyyy-mm-dd'));
insert into professor
	values(201, 'Maxwell', 20, 'Automation', to_date('1998-03-01', 'yyyy-mm-dd'));
insert into professor
	values(202, 'Picasso', 20, 'CAD', to_date('2019-08-15', 'yyyy-mm-dd'));
insert into professor
	values(301, 'Gauss', 30, 'Magnetics', to_date('1997-04-20', 'yyyy-mm-dd'));
insert into professor
	values(302, 'Einstein', 30, 'Mechanics', to_date('2014-03-01', 'yyyy-mm-dd'));
insert into professor
	values(401, 'Heo Gyun', 40, 'Novel', to_date('2009-03-01', 'yyyy-mm-dd'));

insert into student
	values(1001, 'Minsu', 10, 101, 'M', 'Daegu', 
	to_date('2005-12-15', 'yyyy-mm-dd'), 3.93);
insert into student
	values(1002, 'Emily', 30, 302, 'F', 'Seoul', 
	to_date('2002-04-29', 'yyyy-mm-dd'), 3.25);
insert into student
	values(1003, 'Suji', 10, 102, 'F', 'Daegu', 
	to_date('1998-01-03', 'yyyy-mm-dd'), 4.17);
insert into student
	values(1004, 'Insung', 20, 201, 'M', 'Busan', 
	to_date('2007-10-10', 'yyyy-mm-dd'), 3.67);
insert into student
	values(1005, 'Daeho', 40, 401, 'M', 'Ulsan', 
	to_date('2006-04-04', 'yyyy-mm-dd'), 3.04);
insert into student
	values(1006, 'Smith', 10, 101, 'M', 'Seoul', 
	to_date('2001-11-05', 'yyyy-mm-dd'), 2.45);
insert into student
	values(1007, 'Maria', 20, 201, 'F', 'Gumi', 
	to_date('2002-09-23', 'yyyy-mm-dd'), 3.45);
insert into student
	values(1008, 'Gildong', 30, 302, 'M', 'Pohang', 
	to_date('2005-08-16', 'yyyy-mm-dd'), 3.31);
insert into student
	values(1009, 'Jane', 40, 401, 'F', 'Daegu', 
	to_date('2004-03-20', 'yyyy-mm-dd'), 2.08);
insert into student
	values(1010, 'Taehee', 20, 202, 'F', 'Busan', 
	to_date('2006-07-03', 'yyyy-mm-dd'), 4.41);
insert into student
	values(1011, 'Chilsu', 10, 102, 'M', 'Seoul', 
	to_date('1999-06-19', 'yyyy-mm-dd'), 2.88);
insert into student
	values(1012, 'Sarang', 10, 101, 'F', 'Ulsan', 
	to_date('2000-04-23', 'yyyy-mm-dd'), 3.68);
insert into student
	values(1013, 'Brown', 30, 302, 'M', 'Daegu', 
	to_date('1998-02-21', 'yyyy-mm-dd'), 1.75);
insert into student
	values(1014, 'Hyunsu', 20, NULL, 'M', 'Gumi', 
	to_date('2002-04-29', 'yyyy-mm-dd'), 2.03);
```

All right! After you insert these data into your database, you are ready to learn SQL. Are you ready to dive into SQL? Let's get into for that.



## Database Retrieval
---
In this section, we will see how to select the part of data we want.

#### Basic SQL Select

- Select specific columns : Select id and name from student table.

  ```sql
         SID SNAME     
  ---------- ----------
        1001 Minsu     
        1002 Emily     
        1003 Suji      
        1004 Insung    
        1005 Daeho     
        1006 Smith     
  .......
  ```

  ```SQL
  SELECT sid, sname
  FROM student;
  ```

- Select all columns : Select all from student table.

  ```sql
         SID SNAME          DEPTNO    ADVISOR GE ADDR       ....
  ---------- ---------- ---------- ---------- -- ---------- ....
        1012 Sarang             10        101 F  Ulsan      ....
        1013 Brown              30        302 M  Daegu      ....
        1014 Hyunsu             20            M  Gumi       ....
  ..........
  ```

  ```sql
  SELECT *
  FROM student;
  ```

- Select column with no duplicated : Select department number with no dupliated.

  ```sql
      DEPTNO
  ----------
          40
          30
          10
          20
  ```

  ```sql
  SELECT distinct deptno
  FROM student
  ```

- Select column with changed it's name : Select deptno and print as 'department'.

  ```sql
         SID SNAME      DEPARTMENT
  ---------- ---------- ----------
        1001 Minsu              10
        1002 Emily              30
        1003 Suji               10
        1004 Insung             20
        1005 Daeho              40
        1006 Smith              10
  .....
  ```

  ```sql
  SELECT sid, sname, deptno department
  FROM student;
  ```

- Combine columns : Combine id and name, and print as 'student' from student table.

  ```sql
  STUDENT                                           
  --------------------------------------------------
  1001Minsu
  1002Emily
  1003Suji
  1004Insung
  1005Daeho
  1006Smith
  ......
  ```

  ```sql
  SELECT sid||sname student
  FROM student;
  ```

- Sort column : Select id, name, deptno, grade from student table, and order by deptno.

  ```sql
         SID SNAME          DEPTNO      GRADE
  ---------- ---------- ---------- ----------
        1012 Sarang             10       3.68
        1006 Smith              10       2.45
        1003 Suji               10       4.17
        1001 Minsu              10       3.93
        1011 Chilsu             10       2.88
        1014 Hyunsu             20       2.03
  ......
  ```

  ```sql
  SELECT sid, sname, deptno, grade
  FROM student
  ORDER BY deptno;
  ```

- Sort column by descending : Select name, addr, birthdate from student table, and order by descending birthdate.

  ```sql
  SNAME      ADDR       BIRTHDAT
  ---------- ---------- --------
  Insung     Busan      07/10/10
  Taehee     Busan      06/07/03
  Daeho      Ulsan      06/04/04
  Minsu      Daegu      05/12/15
  Gildong    Pohang     05/08/16
  Jane       Daegu      04/03/20
  .......
  ```

  ```sql
  SELECT sname, addr, birthdate
  FROM student
  ORDER BY birthdate DESC;
  ```

- Sort two columns : Select deptno, name, grade from student table, and order by deptno first and order by grade inside deptno groups.

  ```sql
      DEPTNO SNAME           GRADE
  ---------- ---------- ----------
          10 Suji             4.17
          10 Minsu            3.93
          10 Sarang           3.68
          10 Chilsu           2.88
          10 Smith            2.45
          20 Taehee           4.41
  ......
  ```

  ```sql
  SELECT deptno, sname, grade
  FROM student
  ORDER BY deptno, grade DESC;
  ```

- Comparison Operator : Select females' id, name, deptno, addr.

  ```sql
         SID SNAME          DEPTNO ADDR      
  ---------- ---------- ---------- ----------
        1002 Emily              30 Seoul     
        1003 Suji               10 Daegu     
        1007 Maria              20 Gumi      
        1009 Jane               40 Daegu     
        1010 Taehee             20 Busan     
        1012 Sarang             10 Ulsan     
  ```

  ```sql
  SELECT sid, sname, deptno, addr
  FROM student
  WHERE gen = 'F';
  ```

- Comparison Operator2 : Select name, deptno, addr, which grade is over than 3.5

  ```sql
  SNAME          DEPTNO      GRADE
  ---------- ---------- ----------
  Minsu              10       3.93
  Suji               10       4.17
  Insung             20       3.67
  Taehee             20       4.41
  Sarang             10       3.68
  ```

  ```sql
  SELECT sname, deptno, grade
  FROM student
  WHERE grade > 3.5;
  ```

- Between Operator : Select name, grade, which grade is between 3.0 and 3.5

  ```sql
  SNAME           GRADE
  ---------- ----------
  Emily            3.25
  Daeho            3.04
  Maria            3.45
  Gildong          3.31
  ```

  ```sql
  SELECT sname, grade
  FROM student
  WHERE grade between 3.0 and 3.5;
  ```

- In Operator : Select id, name, grade, advisor from student table, which student advisor's number is 101, 201, or 401.

  ```sql
         SID SNAME           GRADE    ADVISOR
  ---------- ---------- ---------- ----------
        1001 Minsu            3.93        101
        1004 Insung           3.67        201
        1005 Daeho            3.04        401
        1006 Smith            2.45        101
        1007 Maria            3.45        201
        1009 Jane             2.08        401
        1012 Sarang           3.68        101
  ```

  ```sql
  SELECT sid, sname, grade, advisor
  FROM student
  WHERE advisor in (101, 201, 401);
  ```

- Like Operator : It is the wildcard character for char dataset.

  - `%` : zero or more character positions

  - `_` : one character position

  - Example

    - LIKE 'Kim%' : it is true, if string start on 'Kim'.
    - LIKE '%Kim%' : it is true, if string contains 'Kim'.
    - LIKE '%TH' : it is true, if string end with 'TH'.
    - LIKE '__TH%' : it is true, if string that 3rd and 4th position is 'TH'.
    - LIKE '%TH_' : it is true, if the previous position from at the end is 'TH'.

  - Practice : Select names which name starts on 's'.

    ```sql
    SNAME     
    ----------
    Suji
    Smith
    Sarang
    ```

    ```sql
    SELECT sname
    FROM student
    WHERE sname like 'S%';
    ```

  - Practice2 : Select names which name's length is 4.

    ```sql
    SNAME     
    ----------
    Suji
    Jane
    ```

    ```sql
    SELECT sname
    FROM student
    WHERE sname like '____';
    ```

- Logical Operator : Select id, name, addr, grade from student table, which grade is over than 3.5 and addr is 'Daegu' or 'Ulsan'.

  ```sql
         SID SNAME      ADDR            GRADE
  ---------- ---------- ---------- ----------
        1001 Minsu      Daegu            3.93
        1003 Suji       Daegu            4.17
        1012 Sarang     Ulsan            3.68
  ```

  ```sql
  SELECT sid, sname, addr, grade
  FROM student
  WHERE grade > 3.5 AND (addr = 'Daegu' OR addr = 'Ulsan');
  ```

- Not Operator : Select name, grade, which grade is not between 3.0 and 3.5

  ```sql
  SNAME           GRADE
  ---------- ----------
  Minsu            3.93
  Suji             4.17
  Insung           3.67
  Smith            2.45
  Jane             2.08
  Taehee           4.41
  ......
  ```

  ```sql
  SELECT sname, grade
  FROM student
  WHERE grade not between 3.0 and 3.5;
  ```

- Not Operator2 : Select name. addr, which addr is not start on 'D'.

  ```sql
  SNAME      ADDR      
  ---------- ----------
  Emily      Seoul     
  Insung     Busan     
  Daeho      Ulsan     
  Smith      Seoul     
  Maria      Gumi      
  Gildong    Pohang    
  ......
  ```

  ```sql
  SELECT sname, addr
  FROM student
  WHERE addr not like 'D%';
  ```

- Null : Select id, name, which student has no advisor.

  ```sql
         SID SNAME     
  ---------- ----------
        1014 Hyunsu    
  ```

  ```sql
  SELECT sid, sname
  FROM student
  WHERE advisor is null;
  ```

- lower(), upper() : make string to lowercase or uppercase.

  Select name, college from department table. Print name as lowercase, and print college as uppercase.

  ```sql
  LOWER(DNAME)         UPPER(COLLEGE)      
  -------------------- --------------------
  computer             ENGINEERING         
  mechanical           ENGINEERING         
  physics              SCIENCES            
  korean language      LIBERAL ARTS        
  general education    BASIC STUDIES      
  ```

  ```sql
  SELECT lower(dname), upper(college)
  FROM department;
  ```

- lpad() : print fields as "lpad(field, format length, 'blank char')".

  Print deptno, name, budget from department table on this format.

  ```SQL
  LPAD(DEPTN LPAD(DNAME,20,'*')   LPAD(BUDGET,20,'.') 
  ---------- -------------------- --------------------
          10 ************Computer ............10000000
          20 **********Mechanical ............20000000
          30 *************Physics ............10000000
          40 *****Korean Language .............8000000
          50 ***General Education .............8000000
  ```

  ```sql
  SELECT lpad(deptno, 10, ' '), lpad(dname, 20, '*'), lpad(budget, 20, '.')
  FROM department;
  ```

- substr() : "substr(string or field, pos, n)". is print string from pos to n. if n is null, print pos to the end of string.

  Print dname like this :

  ```sql
  DNAME                SUBSTR(DNAME,2)     SUB
  -------------------- ------------------- ---
  Computer             omputer             mpu
  Mechanical           echanical           cha
  Physics              hysics              ysi
  Korean Language      orean Language      rea
  General Education    eneral Education    ner
  ```

  ```sql
  SELECT dname, substr(dname, 2), substr(dname, 3, 3)
  FROM department;
  ```

- instr()

  - instr(field, 'char') : print index where char is available in field.
  - instr(field, 'char', num1, num2) : print index where num2-th char is available from num1.

  ```sql
  DNAME                INSTR(DNAME,'E') INSTR(DNAME,'E',2,2)
  -------------------- ---------------- --------------------
  Computer                            7                    0
  Mechanical                          2                    0
  Physics                             0                    0
  Korean Language                     4                   15
  General Education                   2                    4
  ```

  ```sql
  SELECT dname, instr(dname, 'e'), instr(dname, 'e', 2, 2)
  FROM department;
  ```

- length() : print string's length.

  Select deptno, name, and print length of deptno's data and print length of name's data.

  ```sql
      DEPTNO LENGTH(DEPTNO) DNAME                LENGTH(DNAME)
  ---------- -------------- -------------------- -------------
          10              2 Computer                         8
          20              2 Mechanical                      10
          30              2 Physics                          7
          40              2 Korean Language                 15
          50              2 General Education               17
  ```

  ```sql
  SELECT deptno, length(deptno), dname, length(dname)
  FROM department;
  ```

- translate() : translate(field, 'A', 'B') is find A in the field and changes as B.

  ```sql
  DNAME                TRANSLATE(DNAME,'E', TRANSLATE(DNAME,'IE'
  -------------------- -------------------- --------------------
  Computer             ComputEr             ComputEr            
  Mechanical           MEchanical           MEchanIcal          
  Physics              Physics              PhysIcs             
  Korean Language      KorEan LanguagE      KorEan LanguagE     
  General Education    GEnEral Education    GEnEral EducatIon   
  ```

  ```sql
  SELECT dname, translate(dname, 'e', 'E'), translate(dname, 'ie', 'IE')
  FROM department;
  ```

- round() : round(field or number, round decimal) do rounds number.

  ```sql
  ROUND(45.923,1) ROUND(45.923) ROUND(45.323,-1) ROUND(GRADE,1)
  --------------- ------------- ---------------- --------------
             45.9            46               50            3.3
             45.9            46               50            3.3
             45.9            46               50            1.8
  ```

  ```sql
  SELECT round(45.923, 1), round(45.923), round(45.323, -1), round(grade, 1)
  FROM student
  WHERE deptno=30;
  ```

- power() : power(field or number, power number) do powers number.

  ```sql
       GRADE POWER(GRADE,2) POWER(50,5)
  ---------- -------------- -----------
        3.25        10.5625   312500000
        3.31        10.9561   312500000
        1.75         3.0625   312500000
  ```

  ```sql
  SELECT grade, power(grade, 2), power(50, 5)
  FROM student
  WHERE deptno = 30;
  ```

- sqrt() : sqrt(field or number) do square root for number.

  ```sql
       GRADE SQRT(GRADE)   SQRT(40)
  ---------- ----------- ----------
        3.25  1.80277564 6.32455532
        3.31  1.81934054 6.32455532
        1.75  1.32287566 6.32455532
  ```

  ```sql
  SELECT grade, sqrt(grade), sqrt(40)
  FROM student
  WHERE deptno = 30;
  ```

- sign() : check sign. if input < 0 then print -1, if input = 0 then print 0, if input > 0 then print 1.

  ```sql
       GRADE  GRADE-3.0 SIGN(GRADE-3.0)
  ---------- ---------- ---------------
        3.25        .25               1
        3.31        .31               1
        1.75      -1.25              -1
  ```

  ```sql
  SELECT grade, grade-3.0, sign(grade-3.0)
  FROM student
  WHERE deptno = 30;
  ```

- Calculate dates : SQL can calculate date type data. sysdate get current time,

  ```sql
  HIREDATE HIREDATE+7 HIREDATE-7 SYSDATE-HIREDATE
  -------- ---------- ---------- ----------------
  98/03/01 98/02/22   98/03/08         9353.35295
  14/03/01 14/02/22   14/03/08         3509.35295
  09/03/01 09/02/22   09/03/08         5335.35295
  ```

  ```sql
  SELECT hiredate, hiredate-7, hiredate +7, sysdate-hiredate
  FROM professor
  WHERE hiredate like '%01';
  ```

- months_between() : months_between(date1, date2) prints month length between two dates.

  ```sql
  MONTHS_BETWEEN(SYSDATE,HIREDATE)
  --------------------------------
                        333.495333
                        255.946946
                        307.269527
                        317.656623
  ```

  ```sql
  SELECT months_between(sysdate, hiredate)
  FROM professor
  WHERE months_between(sysdate, hiredate) > 200;
  ```

- add_months() : add_months(date1, num) adds num months to date1.

  ```sql
  HIREDATE ADD_MONTHS(HIREDATE, 3)
  -------- -----------------------
  95/12/25 96/03/25
  02/06/11 02/09/11
  98/03/01 98/06/01
  19/08/15 19/11/15
  ```

  ```sql
  SELECT hiredate, add_months(hiredate, 3)
  FROM professor
  WHERE deptno = 10 or deptno = 20;
  ```

- next_day() : next_day(date1, num) prints the num day of the week.

  (Sun = 1, Mon = 2, Tue = 3, Wed = 4, Thu = 5, Fri = 6, Sat = 7)

  ```sql
  HIREDATE NEXT_DAY
  -------- --------
  95/12/25 95/12/29
  02/06/11 02/06/14
  09/03/01 09/03/06
  ```

  ```sql
  SELECT hiredate, next_day(hiredate, 6)
  FROM professor
  WHERE deptno = 10 or deptno = 40;
  ```

- last_day() : last_day(date) prints the last day on that month.

  ```sql
  HIREDATE LAST_DAY
  -------- --------
  95/12/25 95/12/31
  02/06/11 02/06/30
  98/03/01 98/03/31
  19/08/15 19/08/31
  ```

  ```sql
  SELECT hiredate, last_day(hiredate)
  FROM professor
  WHERE deptno = 10 or deptno = 20;
  ```

  Practice : print years of work for professor who are belonging to department number 20.

  ```sql
         PID PNAME      HIREDATE YEARS_OF_WORK
  ---------- ---------- -------- -------------
         201 Maxwell    98/03/01            25
         202 Picasso    19/08/15             4
  ```

  ```sql
  SELECT pid, pname, hiredate, trunc((sysdate-hiredate)/365) years_of_work
  FROM professor
  WHERE deptno = 20;
  ```

- to_char() : to_char(date, 'format') transform date to format to print.

  ```sql
  TO_CHAR(SYSDATE,'DAY,DDTHMONTHYY
  --------------------------------
  MONDAY, 09TH 10M 2023
  ```

  ```sql
  SELECT to_char(sysdate, 'DAY, DDTH MONTH YYYY')
  FROm sys.dual; /*temporary table*/
  ```

  ```sql
  TO_CHAR(SYSDATE, 'HH:MI:SS')
  ----------------------------
  08:58:43
  ```

  ```sql
  SELECT to_char(sysdate, 'HH:MI:SS')
  FROm sys.dual; /*temporary table*/
  ```

- to_date() : to_date(date, 'format') transform date to format.

  ```sql
         PID PNAME      HIREDATE
  ---------- ---------- --------
         102 Turing     02/06/11
  ```

  ```sql
  SELECT pid, pname, hiredate
  FROM professor
  WHERE hiredate = to_date('2002-06-11', 'yyyy-mm-dd');
  ```

- decode() : decode(field, cond1, cond1 true value, cond2, cond2 true value, false value) check if-else condition and print it's true and false value.

  ```sql
  SNAME          DEPTNO DECODED
  ---------- ---------- -------
  Minsu              10 CE     
  Emily              30 NOT Eng
  Suji               10 CE     
  Insung             20 ME     
  Daeho              40 NOT Eng
  Smith              10 CE     
  Maria              20 ME     
  ........
  ```

  ```sql
  SELECT sname, deptno, decode(deptno, 10, 'CE', 20, 'ME', 'NOT Eng') DECODED_DEPT
  FROM student;
  ```

- AVG() : avg(field) print average value in field.

  ```sql
  AVG(GRADE)
  ----------
        3.15
  ```

  ```sql
  SELECT avg(grade)
  FROM student;
  ```

- MIN() : min(field) print minimum value in field.

  ```sql
  MIN(GRADE)
  ----------
        2.03
  ```

  ```sql
  SELECT min(grade)
  FROM student
  WHERE deptno = 20;
  ```

- COUNT() : count(field) print number of field values.

  ```sql
    COUNT(*)
  ----------
           5
  ```

  ```sql
  SELECT count(*)
  FROM student
  WHERE deptno = 10;
  ```

- GROUP BY : it is used for group records in field. it must be used in front of where condition.

  ```sql
      DEPTNO AVG(GRADE)
  ---------- ----------
          30       2.77
          40       2.56
          10      3.422
          20       3.39
  ```

  ```sql
  SELECT deptno, avg(grade)
  FROM student
  GROUP BY deptno; /*avg will be performed on deptno groups.*/
  ```

- HAVING : it is used for search groups(made by GROUP BY) that specific condition is matched.

  ```sql
      DEPTNO AVG(GRADE)
  ---------- ----------
          10      3.422
          20       3.39
  ```

  ```sql
  SELECT deptno, avg(grade)
  FROM student
  GROUP BY deptno
  HAVING count(*) > 3;
  ```

- Subquery : the SQL language that combined two query into one.

  Example : Select name, deptno, grade from student table, which the student has the highest grade.

  ```sql
  SNAME          DEPTNO      GRADE
  ---------- ---------- ----------
  Taehee             20       4.41
  ```

  ```sql
  SELECT sname, deptno, grade
  FROM student
  WHERE grade = (select max(grade) from student);
  ```

  Example2 : Select name, grade, deptno from student table, which the student's grade is higher than the lowest grade in deptno 40.

  ```sql
  SNAME           GRADE     DEPTNO
  ---------- ---------- ----------
  Taehee           4.41         20
  Suji             4.17         10
  Minsu            3.93         10
  Sarang           3.68         10
  Insung           3.67         20
  ......
  ```

  ```sql
  SELECT sname, grade, deptno
  FROM student
  WHERE grade > any(select grade from student where deptno = 40)
  ORDER BY grade DESC;
  ```

  Example3 : Select name, grade, deptno from student table, which the student's grade is higher than the highest grade in deptno 40.

  ```sql
  SNAME           GRADE     DEPTNO
  ---------- ---------- ----------
  Taehee           4.41         20
  Suji             4.17         10
  Minsu            3.93         10
  Sarang           3.68         10
  Insung           3.67         20
  Maria            3.45         20
  ......
  ```

  ```sql
  SELECT sname, grade, deptno
  FROM student
  WHERE grade > all(select grade from student where deptno = 40)
  ORDER BY grade DESC;
  ```

  Example4 : Select name, grade, deptno from student table, which has the highest grade in each department.

  ```sql
  SNAME           GRADE     DEPTNO
  ---------- ---------- ----------
  Gildong          3.31         30
  Daeho            3.04         40
  Suji             4.17         10
  Taehee           4.41         20
  ```

  ```sql
  SELECT sname, grade, deptno
  FROM student
  WHERE (grade, deptno) in (select max(grade), deptno from student group by deptno);
  ```

  Example5 : Select deptno, average of grade from student table, which the department's average grade is higher than department 30's average grade.

  ```sql
      DEPTNO AVG(GRADE)
  ---------- ----------
          10      3.422
          20       3.39
  ```

  ```sql
  SELECT deptno, avg(grade)
  FROM student
  GROUP BY deptno
  HAVING avg(grade) > (select avg(grade) from student where deptno = 30);
  ```

  Example6 : Select id, name, deptno, grade from student table, which has the highest grade in Engineering College.

  ```sql
         SID SNAME          DEPTNO      GRADE
  ---------- ---------- ---------- ----------
        1010 Taehee             20       4.41
  ```

  ```sql
  SELECT sid, sname, deptno, grade
  FROM student
  WHERE grade =
  (select max(grade) from student where deptno in
  (select deptno from department where college = 'Engineering'));
  ```

  Example7 : Select name, deptno, grade from student table, which has the lower grade than the average grade of his/her department.

  ```sql
  SNAME          DEPTNO      GRADE
  ---------- ---------- ----------
  Smith              10       2.45
  Chilsu             10       2.88
  Hyunsu             20       2.03
  Brown              30       1.75
  Jane               40       2.08
  ```

  ```sql
  SELECT sname, deptno, grade
  FROM student s
  WHERE grade < (select avg(grade) from student where deptno = s.deptno)
  ORDER BY deptno;
  ```

  Example8 : Select name, deptno, major from professor table, which has the student for advise.

  ```sql
  PNAME          DEPTNO MAJOR     
  ---------- ---------- ----------
  Codd               10 Database  
  Turing             10 Compiler  
  Maxwell            20 Automation
  Picasso            20 CAD       
  Einstein           30 Mechanics 
  Heo Gyun           40 Novel     
  ```

  ```sql
  SELECT pname, deptno, major
  FROM professor p
  WHERE exists(select sid from student where advisor = p.pid)
  ORDER BY deptno;
  ```



#### Join

SQL Join is same as Join algebra. Like Join algebra, SQL Join has natrual join, inner join, and outer join.

Join is used for connect records by same attributes on different tables.

- Join

  Example : Select id, student name, department name from student table and department table.

  ```sql
         SID SNAME      DNAME               
  ---------- ---------- --------------------
        1001 Minsu      Computer            
        1002 Emily      Physics             
        1003 Suji       Computer            
        1004 Insung     Mechanical          
        1005 Daeho      Korean Language     
        1006 Smith      Computer           
  .......
  ```

  ```sql
  SELECT sid, sname, dname
  FROM student, department
  /*connect two tables by same attributes*/
  WHERE student.deptno = department.deptno;
  ```

  Example2 : Select id, deptno, college from student table and department table.

  ```sql
         SID     DEPTNO COLLEGE             
  ---------- ---------- --------------------
        1001         10 Engineering         
        1002         30 Sciences            
        1003         10 Engineering         
        1004         20 Engineering         
        1005         40 Liberal Arts        
        1006         10 Engineering         
  ```

  ```sql
  SELECT sid, s.deptno, college
  FROM student s, department d
  WHERE s.deptno = d.deptno;
  ```

  Example3 : Select the student's id, name, deptno, grade, which has the highest grade on Engineering college.

  ```sql
         SID SNAME          DEPTNO      GRADE
  ---------- ---------- ---------- ----------
        1010 Taehee             20       4.41
  ```

  ```sql
  SELECT sid, sname, s.deptno, grade
  FROM student s, department d
  WHERE s.deptno = d.deptno AND college = 'Engineering'
  AND grade = 
  (select max(grade) from student where deptno in
  (select deptno from department where college = 'Engineering'));
  ```

  Example4 : Select the student's name, department name, advisor's name and grade, which his/her grade is over than 3.5

  ```sql
  SNAME      DNAME                PNAME           GRADE
  ---------- -------------------- ---------- ----------
  Minsu      Computer             Codd             3.93
  Sarang     Computer             Codd             3.68
  Suji       Computer             Turing           4.17
  Insung     Mechanical           Maxwell          3.67
  Taehee     Mechanical           Picasso          4.41
  ```

  ```sql
  SELECT sname, dname, pname, grade
  FROM student s, department d, professor p
  WHERE s.deptno = d.deptno
  AND s.advisor = p.pid
  AND grade >= 3.5;
  ```

  Example5 : Select students' name which they have the same birthdate each other.

  ```sql
  SNAME      SNAME      BIRTHDAT
  ---------- ---------- --------
  Emily      Hyunsu     02/04/29
  ```

  ```sql
  SELECT s.sname, t.sname, s.birthdate
  FROM student s, student t
  WHERE s.birthdate = t.birthdate
  AND s.sid < t.sid;
  ```

- Outer Join : extended join. If you need to be print informations with join algebra but there are no connection data for join algebra, you can use "outer join" to print only informations by connecting with null data.

  Example : Select department number, department name, professor name by each department, except department 20.

  ```sql
  /* Without Outer Join */
  
      DEPTNO DNAME                PNAME     
  ---------- -------------------- ----------
          10 Computer             Codd      
          10 Computer             Turing    
          30 Physics              Gauss     
          30 Physics              Einstein  
          40 Korean Language      Heo Gyun  
  /* there aren't deptno 50 information, because there are no professor in deptno 50. */
  ```

  ```sql
  SELECT d.deptno, dname, pname
  FROM department d, professor p
  WHERE d.deptno = p.deptno AND d.deptno != 20;
  ```

  ```sql
  /* With Outer Join */
  
      DEPTNO DNAME                PNAME     
  ---------- -------------------- ----------
          10 Computer             Codd      
          10 Computer             Turing    
          30 Physics              Gauss     
          30 Physics              Einstein  
          40 Korean Language      Heo Gyun  
          50 General Education              
  ```

  ```sql
  SELECT d.deptno, dname, pname
  FROM department d, professor p
  WHERE d.deptno = p.deptno(+) AND d.deptno != 20;
  
  /* When join is operated, attach (+) symbol to the table that has no data.*/
  ```



#### Set Operation

- Union : union two sets.

  ```sql
  ADDR      
  ----------
  Ulsan
  Daegu
  Pohang
  Seoul
  ```

  ```sql
  SELECT addr
  FROM student
  WHERE deptno = 30
  UNION
  SELECT addr
  FROM student
  WHERE deptno = 40;
  ```

- INTERSECT : intersect two sets.

  ```sql
  ADDR      
  ----------
  Daegu
  ```

  ```sql
  SELECT addr
  FROM student
  WHERE deptno = 30
  INTERSECT
  SELECT addr
  FROM student
  WHERE deptno = 40;
  ```

- MINUS : delete common records from front set by rear set.

  ```sql
  ADDR      
  ----------
  Pohang
  Seoul
  ```

  ```sql
  SELECT addr
  FROM student
  WHERE deptno = 30
  MINUS
  SELECT addr
  FROM student
  WHERE deptno = 40;
  ```

  

## Modify Database
---
There are some SQL language to change data on database : INSERT, UPDATE, and DELETE.

- INSERT : insert new records to the database.                              

  ```sql
  INSERT INTO department
  VALUES (60, 'Statistics', 'Sciences', 30000000);
  
  INSERT INTO department(deptno, dname)
  VALUES (70, 'Philosophy');
  
  INSERT INTO department
  VALUES (80, 'Industrial Design', null, null);
  ```

  When you need to insert time and date information, you can use TO_DATE() function.

  ```sql
  INSERT INTO student
  VALUES (2000, 'John', 10, 101, 'M', 'London',
  TO_DATE('2001/06/24', 'YYYY/MM/DD'), 3.67);
  ```

  You can duplicate some data from one table to the another.

  ```sql
  /* Assume d10student table is already created. */
  
  INSERT INTO d10student(sid, sname, addr, grade)
  SELECT sid, sname, addr, grade
  FROM student
  WHERE deptno = 10;
  ```

- UPDATE : modify  some records what you want.

  ```sql
  UPDATE student
  SET deptno=10, addr='Daegu', grade=3.89
  WHERE sname = 'Taehee';
  ```

  Example : Increase database department's budget to the highest of the other departments.

  ```sql
  UPDATE department
  SET budget = (SELECT max(budget) FROM department)
  WHERE deptno in (SELECT deptno FROM professor WHERE major = 'Database');
  ```

- DELETE : delete some records what you want.

  ```sql
  DELETE FROM student
  WHERE deptno = 20;
  ```

  Example : Remove the department that has no student.

  ```sql
  DELETE FROM department
  WHERE deptno NOT IN (SELECT DISTINCT deptno FROM student);
  ```



## Defining Table
---
In this section, we will see how to create and modify, and delete table briefly.

You don't need to learn handle table right now, because this is very complex work and if you need to make table, you just refer the guide and follow it. So, I will just introduce what SQL language is available to handle table.

- CREATE : create table with your desired attributes.

  ```sql
  CREATE TABLE STUDENT (
  SID 			Number(4) NOT NULL PRIMARY_KEY,
  SNAME 			VARCHAR(10) CHECK (Sname = initcap(Sname))
  				CONSTRAINT ST_Sname,
  DeptNo 			Number(2) REFERENCES Department(DeptNo)
  				ON DELETE CASCADE,
  Advisor 		Number(3) REFERENCES Professor(PID)
  				CONSTRAINT ST_Advisor,
  GEN 			VARCHAR(2),
  ADDR 			VARCHAR(10),
  BirthDate 		DATE CHECK (BirthDate <= SYSDATE),
  Grade 			Number(3, 2),
  NiNO 			CHAR(12) UNIQUE CONSTRAINT ST_Ni,
  );
  ```

- Creating a table from another :

  ```sql
  CREATE TABLE DEPT30(id, name, gender, grade)
  AS
  SELECT 	sid, sname, gen, grade
  FROM 	student
  WHERE	deptno = 30;
  ```

- Creating an Index : Indicating an records by desired attributes.

  ```sql
  Create Unique Index st_idx ON student(sid);
  Create Index name_idx ON student(sname, gen);
  ```

- DROP : Dropping a table loses all the data in it and all the indexes associated with it. Any VIEWs(we will see later) will remain, but they become invalid.

  Only the creator of the table or DBA can drop it.

  ```sql
  DROP TABLE STUDENT;
  DROP INDEX ST_IDX;
  ```

- ALTER : add or modify some attributes on the table.

  ```sql
  ALTER TABLE student ADD(telephone varchar(20));
  ALTER TABLE student MODIFY(addr varchar(20));
  ```



## Security for Database
---
In this section, we will see the authority for the database.

- GRANT : give some permission to the other.

  ```sql
  GRANT privileges ON table TO user;
  ```

  ```sql
  GRANT SELECT ON student TO ADAMS;
  GRANT UPDATE(Grade, Deptno) ON student TO ADAMS;
  GRANT INSERT, UPDATE ON student TO ADAMS, JONES;
  GRANT ALL ON student TO ADAMS;
  GRANT SELECT ON student TO ADAMS WITH GRANT OPTION;
  GRANT SELECT ON student TO PUBLIC;
  ```

- REVOKE : deprive a permission from the other.

  ```sql
  REVOKE privileges ON table FROM user;
  ```

  ```sql
  REVOKE SELECT ON student FROM ADAMS;
  REVOKE ALL ON student FROM ADAMS;
  REVOKE ALL ON student FROM ADAMS CASCADE;
  /*CASCADE command deprive all permissions from the anothers that ADAMS gave.
  ```

- VIEW : VIEW command makes virtual table for seeing only. VIEW table cannot be duplicated, stored, or modify data inside. As VIEW table restricting access to the database, it can be used for searching data.

  ```sql
  CREATE VIEW view-name AS SELECT statement;
  ```

  ```sql
  CREATE VIEW D30student(ID, Name, Dept, Grade)
  AS
  SELECT sid, sname, deptno, grade
  FROM student
  WHERE deptno = 30;
  ```

  ```sql
  DROP VIEW view-name;
  ```

  ```sql
  DROP VIEW D30student;
  ```

  But, VIEW table can be modified on specific condition.

  - DELETE is prohibited if the view contains :
    - JOIN condition
    - GROUP BY clause
    - DISTINCT command
  - UPDATE is prohibited if the view contains :
    - Any of the above
    - Columns defined by expressions (ex : Grade * 100 / 4.5)
  - INSERT is prohibited if the view contains :
    - Any of the above
    - Any NOT NULL columns are not selected by view

  In conclusion, to SQL VIEW can be updatable, it must be :

  - Only one relation on from clause
  - Only attribute names on select clause. No expression, sum, or distinct.
  - attributes excluded on select clause must be nullable.
  - No GROUP BY and HAVING clause.

  So, D30student VIEW is updatable if nullable condition is satisfied.

  

  But, there are some problem when insert/update for D30student VIEW table - it can be updatable, but cannot see the updated result!

  To solve this problem : add `with check option` at the end. But when you insert some data `with check option`, the data must be satisfied WHERE clause to insert and update.

  ```sql
  CREATE VIEW D30student(ID, Name, Dept, Grade)
  AS
  SELECT sid, sname, deptno, grade
  FROM student
  WHERE deptno = 30
  with check option;
  ```

  

  Plus, if you want the VIEW table cannot be updatable, you can add `with read only` at the end.

  ```sql
  CREATE VIEW D30student(ID, Name, Dept, Grade)
  AS
  SELECT sid, sname, deptno, grade
  FROM student
  WHERE deptno = 30
  with read only;
  ```

  

  