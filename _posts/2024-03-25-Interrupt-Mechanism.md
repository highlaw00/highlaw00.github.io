---
title: "OS - Interrupt Mechanism"
date: 2024-03-25
categories:
  - Operating System
tags:
  - Computer Science
  - Operating System
---

# Intro

여러개의 프로그램이 하나의 컴퓨터에서 수행되는 Multi-programmed 컴퓨터 시스템에서는 여러 Job을 하나의 시스템 내에서 수행하기 위해 인터럽트 메커니즘이 필수이다.

## Interrupt Process

인터럽트의 발생과 처리의 과정은 다음과 같다.

1. CPU의 내부에는 `인터럽트 요청 라인`이 존재하는데, CPU가 각 명령어를 수행하고 그것을 마칠 때 마다 `인터럽트 요청 라인`을 조사한다.
2. 현재 하고 있던 작업의 정보(`pc`등의 레지스터)를 저장한다.
3. CPU는 `인터럽트 벡터 테이블`와 `IRQ`(Interrupt Request Number)를 확인하여 `ISR`(Interrupt Service Routine)으로 jump한다.
4. 인터럽트 핸들러가 `ISR`을 모두 수행하고 원래의 태스크로 돌아온다.

### H/W Interrupt

하드웨어 인터럽트는...
- 실제 물리적인 디바이스(혹은 그것을 제어하는 컨트롤러)가 발생시키는 `전기적인 신호`이다.
- `Asynchronous` 하게 동작한다.

<div class="notice--info">
 어째서 <code>Asynchronous</code> 동작한다고 하는 것일까? <br/><br/>

 I/O 디바이스는 실제 입출력 연산을 시작하고 그것을 마칠때까지 긴 시간이 걸리게 된다. 
 그 시간을 CPU가 Wait하게 되면 Multi-programmed 환경에서는 좋지 않은 UX를 제공할 것이다.<br/><br/>
따라서, CPU는 I/O 디바이스에게 연산을 요청하고 I/O 디바이스는 연산이 끝나면 CPU에게 연산이 끝났다고 보고하는 것이다.
</div>

### S/W Interrupt

소프트웨어 인터럽트는... **트랩**이라고도 불린다.
- 명령어로 수행되는 인터럽트이다.
- `Synchronous` 하게 동작한다.

<div class="notice--info">
 어째서 소프트웨어 인터럽트는 <code>Synchronous</code>하게 동작할까?<br/><br/>

 시스템 콜이나 예외(가령 <code>Divide by zero</code> 등)이 대표적인 소프트웨어 인터럽트이다.<br/> 사용자의 코드가 수행되다가 CPU가 소프트웨어 인터럽트 명령어를 실행하면, OS가 커널 모드로 진입하여 해당 인터럽트의 커널 루틴을 수행한다.
</div>