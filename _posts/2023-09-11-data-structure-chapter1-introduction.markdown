---
layout: post
title: "[Data Structure]Chapter1. Introduction"
subtitle: "data structure introduction"
categories: dev
tags: datastructure complexity selecting binary recursion
comments: false
---

## Introduction
> The concept of data structure and algorithm, and show its very simple examples.

- Contents
	- [What is data structure and algorithm?](#what-is-data-structure-and-algorithm)
	- [Example 1. Selecting sort](#example-1.-selecting-sort)
	- [Example 2. Binary Search](#example-2.-binary-search)
	- [What is ADT?](#what-is-adt)
	- [Space Complexity and Time Complexity](#space-complexity-and-time-complexity)
	
## What is data structure and algorithm?
---
Literally, data structure means the structure of data. To manage and make form of data structure, past developers make some useful data structures. One of the most famous data structure is **tree**.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/54b5efea-c1e6-4f22-a2c0-8ba758535c08" alt="image" style="zoom:50%;" />

<center><b>Tree data structure</b></center>

But, how we can get, input, and manage its data with line-by-line source code? To do that, we need to learn the detailed its data structure and learn algorithm to handle it.

Algorithm also literally means the logic of something that how to operate. To handle data structure, we just cannot write few source code, but we need to understand its algorithm. All algorithms have this characteristics:

- Input : Existing 0 or above values.
- Output : At least one results must be output.
- Definiteness: All commands of algorithms must be obvious, not to be ambiguous.
- Finiteness : All commands of algorithms must be finite.
- Effectiveness : All commands can be executed.



Now, let's see some famous and well-known algorithms.



## Example 1. Selecting sort
---
If you need to sort n(n >=1) pieces of random numbers, how will you sort these?

To simple answer with natural language, "Add the smallest number on sorting list among random numbers that not sorted until now." But... this cannot be told as algorithm. Why?

- This description has ambiguous command.
- This description doesn't have where to add the smallest number, and how to save it.
- Also, this description doesn't have how to organize sorting list.

To make this description more specific, write this with the combination with source code and natural language. This also known as **pseudo code**.

```c
for(i = 0; i < n; i++) {
    Examine list[i] to list[n-1];
    Suppose that the smallest integer is at list[min];
    Interchange list[i] and list[min];
}
```

Then, you can more easily to compose the algorithm. Let's see the final result.

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 101
#define SWAP(x,y,t) ((t)=(x), (x)=(y), (y)=(t)) // SWAP implementation by Macro.

void sort(int[], int);
int main()
{
    int i, n, list[MAX_SIZE];
    printf("Enter the number of numbers to generate: ");
    scanf("%d", &n);
    
    if(n < 1 || n > MAX_SIZE) { // handle error
    	fprintf(stderr, "Improper value of n\n");
        exit(1);
	}
	
	for(i = 0; i < n; i++) {
		list[i] = rand() % 1000; // create n random numbers 
		printf("%d ", list[i]);
	}
	
	sort(list, n); // call sort() func. argument is array and array's size.
	printf("\n Sorted array: \n");
	for(i = 0; i < n; i++)
		printf("%d ", list[i]); // print sorted array.
	printf("\n");
}

void sort(int list[], int n)
{
	int i, j, min, temp;
	for(i = 0; i < n-1; i++) { 			// sort list[i] to list[n-1].
		min = i;						// assume minimal value in 'i' index
		for(j = i+1; j < n; j++) 		// for all values next of 'i' index...
			if(list[j] < list[min]) 	// if the value is smaller...
				min = j;				// set minimal value with it.
		SWAP(list[i], list[min], temp); // swap minimal values with 'i' index value.
	}
}
```

Selecting sort is one of the simplest algorithm for sorting. This codes might be seen difficult, but this just follow one rules : **Searching the smallest number and swap it to the most front index.**

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7d2e1164-8029-4587-8038-a29010beba1a" alt="image" style="zoom:50%;" />

<center><b>Selecting sort</b></center>

For above example, the first operation for searching do 6 times. Then the number 1 is sorted, the second operation do 5 times. then the third do 4 times, and then 3 times, 2 times, and finally, do 1 times at last. So, if you sort **n** numbers of data, the operation for searching do **k** times by this formula.

![image](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/7e7d854d-1524-46a5-ab82-9a4959cef0db)



## Example 2. Binary Search
---
Let's see another famous example, the binary search algorithm.

At first, let's assume this problem : when n(n>=1) numbers of sorted data saved in list[] array, and you have a key to find an corresponding the index of list. In other word, you need to find **i** in **list[i] = key.** How will you find an index?

The binary search algorithm give this method :

- Step 1. setting `left = 0, right = n-1, middle = (left+right)/2`
- Step 2. compare `list[middle]` and `key`.

Now, let's compose this method to pseudo-code.

```c
while(there are more integers to check) {
	middle = (left + right) / 2;
    if (key < list[middle])
        right = middle - 1;
    else if(key == list[middle])
        return middle; // found an index.
    else
        left = middle + 1;
}
```

Do you catch an abstract concept of binary search algorithm? Let's check your idea with final implemented source code.

```c
int binsearch(int list[], int key, int left, int right)
{
    /*serach list[0] <= list[1] <= ... <= list[n-1] for key.
    Return its position if found. Otherwise return -1 */
    int middle; // give 'left = 0, right = n - 1;' for parameters.
    while (left <= right) {
        middle = (left + right) / 2;
        switch(compare(list[middle], key)) {
            case -1 : left = middle + 1; // key is bigger.
                break;
            case 0 : return middle; // found key.
            case 1 : right = middle - 1; // key is smaller.
        }
    }
    return -1; // key cannot be found.
}

int compare(int x, int y)
{
    // compare x and y and output -1, 0, 1 depend on the result.
    if(x < y) return -1;
    else if(x == y) return 0;
    else return 1;
}
```

The description for binary search is here below. Take your time slowly to try to understand it. Maybe you can understand with this single image below.

<img width="504" alt="제목 없음" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/2d8b8686-51d5-400f-b4e4-a7c7ed54cf14">



## What is ADT?

---

ADT is the abstractions of features. Imagine you cook a soup for your parent. What will you do?

1. Boil water in a pot.
2. Put a corn.
3. Stir smoothly for a long time.
4. Add some salt and pepper to complete.

Like this process, ADT is the unit of your actions. In algorithm, ADT is the unit of algorithm's features. For example in array,

- Create array in desired size.
- Retrieve values of your desired index.
- Store values of your desired index.

The exact concept of ADT should include these contents :

- The aspect of algorithm : function name, types of parameters, and return type.
- The method to call a function and explain its result.
- Hide the process of function and implementation.



The below figure is the ADT for Array. Every data structure and algorithms should be written its ADT at first, because it is easy to implement on source code level with ADT. We will see more data structures with ADT on future chapters. So don't worry now, you will become more familiar through your journey of your programmer's life.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0bfa51ac-d7d6-498e-90d0-4990df0bb68b" alt="제목 없음" style="zoom:67%;" />





## Space Complexity and Time Complexity
---
These two aspects are friends with all of algorithms. Space Complexity is the consumption of memory to execute the program. But it is not the considerable aspect these days, because the size of memory is incredibly large than 30 years ago.

However, **Time Complexity** is the most important for all of algorithm, Because some algorithms could take time **EXPONENTIALLY** if you make algorithms in an in-efficient way.

Basically, assignment values, add, subtract, multiple, divide and other arithmetic operation serves one **Program Step**. Program Step is the basic unit of operation of software. For example, we saw the selecting sort algorithm and the number of operation results for n*(n-1)/2. In this, n means the program step, and the time complexity is n^2. Time complexity is set by most highest square of the formula.

<img src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/3cb497fd-de78-4528-b49d-2fa04c7e0881" alt="image" style="zoom:50%;" />

<center><b>Time Complexity of Selecting Sort.</b></center>

