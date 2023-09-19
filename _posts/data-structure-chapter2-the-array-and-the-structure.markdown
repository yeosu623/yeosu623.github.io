---
layout: post
title: "[Data Structure]Chapter2. The Array and The Structure"
subtitle: "the array and the structure"
categories: dev
tags: datastructure
comments: false
---

## Introduction
> The array and the structure in C.

- Contents
	- [What is Array?](#what-is-array)
	- [What is Structure?](#what-is-structure)
	- [What is Union?](#what-is-union)
	- [Chapter4](#link-to-chapter4)
	- [Chapter5](#link-to-chapter5)
  
## What is Array?
---
Array is the sequence variables with same type. The below figure is the definition of array of ADT. But, you don't need to fully understand it to use array, because ADT is just an abstraction of features.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/e1fd659e-cf88-4d9c-b84a-6bc4e81fe3d3" alt="ADT" style="zoom:67%;" />

To use array in C :

- Define array 
  - int list[5], *plist[5];
  - All index or array start on 0.
- Implementation of array
  - Assume the address of list[0] = a
  - The address of list[1] = a + sizeof(int)
  - list + i = &list[i], *(list + i) = list[i]
  - Give array as argument is same as copy the start address of the array. This is same effect about call-by reference.

To dynamically allocate array in C :

 ```C
 /* 1D dynamic array */
 int *A = (int*)malloc(sizeof(int) * 100); // initialized with garbage values.
 int *B = (int*)calloc(100, sizeof(int)); // initialized with 0.
 
 A = (int*) realloc(A, sizeof(int) * 200); // resize array.
 free(A); // get off the array from memory.
 
 /* 2D dynamic array */
 int **C = (int**)malloc(sizeof(int*) * 10);
 for(int i = 0; i < 10; i++)
     C[i] = (int*)malloc(sizeof(int) * 20);
 ```



## What is Structure?
---
Structure is a user-defined type with more than one types. It can have variety of types - can be mixed with int, double, array, also another structure.

It is end-to-end with array; array is composed with same components, but structure is with different things.

```C
struct humanBeing {
    char name[10];
    int age;
    double height;
};
typedef struct humanBeing human_being;

int main() {
    human_being person;
    strcpy(person.name, "James Lee");
    person.age = 21;
    printf("%f", person.height);
}
```





## What is Union?
---
Chapter3에 관한 내용을 여기다가 적습니다.  



## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  