---
layout: post
title: "[JAVA]Chatper2. The basic syntax of JAVA"
subtitle: "The basic syntax of JAVA"
categories: main_category
tags: sub_category tag1 tag2 tag3
comments: false
---

## Introduction
> The contents of basic syntax of JAVA language.

- Contents
	- [The Basic Structure of JAVA Program](#the-basic-structure-of-java-program)
	- [Primitive Types of JAVA](#primitive-types-of-JAVA)
	- [The Usage for types](#the-usage-for-types)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## The Basic Structure of JAVA Program
---
Now, let's dive into JAVA language syntax. But, where do we start? JAVA has a lots of features, so it is difficult to learn JAVA in short time. So, let's start to see the basic form of JAVA program.

```java
package univ_study;

// This is class.
public class Hello {
	// JAVA program always start on "main" method.
	public static void main(String[] args) {
		int i = 20;
		char a;
		a = '?';
		System.out.println(a); // Print '?' in a console window
		System.out.println("Hello"); // Print "Hello" in a console window
	}
}
```

This is the basic form of JAVA. You don't need to understand these all of syntax now, we will look this code to find the pattern of the program.

All of the JAVA source code must follow these rules : 

- All program must start on `main` method. In specific, `public static void main(String[] args)` method starts all of JAVA program. we will see these syntax one by one in future. But now, only you need to know that truth.
- `main` method must be included in `class`. In specific, `public class Hello` class has main method.
- Then, write your code in `main` method. At the end of the sentences, you must write `;` to recognize that this is the end of the sentence.



## Primitive Types of JAVA
---
But, what does `int i = 20;` and  `char a;` means? `int` and `char` is one of the **variable** types. variable is the container you can put and get some data. Imagine you store an apple in a box. an apple matches on a data, and a box matches on a variable.

So, JAVA language has 8 primitive types.

- boolean : 1 byte size. you can store true or false values here.
- char : 2 bytes size. you can store one character (e.g. 'a', '0', '가') values here. all of the characters recognized unicode on JAVA, so all of these has 2 bytes size.
- byte : 1 byte size. you can store numeral values (e.g. 1, 100, 800) values here. Note that 1 and '1' is the different values. 1 means numeral values, and '1' means character values. So, 1 + 1 can be calculated to 2, but '1' + '1' **cannot be calculated**. It means write '1' and then '1', so the result will be "11".
- short : 2 bytes size. you can store numeral values here.
- int : 4 bytes size. you can store numeral values here.
- long : 8 bytes size. you can store a large numeral values here.
- float : 4 bytes size. you can store decimal values (e.g. 1.1, 0.789) values here.
- double : 8 bytes size. you can store more precious decimal values (e.g. 1.12345343, 0.4848888888) values here.



## The Usage for types
---
Let's see how to use these types above.

- At first, you can store data in variable.

  ```java
  int a = 10;
  int b;
  b = 10;
  char c = 'A';
  ```

- You can use this data by writing variable names.

  ```java
  System.out.println(a);
  System.out.println("The value of b is " + b);
  System.out.println(c);
  ```



## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  