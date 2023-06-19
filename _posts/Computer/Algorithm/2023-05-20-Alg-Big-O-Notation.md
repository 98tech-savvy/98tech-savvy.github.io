---
title:  "[Alg] 빅오표기법(대문자 O 표기법) - 계산 복잡도 표현"
excerpt: "어떤 알고리즘이 문제를 풀기 위해 해야 하는 계산이 얼마나 복잡한지를 나타내는 표기법"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, Big O Notation, 빅오표기법, 대문자 O 표기법]

toc: true
toc_sticky: true
 
date: 2023-05-20
last_modified_at: 2023-05-20
---

어떤 알고리즘이 문제를 풀기 위해 해야 하는 계산이 얼마나 복잡한지를 나타내는 정도를 **계산 복잡도<sup>complexity</sup>**라고 한다. 계산 복잡도를 표현하는 방법에는 여러 가지가 있지만, 그 중에서 **빅오표기법<sup>Big-O-Notation</sup>**을 많이 사용한다.

예를 들어 [1부터 N까지의 합을 계산하기](https://98tech-savvy.github.io/algorithm/Alg-Sum-1-to-N/)의 두 가지 방법(일반적 방법, 가우스 방법)을 빅오표기법으로 나타낸다고 해보자.

첫 번째 알고리즘(일반적인 방법)은 입력 크기 n에 대해 덧셈을 N번 수행해야한다. 이 때 이 알고리즘의 계산 복잡도를 **O(n)** 이라고 표현한다. O(n)은 **필요한 계산 횟수가 입력 크기에 '정비례'할 때 쓴다**

*빅오표기법은 필요한 계산 횟수를 표현하는 것이 아니라 입력 크기와의 관계로 표현하는 것이기 때문에 만약 첫 번째 방법에 덧셈을 두 번한다고 해도 똑같이 O(n)이다.*

두 번째 알고리즘(가우스 방법)은 입력 크기 n에 대해 덧셈 한번, 곱셈 한번, 나눗셈 한번 총 사칙연산을 3번 수행한다. 이 때에는 알고리즘의 계산 복잡도를 **O(1)**로 표현한다. 3번 수행하니 O(3)이 아닌가라고 생각할 수도 있지만 **입력 크기가 커져도 계산 시간이 더 늘어나지 않으면 모두 O(1)로 표기한다**

빅오표기법은 대략적으로 알고리즘의 성능을 표시하는 방법이다. 따라서 소요 시간이나 계산 횟수를 표현한다기 보다는 입력 크기 n과 필요한 계산 횟수와의 관계에 더 주목하는 표현이라고 기억해야한다.

# 시간 복잡도와 공간 복잡도
알고리즘의 **계산 복잡도**는 **시간 복잡도와 공간복잡도**로 나눌 수 있다. 시간 복잡도는 알고리즘이 그 계산을 처리하는데 얼마나 많은 시간을 소요하는가이고 공간 복잡도는 알고리즘이 그 계산을 처리하는데 얼마나 많은 메모리가 필요한가?를 따진다.

# 정리

빅오 표기법(Big-O notation)은 아래 특징을 가지며

- **상수항을 무시**
O(n+2) => O(n)
- **계수도 무시**
O(2n) => O(n)
- **최고차항만 표기**
O($3n^2+2n^2+5n+2$) => O($n^2$)

시간 복잡도 표기법이다.

O(n), O(1) 외에도

O(log n)
O(n log n)
O($n^2$)
O($2^n$)

등이 있음.