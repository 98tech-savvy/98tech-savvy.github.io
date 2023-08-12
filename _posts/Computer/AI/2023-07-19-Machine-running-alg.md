---
title:  "머신러닝 알고리즘의 이해"
excerpt: "머신러닝이 어떻게 학습하는지에 대해 알아보자"

categories:
  - AI
tags:
  - [AI, Machine running, Algorithm, 알고리즘, 머신러닝, 딥러닝]

toc: true
toc_sticky: true

date: 2023-07-19
last_modified_at: 2023-07-19
---

# 머신러닝 알고리즘이란
**머신러닝**은 **데이터로부터 자동으로 모델을 생성하는 방법**을 뜻한다. 그리고 머신러닝 알고리즘은 이 머신러닝을 작동하기위한 엔진이라고 생각하면 된다. 즉, 데이터 집합들을 모델로 바꿔주는 엔진이다.

# 머신러닝의 작동 원리
일반적으로, 프로그래밍 알고리즘이란 해야할 것에 대한 일들을 컴퓨터에게 간단한 방식으로 알려준다. 예를 들어서

> 알파벳 순서대로 이 배열(array)을 정리해줘

라는 정렬 알고리즘을 통해 정리되지 않은 배열을 정렬할 수 있다.

그리고 문제의 해결이 어려울 수록 알고리즘은 복잡해지고 난해해진다. 머신러닝 알고리즘의 경우 다른 알고리즘들에 비해 더 복잡한데, 머신러닝은 특정 수학 함수에 맞추는 제약이 없다는 점때문이다. 보통 **회귀와 분류** 두 가지 문제 범주로 머신러닝은 문제를 해결하는데, 회귀는 수치 데이터, 분류는 비수치 데이터에 사용한다.

수치 데이터의 경우 특정 주소와 직업을 가진 사람의 예상수입을 구하라
비수치 데이터의 경우 돈을 빌린 사람이 돈을 갚을 것인가?와 같은 문제에 대한 데이터다.

# 지도 학습과 비지도 학습

## 지도 학습
지도 학습의 경우에는 고양이를 예로 들면 이해하기 쉽다. 수천, 수만장의 고양이 사진들을 데이터 집합에 제공해서 이전에 본 적이 없는 고양이 사진을 보여줬을 때 고양이인걸 올바르게 식별할 수 있는가?

## 비지도 학습
비지도 학습의 경우에는 알고리즘이 스스로 데이터를 살펴보고 유의미한 결과를 도출하려고 시도한다. 고객들이 구매한 리스트를 보고 고객들을 유의미한 그룹으로 나누기, 사진 목록에서 비슷한 얼굴들 끼리 그룹화하기 등등.

# 머신러닝을 위한 데이터 정제
머신러닝에 데이터를 사용하기 위해서는 머신러닝에 알맞은 데이터로 필터링해주어야한다. Null, None, Nan 등의 **결측값(값이 측정되지 않는 것)**은 머신러닝에 일반적으로 사용할 수 없기 때문에 이러한 결측값들을 지우는 과정을 거쳐야한다.

1. 결측값이 존재하는 샘플 삭제
2. 결측값이 많이 존재하는 변수 삭제
3. 결측값을 다른 값으로 대체

또 **이상치**가 존재하면 모델의 성능 저하를 유발할 수 있다. 일반적으로 전 처리 과정에서 제거하며, 이상치를 판단하는 기준을 정해주어야한다.

이상치인지 판단하는 방법은 다음과 같다.
1. 통계지표를 사용해 판단
2. 데이터 분포를 보고 직접 판단
3. 머신러닝 기법을 사용해 이상치 분류

# 데이터 인코딩 및 정규화
머신을 위해 범주 데이터를 사용하려면 텍스트 레이블을 다른 양식으로 인코딩해주어야 한다. 일반적으로 2가지 종류의 인코딩이 사용된다.

## 레이블 인코딩
각 텍스트 레이블을 숫자로 대체한다.

## 원 핫(One-Hot) 인코딩
각 텍스트 레이블의 값을 이진 값(1, 0)이 있는 열로 변환한다. 일반적으로 이 원 핫 인코딩을 선호한다.

그리고 숫자 데이터를 사용하려면 일반적으로 데이터를 정규화하는 과정을 거쳐야한다. 그렇지 않으면 범위가 큰 숫자는 특징 벡터간의 유클리드 거리를 지배하고, 이들의 효과가 확대되면 다른 필드가 희생되고 급속 하강 최적화가 수렴되지 않을 수 있기 때문이다. 이 과정을 **특징 스케일링**이라고 하는데, 최소-최대 정규화, 평균 정규화, 단위 길이로 스케일링, 표준화 등등이 있다.