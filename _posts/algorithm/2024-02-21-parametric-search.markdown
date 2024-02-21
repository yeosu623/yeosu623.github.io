---
layout: post
title: "[Algorithm]Parametric Search"
subtitle: "the subgroup of binary search"
categories: algorithm
tags: algorithm parametric search
comments: false
---

## Introduction
> What is Parametric Search? And How Implement it?
>
> (This post is based on [here](https://ialy1595.github.io/post/parametric-search/).)

- Contents
	- [What is Parametric Search?](#what-is-parametric-search)
	- [Logic Flow](#logic-flow)
	- [Implementation(C, C++)](#Implementation)
	
## What is Parametric Search?
---
Parametric Search is used for finding the optimal value with binary search. Consider that you need to get some number of wire cuts with maximum length. So, you can check what if the length is 1, the length is 2, 3, ... to the longest wire among these wires.

This method is basically working, but it is too slow to search. Because this method need to search 1 to the longest wire, so the time complexity will be O(longest wire * search logic). Can we make this logic more efficiently?

When we search 1 to the longest wire, how about imply with binary search? So we can search the middle of length, and divide the answer range to 1/2 when search logic is worked. So, the new method of time complexity will be O(log(longest wire) * search logic).



## Logic Flow
---
Parametric Search is based on Binary Search, but some specific parts is different.

**First**, Binary Search is used for finding the **one specific value**, But Parametric Search is used for finding the **max or min optimal value**. So there are two way to approach.

When finding the max value, the range is divided :

- When condition matched, the range is m ~ r
- When condition unmatched, the range is l ~ (m-1)

<img width="285" alt="max" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/166a0231-9693-4496-80e0-080d6c360932">

When finding the min value, the range is divided:

- When condition matched, the range is l ~ m
- When condition unmatched, the range is (m+1) ~ r

The key point is that when condition matched, the "m" value is included, and the matched range is directed to the max or min way.



**Second**, Binary Search loop condition is left <= right, but Parametric Search loop condition is left < right, and end when **left == right**.

This is because that binary Search finds the specific value, the algorithm ends. Besides, Parametric Search haven't find the specific value, only to finding max or min value. In other words, there are no ending condition.

So, Parametric Search is ends when left == right. But, this has a minor problem : there is a hazard to fall infinite-loop. See the below figure.

<img width="285" alt="22" src="https://github.com/yeosu623/yeosu623.github.io/assets/72304945/ff840540-6cdc-45ee-95ae-79a34c86b597">

Consider when we finding max value. If set "m = (l + r) / 2" like Binary Search, what problem occur?

Think about when the gap between l and r is 1, like above figure. Then, l + r will be odd number, and (l + r) / 2 has the remainder, 0.5. To change that range...

- When finding max value, set m = (l + r + 1) / 2.
  - When condition matched, set l = m;
  - When condition unmatched, set r = m - 1;
- When finding min value, set m = (l + r) / 2;
  - When condition matched, set r = m;
  - When condition unmatched, set l = m + 1;

Then finally, **l == r** will be made!



## Implementation

---

The explanation is a bit harder, but the code is very simple. Below code can be used for finding max value. And I want to left for homework to write the code for finding min value.

```C++
// Parametric Search : finding max value
while(l < r) {
    m = (l + r + 1) / 2;

    if( condition(m) ) l = m;
    else r = m - 1;
}
// the answer can either l or r.
```



