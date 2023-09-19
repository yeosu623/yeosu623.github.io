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
	- [Chapter3](#link-to-chapter3)
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



There are some cautions when you are use structure.

- Caution 1 : Do not compose function with structure type for parameter. Use the pointer of structure type for parameter instead.

  The reason is that if you give argument for structure type, the structure not only just give values for parameter but also be copied it. So, use pointer instead to give address for parameter to solve these problem.

- Caution 2 : You need to consider memory alignment on structure. Structure align memory that is automatically sized based on the **multiple of the largest type size**.

  So, if you compose structure like this and if your OS is recognized about int size is 4,
  
  ```C
  struct A {
      int a;
      int b;
      char c;
  }
  ```

  This structure's size will not be 9, but will be 12.

  Like this, if you compose like this :
  
  ```C
  struct B {
  	char a;
      short b;
      int c;
  }
  ```
  
  The size will be 8.
  
  Otherwise, if you compose like this :
  
  ```C
  struct C {
      char a;
      double b;
  }
  ```
  
  The size will be 16.



## Link-to-Chapter3
---




## Link-to-Chapter4  
---
Chapter4에 관한 내용을 여기다가 적습니다.  

## Link-to-Chapter5  
---
Chapter5에 관한 내용을 여기다가 적습니다.  