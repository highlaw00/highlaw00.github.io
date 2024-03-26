---
title: "OS - Process Concept"
date: 2024-03-26
categories:
  - Operating System
tags:
  - Computer Science
  - Operating System
---

# Process and Threads Intro

OS의 역할 중 Process management의 역할에 대해 알아보자.  
컴퓨터 시스템이 동시에 여러개의 작업을 수행하기 위해서는 Process들에게 자원을 적절히 분배해주어야 한다. 이것의 책임은 **OS**에 있다.  
OS는 이것을 실현시키기 위해 **Scheduling**과 **Synchronization** 기법을 사용한다.

## What is Process?

- 프로세스란, **수행(Execution)중인 프로그램**이다!
  - 프로그램(실행 파일)이란, Disk와 같은 영구 저장 장치에 존재하는 데이터일 뿐이다.
  - 프로세스는 `An execution stream` in the context of a particular `process state` 라고 재정의 할 수 있다.
- `Execution stream` ?
  - 프로세스는 여러개의 명령어로 이루어져있는데 그것을 나열하면 `Executuion stream`이 된다.
- `Process state` ?
  - `Execution stream`의 스냅샷으로 볼 수 있는 개념
  - 프로세스의 현재 상태(코드, 데이터, 변수 등)를 나타낸다.

### 프로세스의 개념은 왜 생겨났는가?

- 만약, 프로세스의 개념이 없었더라면 Multi-tasking을 구현하기 위해 필요한 `Concurrency control`을 하기 매우 복잡해진다.
- 따라서 프로세스를 하나의 엔티티로 보아 이것을 쉽게 하도록 하였다.(Decomposition of system)

### Context(State)

Process의 상태는 크게 세가지의 context로 분류된다.

- Memory context
  - Process의 수행을 위해 메인 메모리에 존재해야 하는 context
  - `code segment`, `data segment`(global), `stack segment`(local), `heap`(dynamic memory allocation)
- Hardware context
  - `CPU registers`, `I/O registers`
- System context
  - `process table`, `open file table`, `page table`
  - OS가 프로세스를 관리하기 위해 생성한 자료구조

## Multi-programming vs. Multi-processing

멀티 프로그래밍과 멀티 프로세싱은 비슷한 개념같지만 사실은 아니다.
프로그래밍은 메모리의 관점이고, 프로세싱(태스킹)은 CPU의 관점

Uni-programming

- 하나의 프로세스가 메모리를 전체 장악하는 방식
- 구형 OS가 사용하던 방식

Multi-programming

- 여러 프로세스가 메모리를 나눠 가지는 방식

Single-processing(tasking)

- 하나의 작업만이 CPU에 의해 수행되는 방식

Multi-processing(tasking)

- 여러 프로세스가 동시에 CPU에 의해 수행되는 방식

### Design-time entity vs. Run-time entity

논외이지만, SW 공학적인 관점에서 OS는 굉장히 고마운 존재이다.  
만약 OS가 없다면 고객이 원하는 Task를 해결해주는 Component(Process)를 개발하는 것에 그치는 것이 아니라 그것들의 실행을 중재해주고 관리해줄 시스템까지 개발해야되기 때문이다.

따라서, 현대 OS는 **애플리케이션의 런타임 환경을 제공해주는 소프트웨어**라고 정의할 수 있게 된다.

## Process Control Block (PCB)

`PCB`는 프로세스의 현재 상태(값)를 저장하기 위해 존재하는 자료구조이다.

### State of Process

프로세스의 상태로는 다음과 같은 것이 있다. 그리고 프로세스의 상태는 계속해서 Transition하게 된다.

이 때 언급되는 프로세스의 상태는 `PCB`에 저장된 프로세스 상태와는 다른것이다!

![state-diagram]({{site.url}}/assets/images/state-diagram.png)

`Running`

- 프로세스의 명령어가 실행되고 있는 상태
- `Ready` 프로세스가 CPU에 의해 Dispatch 되면 Running 상태가 된다.
- 어떤 컴퓨터 시스템에서 `Running`될 수 있는 프로세스의 개수는 해당 시스템의 CPU 코어에 의해 결정된다.
- `Running` 프로세스가 `Ready` 상태로 변하는 경우: 한 프로세스가 오랜 시간 CPU를 점유하고 있으면 OS가 이것을 강제로 `Ready`로 바꾼다.

`Waiting`

- 프로세스가 어떠한 이벤트가 발생하는 것을 기다리는 상태
- 일반적으로 I/O에 의해 `Waiting` 상태로 변환된다. I/O 완료 이벤트 등이 발생하면 다시 `Ready` 상태로 변한다.
- `Waiting`을 하는 이유에 따라 다른 Queue에 들어간다.

`Ready`

- 프로세스가 CPU에 의해 할당되는 것을 기다리는 상태
- 프로그램이 메모리에 적재되었으나 다른 프로세스의 CPU 점유 등으로 인해 아직 실행되지 않은 상태
- CPU라는 서비스를 받기 위해 Ready Queue(run queue)에 들어간 상태

### 비선점 스케쥴링 & 선점 스케쥴링

`Non-preemtive Scheduling`

- 어떤 프로세스가 running 하다가 자발적으로 CPU를 양보하는 것
- Synchronous I/O의 수행 등으로 인해 일어난다.

`Preemtive Scheduling`

- 어떤 프로세스가 running 하다가 자신의 의지와는 무관하게 OS에 의해 강제로 `Ready` 상태로 변하는 것
- 반드시 Operating System의 개입이 필요하다. 이를 위해 인터럽트가 발생해야 한다.
