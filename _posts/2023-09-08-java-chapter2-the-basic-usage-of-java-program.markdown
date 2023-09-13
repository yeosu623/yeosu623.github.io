---
layout: post
title: "[JAVA]Chatper2. The basic usage of JAVA program"
subtitle: "The basic usage of JAVA program"
categories: dev
tags: java type variable if
comments: false
---

## Introduction
> The contents of basic usage of JAVA language.

- Contents
	- [The Basic Structure of JAVA Program](#the-basic-structure-of-java-program)
	- [Primitive Types of JAVA](#primitive-types-of-JAVA)
	- [The Usage for types](#the-usage-for-types)
	- [Input data](#input-data)
	- [Operators](#operators)
  - [If statement](#if-statement)
  
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

Plus, I introduce the most widely uses of non-primitive types. This exactly means `instance`, but this is too fast to explain it. I will explain it later, but first, just see which type is widely used.

- String : String means the sequence of characters. (e.g. "hello world!") To contain string type data, you just write `string` to do.
- Array : contain sequence data. (e.g. [1, 2, 3, 4]). We will see this later chapter.



## The Usage for types
---
Let's see how to use these types above.

- At first, you can store data to define a **variable** with type name.

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



## Input data
---
To input data, you need to import some library (pre-defined features) and write these source code. It has some important concept, but it is hard to understand now. So, let's write this source code and just over it.

```java
import java.util.Scanner;

public class InputData {
    public static void main(String[] args) {
        /* Create scanner instance. 
        'sc' is the reference variance name, so you can set name on your want.
        Scanner will divide the input value by blank or enter.
        */
        Scanner sc = new Scanner(System.in);
        
        String name = sc.next(); // Return next token with String type.
        int age = sc.nextInt(); // Return next token with Int type.
        double weight = sc.nextDouble(); // Return next token with double type.
        
        System.out.println("name : " + name);
        System.out.println("age : " + age);
        System.out.println("weight : " + weight);
    }
}
```



## Operators
---
Operators means arithmetic operators, like +, -, *, /, etc. We will see basic operators on this section.

| Operators             | features             |
| --------------------- | -------------------- |
| Increment, Decrement  | ++, --               |
| Arithmetic            | +, -, *, /, **%**    |
| Bit shift             | >>, <<, >>>          |
| Comparison            | >, <, >=, <=, ==, != |
| Bit operation         | &, \|, ^, ~          |
| Logical operation     | &&, \|\|, !          |
| Conditional operation | ? :                  |
| Assignment operation  | =, +=, -=, *=, /=    |

Let's see these operations one by one.

- Increment, Decrement : addition or subtraction variable's values by one.

  ```java
  int a = 1;
  int b;
  
  b = ++a; // Add 1 on variable PRIORITY when this code execute.
  b = a++; // Add 1 on variable LASTLY when this code execute.
  
  b = --a; // Subtract 1 on variable PRIORITY when this code execute.
  b = a--; // Subtract 1 on variable LASTLY when this code execute.
  ```

- Arthimetic : the basic arthimetic operations.

  ```java
  int a = 10;
  int b = 2;
  int result;
  
  result = a + b; // Addition
  result = a - b; // Subtraction
  result = a * b; // Multiplication
  result = a / b; // Division (See important note below)
  result = a & b; // Modulus operation. It results the rest of a division.
  
  /* Note that division result can be different depend on what you use on operand.
  If you divide Int by Int, the result comes by INT.
  For example, if you do 5 / 3, the result comes on 1, not on 1.666!!!!!!!!!
  
  To get the decimal points of the result, you should divide Float or Double at least one operand.
  For example, if you do '5 / 3.0', '5.0 / 3', or '5.0 / 3.0', the result comes on 1.666666. 
  */
  ```

- Bit Shift : Shift bits. But you may not use this operator when you are make application software.

- Comparison : normal comparison operator. `!=` means **not same**.

- Bit operation : literally bit operations. But you may not use these operator when you are make application software.

- Logical Operation : `&&, ||, and !` means AND, OR, and NOT, sequencely.

- Condition Operation : Output different values depends on condition. 

  ```java
  int a = 5;
  int b = 3;
  String result;
  
  result = (a > b) ? "a is bigger" : "b is bigger";
  /* AAA ? BBB : CCC;
  AAA : Condition section.
  BBB : Output this if condition is true.
  CCC : Output this if condition is false.
  */
  ```

- Assignment Operation : Do assign(`=`) and arithmetic operation at the same time.

  ```java
  int a = 1;
  a += 3; // The values of a become 4
  ```

  

## If statement

---

If statement makes condition for a program. Easy example, if you afford $1000, you can buy some normal office desktop computer, but if you afford $3000, you can buy a super fast gaming computer! So, let's see how to use if statement.

```java
import java.util.Scanner;

public class BuyComputer {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("How much you can afford for your computer? : ");
        int afford = sc.nextInt();
        
        if(afford == 1000)
            System.out.println("You bought normal office desktop computer.");
    }
}
```

But only `if` cannot give an option for not enough money. Then, you can use `then` statement for exclusive of if statement.

```java
import java.util.Scanner;

public class BuyComputer {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("How much you can afford for your computer? : ");
        int afford = sc.nextInt();
        
        if(afford == 1000)
            System.out.println("You bought normal office desktop computer.");
        else
            System.out.println("You don't have enough money!");
    }
}
```

So, how we can add an option for super-fast gaming computer? Just stack if-else statement to give another if statement option.

```java
import java.util.Scanner;

public class BuyComputer {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("How much you can afford for your computer? : ");
        int afford = sc.nextInt();
        
        if(afford == 1000)
            System.out.println("You bought normal office desktop computer.");
        else if(afford == 3000)
            System.out.println("You bought super fast gaming desktop computer!");
        else
            System.out.println("You don't have enough money!");
    }
}
```

Or you can nest if statement.

```java
import java.util.Scanner;

public class BuyComputer {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("How much you can afford for your computer? : ");
        int afford = sc.nextInt();
        boolean buy = true;
        
        if(afford == 1000) {
            if(buy == true) {
                System.out.println("You bought normal desktop computer.");
            }
        }
    }
}
```



