---
layout: post
title: "[TEST]Typora 마지막 테스트"
subtitle: "Typora test final"
categories: others
tags: others typora markdown editor
comments: false
---

## Introduction
> Typora 마크다운 에디터 마지막 테스트

- Contents
	- [글 테스트](#text-test)
	- [그림 테스트](#image-test)
	
## Text test
---
다른건 전부 해보았으니 코드 테스트만 해본다.

```java
package univ_study;

public class Hello2030 {
	public static void main(String[] args) {
		System.out.println("Hello");
	}
}
```

```java
class BreakBasic {
    public static void main(String[] args) {
        int num = 1;
        boolean search = false;

        // 처음 만나는 5의 배수이자 7의 배수인 수를 찾는 반복문
        while(num < 100) {
            if(((num % 5) == 0) && ((num % 7) == 0)) {
                search = true;
                break; // while문을 탈출
            }
            num++;
        }

        if(search)
            System.out.println("찾는 정수 : " + num);
        else
            System.out.println("배수가 없습니다.");
    }
}
```

> 인용문 테스트입니다.
>
> > 이중 인용문 테스트입니다.
> >
> > > 삼중 인용문 테스트 입니다.



`코드블럭 테스트입니다.`





## Image Test
---
![youtube logo](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/c87989f2-116c-43f0-9012-bb4185988984)

![cmd 창](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/00c3346d-a85b-4ff6-9946-2d015ca942f8)

![python IDLE](https://github.com/yeosu623/yeosu623.github.io/assets/72304945/0b285560-fab5-42cb-94dd-83c7a1e487e1)

