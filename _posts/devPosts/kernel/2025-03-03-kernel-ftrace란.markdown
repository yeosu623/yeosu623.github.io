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
  - [ftrace 로그 해석하기](#ftrace-로그-해석하기)
  



## ftrace의 역사

리눅스가 막 개발되기 시작할 때 부터 커널을 디버깅하는 도구는 많았었다. 대표적으로 kprobes가 있는데, kprobes는 리눅스 커널의 코드 안에 직접 프로브(커널을 추적하기 위해 임의로 삽입한 코드)를 삽입하여 디버깅 정보를 수집하였다. 하지만 kprobes는 초보자를 위한 도구는 아니였다. 사용하기 위해서는 커널 심볼 테이블의 내용을 잘 알고 있어야 됬고, 커널 함수의 흐름을 세부적으로 파악하여 함수 호출 전, 후, 오류 발생시를 나누어 프로브를 작성해야 되었다. 밑의 사진처럼 말이다.

![Image](https://github.com/user-attachments/assets/4034ec72-20e3-4d25-9ee4-7f471c38af1c)

게다가 kprobes에는 **실시간 시스템에 부적합** 하다는 치명적인 단점이 하나 있다. 코드를 직접 삽입하여 프로브를 만드는 것도 번거로운데, 문제는 프로브가 실행될 때 마다 코드의 실행 흐름이 커널에서 프로브로 전달되면서 **커널의 실행이 잠시 지연되는** 현상이 발생한다는 점이다. kprobes를 함수 호출이 많은 곳에서 사용하면 시스템이 락업(Lockup) 되거나 커널 패닉까지 이어질 수 있어, 현재는 특수한 상황에서만 사용되는 추세이다.

하지만 printk, kprobes같이 코드를 직접 수정하여 디버깅하는 방식과 달리, **ftrace는 커널 내부에 내장되어 있는 기능** 이라 소스코드를 수정하지 않고 커널의 동작을 확인할 수 있다. 물론 소스코드를 수정하지 않으니 **함수를 몇십번 호출해도 성능에 영향이 없어** 현재 커널 디버깅에 많이 사용하고 있다.

ftrace는 리눅스 커널 2.6.27에 2008년 9월 Steven Rostedt에 의해 처음 도입되었으며, 커널 로그 분석 뿐만 아니라 스케줄링, 인터럽트, 메모리 매핑 I/O, CPU 상태, 파일 시스템 및 가상화 등 다양한 작업의 정적 추적도 가능하고, 커널의 대기 시간도 동적으로 측정할 수 있다.



## ftrace를 설정하는법

먼저, ftrace는 정식으로 리눅스 커널 안에 내장되어 있어 이를 직접 입력하여 활성화 시켜주어야 한다. 입력해 주어야 하는 파일과 설정값은 밑과 같으며, 입력 후에 커널 이미지를 설치하고 재부팅 해야한다.

설정값의 이름을 보면 ftrace, irq 인터럽트 핸들러, stack 등과 관련이 있어 보인다.

참고로, 라즈베리파이에서는 이미 ftrace 사용에 필요한 설정이 활성화 되어 있어 따로 해야할 것은 없다.

```bash
/arch/arm/configs/your_device_defconfig

CONFIG_FTRACE=y
CONFIG_DYNAMIC_FTRACE=y
CONFIG_FUNCTION_TRACER=y
CONFIG_FUNCTION_GRAPH_TRACER=y
CONFIG_IRQSOFF_TRACER=y
CONFIG_SCHED_TRACER=y
CONFIG_FUNCTION_PROFILER=y
CONFIG_STACK_TRACER=y
CONFIG_TRACER_SNAPSHOT=y
```



이제 ftrace를 사용할 준비가 완료되었다! 이제 ftrace를 사용해보자.

사용할 수 있는 설정 파일들은 **<u>/sys/kernel/debug/tracing</u>** 에 있는데, 실제로 사용하는 파일들은 많지 않다.

각각의 파일에 1만 입력('echo 1' 등으로 입력하거나, 편집기로 직접 입력하면 된다.) 하면 활성화, 0만 입력하면 비활성화 하겠다는 의미이며, 실제로 사용하는 파일들은 다음과 같다. 나열한 파일들은 /sys/kernel/debug/tracing 의 하위 디엑터리에 있는 것으로 가정한다.

- /tracing_on : ftrace 활성화(1)/비활성화(0).
- /current_tracer : ftrace 종류를 선택한다. 설정값은 다음과 같다.
  - nop : 기본 트레이서이다. ftrace의 이벤트만 출력한다. 이벤트란 커널의 서브시스템, 기능의 세부동작을 의미한다.
  - function : 함수 트레이서이다. set_ftrace_filter로 지정한 함수를 누가 호출하는지 출력한다.
  - function_graph : 함수 실행 시간과 세부 호출 정보를 그래프 포맷으로 출력한다.
- **/set_ftrace_filter** : 트레이싱하고 싶은 함수를 지정하는 파일이며, /current_tracer에서 function, function_graph로 설정할 때만 동작한다.
  - 지정할 수 있는 함수는 /available_filter_functions 파일에 있는 것만 가능하다. 만약 이 파일에 없는 함수를 지정할 경우 시스템이 락업(시스템이 아무런 반응을 하지 않는 현상) 된다.
  - **/set_ftrace_filter에는 반드시 최소 하나 이상의 함수를 설정해야 한다.** 의미없이 설정할 수 있는 함수의 예로는 커널 부팅중에 실행되는 함수, 이를테면 secondary_start_kernel 등이 있다. 만약 아무런 함수도 설정하지 않았다면, 모든 커널 함수를 트레이싱하여 결국 시스템이 락업된다.

- /options/func_stack_trace : set_ftrace_filter에 지정된 함수의 콜 스택 출력을 활성화(1)/비활성화(0) 한다.
- /options/sym-offset : 함수를 호출할 때 주소의 오프셋 출력을 활성화(1)/비활성화(0) 한다.
- /events/... : 원하는 이벤트를 골라서 활성화(1)/비활성화(0)를 시킬 수 있다.



중요한 이벤트는 다음과 같다. 적는 이벤트는 /events 의 하위 디렉터리이다.

- /sched : 프로세스가 스케줄링되는 동작과, 스케줄링 개요를 트레이싱하는 이벤트를 볼 수 있다.
  - /sched_switch : 컨텍스트 스위칭 동작
  - /sched_wakeup : 프로세스를 깨우는 동작
- /irq : 인터럽트와 Soft IRQ를 트레이싱하는 이벤트가 있다. Soft IRQ는 커널 모듈의 일종이며, 중요도가 낮고 바로 처리하지 않아도 되는 인터럽트를 처리한다.
  - /irq_handler_entry : 인터럽트가 발생한 시각과 인터럽트 번호 및 이름을 출력
  - /irq_handler_exit : 인터럽트 핸들링이 완료
  - /softirq_raise : Soft IRQ 서비스 실행 요청
  - /softirq_entry : Soft IRQ 서비스 실행 시작
  - /softirq_exit : Soft IRQ 서비스 실행 완료



## ftrace 로그 해석하기

ftrace를 활성화 시키면, **<u>/sys/kernel/debug/tracing 디렉터리의 /trace 파일 안에 로그가 담긴다.</u>** 이제 한 번 확인해보자!

```bash
chromium-browse - 1436 [002] d... 9445.131875 : sched_switch : prev_comm=chromium-browse prev_pid=1436 prev_prio=120 prev_state=S ==> next_comm=kworker/2:3 next_pid=1454 next_prio=120
```

...???? 이게 대체 무슨 뜻인가? 하나씩 확인해보자.

- chromium-browse : **프로세스 이름**
- 1436 : **프로세스 ID**
- [002] : **CPU 번호**. 몇 번째 CPU에서 프로세스가 실행 중인지.
- d... : **컨텍스트 정보** (환경 정보). 한 칸에 하나의 정보가 있다.
  1. 인터럽트 활성화/비활성화(d)
  2. 선점 스케줄링 대상(n)
  3. 인터럽트 컨텍스트(h)/Soft IRQ(s)
  4. 프로세스의 thread_info 구조체의 preempt_count 값(. 혹은 0~3)

- 9445.131875 : **타임스태프**
- sched_swtich : **이벤트 이름**
- 그 이후 : 이벤트 내용

앞으로의 포스팅에서 다양한 이벤트를 분석하면서 스케줄링, IRQ 등의 커널이 어떻게 동작하는지를 하나씩 확인해볼 것이다.



## References

- <a href="https://velog.io/@mythos/Linux-Tutorial-14-%EB%94%94%EB%B2%84%EA%B9%85-%EC%84%B1%EB%8A%A5-%EB%B6%84%EC%84%9D-Kprobes">https://velog.io/@mythos/Linux-Tutorial-14-%EB%94%94%EB%B2%84%EA%B9%85-%EC%84%B1%EB%8A%A5-%EB%B6%84%EC%84%9D-Kprobes</a>
- <a href="https://yohda.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%BB%A4%EB%84%90-Interrupt-softirq">https://yohda.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%BB%A4%EB%84%90-Interrupt-softirq</a>
