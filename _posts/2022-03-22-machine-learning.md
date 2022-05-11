---
layout: single
title: "[딥러닝] 용어"
categories:
  - Deep Learning
tag: [머신러닝]
toc: true
---
## 데이터 종류
1. 정형데이터 ( Structured Data)
- 테이블과 같이 고정된 컬럼에 저장되는 데이터와 파일, 그리고 팽과 열에 의해 데이터 속성이 구별되는 스프레시트 형태의 데이터
2. 비정형 데이터
- 데이터 변수가 사전에 구조적으로 정의된 의미를 갖지 않는 데이터
- 이미지, 텍스트 데이터 등
    - 이미지는 3차원 Tensor로 표현(Width, Height, RGB)

## 변수
1. 이산형 변수
- 명목형 (범주형) : 여러 Class 중 하나의 이름에 데이터를 분류할 수 있을 때 사용
- 순서형: 데이터가 속하는 Class 들에 순서가 있는 경우
2. 연속형 변수
- 실수 형태의 연속적인 값을 가지고 있는 변수
- ex) 키, 몸무게

## 지도 학습
- 기계 학습의 한 범주
- 학습 데이터로부터 X -> Y 의 관계를 설명하는 함수를 찾는 방법론
- y가 범주형이면 분류, 연속형이면 회귀

> 우리의 주 관심은 Y(예측 대상), Y를 설명하는 X 는 여러 개, 여러 개의 X와 Y의 관계를 찾는 것

## 인공지능 기계 학습
- 인공지능: 입력값을 넣어주면 출력값이 나오는 함수
- 기계학습: 데이터로부터 함수를 찾아주는 학문