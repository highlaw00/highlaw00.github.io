---
title: "[AWS] ELB(Elastic Load Balancer) - 심화"
date: 2024-03-30
categories:
  - AWS
tags:
  - Computer Science
  - AWS
  - Cloud Computing
---

# 고정 세션(Sticky Session)

![alt text]({{site.url}}/assets/images/sticky-session.png)

- 클라이언트가 이전에 접근한 인스턴스에게 로드 밸런싱을 해주는 기능
- `ALB`에서 사용 가능
- `쿠키`를 활용해 구현되며 쿠키 만료 기간 등을 설정할 수 있다.

# 쿠키

## 애플리케이션 기반 쿠키(Application-based Cookie)

### 커스텀 쿠키
- 타겟의 애플리케이션에서 생성되는 쿠키
- 애플리케이션에서 필요로 하는 사용자 정의 속성이 포함될 수 있음
- 쿠키 이름은 각 타겟 그룹 별로 식별되어야 함
- `AWSALB`, `AWSALBAPP`, `AWSALBTG` 등은 예약되어있기 때문에 사용 불가

### 애플리케이션 쿠키
- 로드 밸런서 자체에서 생성됨
- `AWSALBAPP`의 이름으로 된 쿠키

## 기간 기반 쿠키(Duration-based Cookies)
- 로드 밸런서에서 생성되는 쿠키
- ALB에서는 `AWSALB`로 불린다.

# 크로스존 로드밸런싱 (Cross Zone Load Balancing)

![alt text]({{site.url}}/assets/images/cross-zone.png)

- 크로스 존 로드밸런싱을 활성화 하면 AZ가 다르더라도 타겟 그룹 내에 존재한다면 동일하게 로드 밸런싱을 한다.
- 만약 비활성화 한다면 동일한 AZ의 타겟 그룹에게만 로드 밸런싱 한다.

## 로드 밸런서 별 상세

### ALB
- 크로스 존 로드밸런싱이 항상 적용
    - 타겟 그룹 계층에서 비활성화 가능
- AZ 간의 데이터 송수신에 비용이 청구되지 않음(기본값 이기 때문)

### NLB & GWLB
- 크로스 존 로드밸런싱 비활성화
- AZ 간의 데이터 송수신에 대한 비용이 청구됨.

# SSL/TLS

- SSL 암호화는 클라이언트와 로드 밸런서 사이에 존재하는 트래픽을 암호화 해주는 기법이다. 이를 **전송 중(In-flight)** 암호화라고 함. 
- 송신자와 수신자 측에서만 이것을 복호화 할 수 있다.
- TLS는 SSL의 최신 버전임으로 동일한 용어라 생각해도 됨!

- Public SSL 인증서는 인증 기관(CA)에서 발급해준다.
- 이 SSL 인증서를 로드 밸런서에 추가하면 클라이언트와 로드 밸런서 사이의 통신을 암호화 할 수 있게 된다.

## SNI(Server Name Indicate)

