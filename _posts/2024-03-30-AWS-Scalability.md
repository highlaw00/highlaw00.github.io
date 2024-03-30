---
title: "[AWS] 확장성과 고가용성 이란?"
date: 2024-03-30
categories:
  - AWS
tags:
  - Computer Science
  - AWS
  - Cloud Computing
---

# 확장성 및 고가용성

## 확장성(Scalability)

<div class="notice--info">
확장성이란? 애플리케이션 시스템이 조정을 통해 더 많은 부하를 처리할 수 있다는 의미
</div>

확장성에는 2가지 확장성이 있다

- 수직 확장성
  - 인스턴스의 성능을 증가시키는 것
- 수평 확장성 (= elasticity)

### 수직 확장성 (Vertical Scalability)

수직 확장성이란? 인스턴스의 크기를 확장하는 것을 의미

<div class="notice--info">
콜센터 주니어 직원은 1분에 5개의 전화를 처리할 수 있지만 시니어 직원은 1분에 10개의 전화를 처리할 수 있다고 가정할 때 주니어 직원을 시니어 직원으로 바꾸면 이것을 <strong>수직 확장</strong> 이라고 하는 것!
</div>

만약 `t2.micro`에서 어플리케이션을 실행하다가 인스턴스를 `t2.large`로 변경하면 **수직 확장**이라고 한다.

수직 확장은 데이터베이스와 같이 분산되지 않는 시스템에서 흔히 사용된다.

### 수평 확장성 (Horizontal Scalability)

수평 확장성이란? 인스턴스의 개수나 시스템의 개수를 늘리는 것을 의미

<div class="notice--info">
콜센터 직원에게 과도한 업무가 주어질 때, 직원을 더 고용한다면 <strong>수평 확장</strong> 한 것이다!
</div>

단일 시스템을 수평 확장하면 시스템이 분산되었다고 표현하며 분산 시스템이라고 부를 수 있게 된다.

## 고가용성(High Availability)

<div class="notice--info">
고가용성이란? 애플리케이션 또는 시스템을 적어도 둘 이상의 AWS의 AZ나 데이터 센터에서 가동중이라는 것을 의미.
</div>

고가용성의 목표는 데이터 센터에서의 손실에서 살아남는 것으로, 하나의 센터에 문제가 생겨도 계속 동작 하게끔 하는 것.

# 정리 (EC2로 예시)

- 수직 확장
  - 인스턴스의 사이즈를 늘이고 줄이는 것
  - `t2.nano`에서 `t2.large`로 업그레이드하는 것이 그 예시
- 수평 확장
  - 인스턴스의 수를 늘리거나 줄이는 것
  - `Scale out`: 인스턴스의 수를 늘리는 것
  - `Scale in`: 인스턴스의 수를 줄리는 것
  - AWS 서비스로는 `Auto Scaling Group`, `Load Balancer`가 있다.
- 고가용성
  - 다수의 AZ에 걸쳐 같은 애플리케이션을 실행하는 인스턴스를 두는 것
  - `Auto Scaling Group multi AZ`, `Load Balancer multi AZ` 가 그 예시
