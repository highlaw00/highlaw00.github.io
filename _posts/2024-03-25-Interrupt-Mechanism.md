---
title: "OS - Interrupt Mechanism"
categories:
  - Operating System
tags:
  - Computer Science
  - Operating System
---

# Intro

여러개의 프로그램이 하나의 컴퓨터에서 수행되는 Multi-programmed 컴퓨터 시스템에서는 여러 Job을 하나의 시스템 내에서 수행하기 위해 인터럽트 메커니즘이 필수이다.

## Metaphor

인터럽트 메커니즘의 종류에 대해 잘 이해하기 위해 다음과 같은 상황을 가정해보자.

<div class="notice--info">
가정 #1. 책을 읽다가 택배 아저씨가 누른 초인종 소리를 듣고 책갈피를 끼운 뒤 문을 열어주고 택배를 받은 뒤 다시 돌아와 책을 다시 읽는 시나리오
</div>

<div class="notice--info">
가정 #2. 책을 읽던 중 "100번째 페이지까지만 읽고 물을 마신 다음에 다시 읽어야겠다!" 라고 생각한 뒤 실제로 100페이지 까지 읽고 물을 마시고 다시 읽는 시나리오
</div>

### H/W Interrupt

하드웨어 인터럽트는 실제 물리적인 디바이스(혹은 그것을 제어하는 컨트롤러)
