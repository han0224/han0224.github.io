---
layout: single
title: "가상화와 컴퓨팅 기술"
categories:
  - Colud Computing
tag: [virtualization, Hypervisor]
toc: true
---
## 🎁 가상화란
- 물리적 IT 자원(한정된 자원)을 가상의 IT 자원으로 전환시키는 기술
- 가상화를 관리하는 소프트웨어(Hypervisor)를 사용해 하나의 물리적 머신에서 가상 머신을 만드는 프로세스

## 🔔 클라우드 컴퓨팅에서 가상화의 필요성
1. **하드웨어 독립성**
  - 가상머신은 하드웨어에 독립이며 다양한 물리적인 서버에 이동하며 동작이 가능
  - 그렇기에 클라우드가 요구하는 부하 균등, 확장성 장애극복 등 효과적으로 지원
1. **서버 통합 제공**
  - 서버 통합: 여러 가상 서버가 하나의 물리적 서버를 공유할 수 있게 함
  - 다중의 가상머신들을 동시에 구동하여 협업 가능
1. **자원 복제**
  - 가상 서버는 하드디스크의 내용의 바이너리 파일 형태로 복사해 보유

## 🍫 Hypervisor
> 가상머신이 물리시스템 자원에 대한 접근을 제공하는 프로그램 ( VMM : Virtual Machine Monitor)

- 호스트에서 여러 가상의 게스트 os를 실행하기 위한 프로그램
- VM 과 HW 간의 IO 명령을 처리하는 인터페이스
- application, user 의 관점에서 가상머신은 물리적 시스템의 모든 속성과 특성을 가지지만 물리적 머신을 에뮬레이트 하는 엄격한 SW

## 🍡 가상화 유형
### 운영체제 기반 가상화

![그림1](https://user-images.githubusercontent.com/70616579/161076477-c67d34cd-1f2e-401a-b19e-d58bd2ac644e.png){: width="50%"}

- 기존 운영체제 위에 가상화 소프트웨어를 설치

### 하드웨어 기반 가상화
![그림2](https://user-images.githubusercontent.com/70616579/161077009-35edb203-bf04-4937-aa5e-d4f9b6008757.png){: width="50%"}
- Host OS 필요로 하지 않는 하드웨어 기반 가상화의 여러 논리적 계층
- Host OS 가 없어서 HW 접근 어려움

## 🌌 클라우드 컴퓨팅 서비스 기술

### 클러스터 컴퓨팅
- 여러 대의 **동일**한 컴퓨터들이 연결되어 하나의 시스템처럼 동작하는 컴퓨터들의 집합

|유형|설명|
|---|---|
| 고가용성 클러스터 | 장애가 발생해도 쉽게 복구 (이중화 dual 구조)|
| 로드 밸런싱 클러스터 | 부하 분산 (작업 요청 적절히 배치)
| 고성능 클러스터|병렬처리 (동시에 여러 컴퓨터 작업 할당)|

### 가상화
[가상화](#가상화란)

## 🧷 Hypervisor 기반 인스턴스
### HW 가상화에 따른 분류
1. CPU 가상화 
1. 메모리 가상화
1. 저장소 가상화
1. 네트워크 가상화

### 가상화 SW - Hypervisor
- 위치와 역할에 따라 2가지 범주로 구분

![그림3](https://user-images.githubusercontent.com/70616579/161083930-a5247db9-2ecc-4cc4-9754-ae350e990d71.png){: width="80%"}
<br/>
<br/>

|구분|설명|
|:---:|---|
| **하이퍼바이저형 가상화**<br/>(**Type1**) | HW 에 하이퍼바이저를 배치<br/>**베이 메탈**이라고도 함|
| **호스트형 가상화**<br/>(**Type2**) | 운영체제 기반, 호스트 OS 위에 하이퍼바이저 배치|

- 가상화 방식에 따른 구분

![그림4](https://user-images.githubusercontent.com/70616579/161086619-30746579-a340-46b6-9ad8-f09502b9ffc4.png){: width="80%"}
<br/>
<br/>

|구분|설명|
|:---:|---|
| 전가상화 | 컴퓨팅 시스템의 HW 자원을 **완전하게 가상화** 하는 방식<br/>- **Type2** 호스트형 가상화<br/>- 게스트 OS 수정 없이 구동 가능<br/>- HW는 Host OS에 의해 제어<br/>- 복잡성으로 인해 낮은 성능|
| 반가상화 | HW의 **일부분만 가상화** 하는 방식<br/>- **Type1** 베이 메탈 형태<br/>- 게스트 OS는 하이퍼바이저의 커널 드라이버와의 통신을 위해 수정 필요<br/>- HW는 수정된 OS를 통해 하이퍼바이저가 통제<br/>- 상대적으로 고성능|