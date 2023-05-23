---
title:  "[Alg] 팩토리얼 구하기 알고리즘"
excerpt: "1부터 n까지 연속한 정수의 곱을 구하는 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 팩토리얼, \!n]

toc: true
toc_sticky: true
 
date: 2023-05-23
last_modified_at: 2023-05-23
---

# 알고리즘 풀이

## 기본 방식

```python
def fact(n):
    sum = 1
    for i in range(1, n + 1):
        sum *= i
    return sum
```

for문을 반복할 때마다 sum의 값에 i를 곱하고 총 n번 진행한 후 반복문을 나와 결과값을 리턴하는 알고리즘

## 재귀 호출 방식

팩토리얼(n!)의 계산식은 $n! = 1 \times 2 \times 3 \times \cdots  \times n$ 이다. 이걸 팩토리얼로 다시 나타내면 $n! = n \times (n-1)!$으로 나타낼 수 있고, 이걸 파이썬 코드로 나타내보면

```python
def fact(n):
    if n <= 1:
        return 1
    return n * fact(n-1)
```

로 표현할 수 있다. 예를 들어 ``fact(5)`` 일 경우

1. $5 \times fact(4)$
2. $5 \times 4 \times fact(3)$
3. $5 \times 4 \times 3 \times fact(2)$
4. $5 \times 4 \times 3 \times 2 \times fact(1)$
5. $5 \times 4 \times 3 \times 2 \times 1(n<=1 일 때 1을 반환)$

의 순서로 진행되는 것이다.

# 시간 복잡도
재귀 호출 방식에서 순서를 보았듯이 n에 대해 n번(n-1번)이 필요하다.

즉 O(n)