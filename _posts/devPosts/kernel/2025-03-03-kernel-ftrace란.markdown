---
layout: post
title: "[Kernel]ftrace에 대하여"
subtitle: "kernel and device driver"
categories: dev
tags: kernel device driver
comments: false
---

## Introduction
> ftrace란 무엇이고, 어떻게 사용하는지 자세하게 알아봅시다.

- Contents
	- [ftrace의 역사](#ftrace의-역사)
  - [ftrace를 설정하는법](#ftrace를-설정하는법)
  - 
  

## ftrace의 역사

리눅스가 막 개발되기 시작할 때 부터 커널을 디버깅하는 도구는 많았었다. 대표적으로 kprobes가 있는데, kprobes는 리눅스 커널의 코드 안에 직접 프로브(커널을 추적하기 위해 임의로 삽입한 코드)를 삽입하여 디버깅 정보를 수집하였다. 하지만 kprobes는 초보자를 위한 도구는 아니였다. 사용하기 위해서는 커널 심볼 테이블의 내용을 잘 알고 있어야 됬고, 커널 함수의 흐름을 세부적으로 파악하여 함수 호출 전, 후, 오류 발생시를 나누어 프로브를 작성해야 되었다. 밑의 사진처럼 말이다.

![Image](https://github.com/user-attachments/assets/4034ec72-20e3-4d25-9ee4-7f471c38af1c)

게다가 kprobes에는 **실시간 시스템에 부적합** 하다는 치명적인 단점이 하나 있다. 코드를 직접 삽입하여 프로브를 만드는 것도 번거로운데, 문제는 프로브가 실행될 때 마다 코드의 실행 흐름이 커널에서 프로브로 전달되면서 **커널의 실행이 잠시 지연되는** 현상이 발생한다는 점이다. kprobes를 함수 호출이 많은 곳에서 사용하면 시스템이 락업(Lockup) 되거나 커널 패닉까지 이어질 수 있어, 현재는 특수한 상황에서만 사용되는 추세이다.

<br>

하지만 printk, kprobes같이 코드를 직접 수정하여 디버깅하는 방식과 달리, **ftrace는 커널 내부에 내장되어 있는 기능** 이라 소스코드를 수정하지 않고 커널의 동작을 확인할 수 있다. 물론 소스코드를 수정하지 않으니 **함수를 몇십번 호출해도 성능에 영향이 없어** 현재 커널 디버깅에 많이 사용하고 있다.

ftrace는 커널 2.6.27에 2008년 9월 Steven Rostedt에 의해 처음 도입되었으며, 커널 로그 분석 뿐만 아니라 스케줄링, 인터럽트, 메모리 매핑 I/O, CPU 상태, 파일 시스템 및 가상화 등 다양한 작업의 정적 추적도 가능하고, 커널의 대기 시간도 동적으로 측정할 수 있다.



## ftrace를 설정하는법





## References

- https://velog.io/@mythos/Linux-Tutorial-14-%EB%94%94%EB%B2%84%EA%B9%85-%EC%84%B1%EB%8A%A5-%EB%B6%84%EC%84%9D-Kprobes
- 
