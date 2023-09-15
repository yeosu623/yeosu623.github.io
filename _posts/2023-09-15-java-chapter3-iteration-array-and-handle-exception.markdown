---
layout: post
title: "[JAVA]Chpater3. Iteration, Array, and Handle Exception"
subtitle: "iteration, array, and handle exception"
categories: dev
tags: java iteration array exception
comments: false
---

## Introduction
> Let's see iteration, array, and how to handle exception in JAVA.

- Contents
	- [What is Iteration?](#what-is-iteration)
	- [Controls in Iteration](#controls-in-iteration)
	- [What is Array?](#what-is-array)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## What is Iteration?
---
Iteration makes something repeat with sequenced numbers. Imagine you need to count 1 to 100 and write it on paper. You need to write numbers one by one in real world, but computer can do that work very easily!

In java, there are three form of iteration.

- `for` statement : The most usage for iteration. You can use it for general iteration, or if you need a sequence numbers.

  ```java
  for(int i = 0; i < 10; i++) {
      System.out.print(i);
  }
  
  // result : 0123456789
  ```

  

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/608ce1c3-0391-4a2d-b347-99eb356605e7" alt="image" style="zoom:50%;" />

- `while` statement : Another form for iteration. You can use it if you need to control iteration with conditional statement.

  ```java
  int i = 0;
  while(i < 10) {
  	System.out.print(i);
      i++;
  }
  
  //result : 0123456789
  ```

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/f420d272-5015-4d0d-9142-f8d64eaf8835" alt="image" style="zoom:50%;" />

- `do-while` statement : A special iteration. You can use it if you need to run iteration one time at first.

  ```java
  int i = 0;
  do {
      System.out.print(i);
      i++;
  } while(i < 10);
  
  //result : 0123456789
  ```

  <img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/8d157062-61b6-4c38-8602-92d8d43dfd03" alt="image" style="zoom:50%;" />



Plus, iteration can be nested. But you need to be careful when you use nested iteration, because this can make problem slowly. Below example is print some multiplication results from 1x1 to 9x9.

```java
public class NestedLoop {
	public static void main(String[] args) {
		for(int i = 1; i < 10; i++) {
			for(int j = 1; j < 10; j++) {
				System.out.print(i + "x" + j + "=" + i*j);
				System.out.print("\t");
			}
			System.out.println();
		}
	}
}
```





## Controls in iteration
---
There are special statement to control iteration. You can use it when you need to jump or stop codes in some condition.

- `Continue` Statement : continue statement jumps the rest codes in iteration. You can use it when you need to skip some codes in desired condition.

```java
// sum of even numbers from 0 to 9.
int sum = 0;

for(int i = 0; i < 10; i++) {
    if(i % 2 == 1) // If number is odd number,
        continue; // skip the rest codes in iteration.
    sum += i; // Only added even numbers.
}
System.out.println("The sum of even numbers is " + sum);
```



- `Break` statement : break statement stop iteration immediately when this executed. You can use it when you need to get out iteration in desired condition.

```java
// sum numbers from 0 to 10.
int sum = 0;

for(int i = 0; i < 1000; i++) {
    sum += i;
    if(i == 10)
        break;
}
System.out.println("The sum from 1 to 10 is " + sum);
```



## What is Array?
---
Array is the format of sequenced variables of same type. It is made of **index** and **value** that corresponding on index.

The index is the position where the values exists. The index always starts on 0.

You can define array with various ways.

- Only define array

```java
int intArray[];
char charArray[];
```

- Create array

```java
// After define array...
intArray = new int[10];
charArray = new char[20];
```

- Define and create array in same time

```java
int intArray[] = new int[10];
char charArray[] = new char[20];
```

- Define, create and initialize array in same time

```java
int intArray[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
// Create array on numbers of values(size = 10).
```

- Plus, be careful not to define in this way.

```java
int intArray[10]; // Compile error.
```



After define array and initialize it, you can put and get values with index number.

Note that the index number always starts on 0. So if you create 5 size of array, you can access array with index 0 to 4.

```java
int intArray[] = new int[5]; // Define and create array
intArray[0] = 5; // put 5 in index 0
intArray[3] = 6; // put 6 in index 3
int n = intArray[3]; // get values in index 3. So, n will be 6.
```



And, I want to introduce the array's best friend. He's name is iteration! You can use both to use array more easily! Below is the good example to show its combination.

```java
import java.util.Scanner;

public class ArrayWithIteration {
	public static void main(String[] args) {
		// Print array values' average.
		int intArray[] = new int[5];
		int sum = 0;
		
		Scanner sc = new Scanner(System.in);
		// You can use '.length' to get array's size. 
		System.out.print("input " + (intArray.length) + " integers.");
		
		for(int i = 0; i < intArray.length; i++)
			intArray[i] = sc.nextInt(); // put values that input by keyboard.
			
		for(int i = 0; i < intArray.length; i++)
			sum += intArray[i]; // add values from array.
		
		System.out.println("The average is " + (double)sum/intArray.length);
		sc.close();
	}
}
```





## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  