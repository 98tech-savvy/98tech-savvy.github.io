---
title:  "[Alg] 최대공약수 구하기 알고리즘"
excerpt: "두 자연수 a와 b의 최대공약수를 구하는 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 최대공약수, Greatest-common-divisor]

toc: true
toc_sticky: true
 
date: 2023-05-25
last_modified_at: 2023-05-25
---

# 최대공약수
최대공약수는 두 개 이상의 정수의 공통 약수 중에서 가장 큰 값을 의미한다.
예를 들어 6과 12의 최대공약수는 6이다

두 개 이상의 정수의 약수 들의 교집합 중에서 가장 큰 값이라고 생각하면 된다.

$\lbrace1,2,3,6\rbrace \cap \lbrace1,2,3,4,6,12\rbrace = \lbrace1,2,3,6\rbrace$ - 공통약수
6 - 최대공약수

두 자연수 a와 b의 최대공약수를 파이썬으로 구해보자.

1. 두 자연수 a와 b중 작은 값을 찾는다
2. 작은 값을 저장하고 그 수를 a와 b를 동시에 나눠 나머지가 없을 때 i를 리턴한다
3. i의 값을 하나씩 줄여서 반복한다

```python
def func(a, b):
    i = min(a, b)
    print(f"i = {i}")

    while True:
        if a % i == 0 and b % i == 0:
            return i
        i -= 1
```

min함수를 이용해 작은 값을 i에 저장하고 무한루프(while True:)문에서 나머지가 0인 값을 return한다. 만약 0으로 나눠지지않는다면 i를 1줄이고 다시 무한루프한다.

# 유클리드 알고리즘
수학자 유클리드(Euclid)는 최대공약수에 다음과 같은 성질이 있다는걸 발견했다.
> a와 b의 최대공약수는 'b'와 'a를 b로 나눈 나머지'의 최대공약수와 같다.
⇒ gcd(a, b) = gcd(b, a % b)

> 어떤 수와 0의 최대공약수는 자기 자신이다.
⇒ gcd(a, 0) = a

예를 들어 60과 24의 최대공약수는

``gcd(60, 24) = gcd(24, 60 % 24) = gcd(24, 12) = gcd(12, 24 % 12) = gcd(12, 0) = 12``

몇 번 과정을 진행하지 않았는데도 최대공약수가 나옴을 확인할 수 있다.

그러면 파이썬으로 이 유클리드 알고리즘을 구현해보자.

```python
def func(a, b):
    if a % b == 0:
        return b
    return func(b, a % b)
```

재귀함수를 사용해 간단하게 최대공약수를 구하는 알고리즘을 만들어냈다.

# 시간복잡도
일반적인 방법은 모든 정수를 나눠보기 때문에 O(n)
유클리드 방법은 [O(log n)](https://dandalf.tistory.com/123)으로 시간복잡도의 효율성이 더 좋다.