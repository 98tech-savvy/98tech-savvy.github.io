---
title:  "[Python] 정적 타입 언어처럼 사용하기"
excerpt: "동적 언어인 Python을 정적 언어처럼 사용해보자"

categories:
  - Python
tags:
  - [Python, 파이썬, 동적 언어, 정적 언어]

toc: true
toc_sticky: true

date: 2023-09-12
last_modified_at: 2023-09-12
---

# 동적 타입 언어와 정적 타입 언어
프로그래밍 언어는 **변수의 타입이 정해지는 시점**에 따라 크게 **두 가지**로 나누어진다. 바로 동적 타입 언어와 정적 타입 언어인데, 두 언어의 차이점은 다음과 같다.

1. 동적 타입 언어
동적 타입(Dynamically Typed) 언어는 런타임 시점에 변수의 타입이 결정되는 언어이다. 따라서 코드에 미리 데이터의 자료형을 결정해 줄 필요가 없다는 편리함이 있지만, 코딩 시에 타입의 제한이 없기 때문에 런타임 단계에서 데이터의 자료형으로 인한 오류가 발생할 수 있다.

2. 정적 타입 언어
정적 타입(Statically Typed) 언어는 컴파일 시점에 변수의 타입이 결정되는 언어이다. 이를 위해서는 코드에 미리 데이터의 자료형을 명시해주어야하며, 그로 인해 타입 에러로 인한 문제를 컴파일 단계에서 해결할 수 있기 때문에 안정성이 높다는 장점이 있다. 그리고 컴파일 시에 미리 타입을 결정하기 때문에 생산속도가 높다. 하지만 프로그래밍의 유연성이 낮다는 단점이 있다.

# Python을 정적 타입 언어 처럼
Python은 **동적 타입 언어**이다. Python을 정적 타입 언어처럼 사용하려면 자료형에 대한 지침을 부여해주면 되는데, 이건 **Python 3.5**부터 가능한 기능이다.

```python
a: int = 1
```
a를 int형 자료형이라고 지침을 부여한 것이다. 또 함수나 클래스의 파라미터에도 타입 힌트를 적용할 수 있다.