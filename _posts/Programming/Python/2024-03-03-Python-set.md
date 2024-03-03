---
title:  "[Python] 파이썬 set 집합 연산 : 합집합, 교집합, 차집합"
excerpt: "집합 자료형인 set으로 집합 연산을 해보자"

categories:
  - Python
tags:
  - [Python, 파이썬, set, 집합 연산, 집합, 집합 자료형, 합집합, 교집합, 차집합, intersection, union, difference]

toc: true
toc_sticky: true

date: 2024-03-03
last_modified_at: 2024-03-03
---

# 집합 자료형, set
set은 '집합 자료형'이다. 그리고 이 '집합'은 수학에서 말하는 집합과 같다. 집합의 특성과 같이 **순서가 없고, 중복적인 요소를 허용하지 않는다.**
또 set type에서는 **합집합, 교집합, 차집합같은 수학 연산을 사용할 수 있다**. 보통 set을 활용해 특정 값을 남기는데 활용할 수 있다.

## 합집합, | union
파이썬에서 합집합은 '|' 나 'union'으로 연산할 수 있다. 파이썬의 합집합도 수학에서의 합집합과 마찬가지로 A집합과 B집합의 원소들을 더한 C집합을 만들 수 있다.

```py
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
set3 = set1 | set2
set4 = set1.union(set2)

>>> set1 = {1, 2, 3, 4}
>>> set2 = {3, 4, 5, 6}
>>> set3 = {1, 2, 3, 4, 5 ,6}
>>> set4 = {1, 2, 3, 4, 5, 6}
```

## 교집합, & intersection
파이썬에서 교집합은 '&'나 'intersection'으로 연산할 수 있다. 파이썬의 교집합도 수학에서의 교집합과 마찬가지로 A집합과 B집합의 공통 원소만을 C집합으로 만들 수 있다.

```py
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
set3 = set1 & set2
set4 = set1.intersection(set2)

>>> set1 = {1, 2, 3, 4}
>>> set2 = {3, 4, 5, 6}
>>> set3 = {3, 4}
>>> set4 = {3, 4}
```

## 차집합, - difference
파이썬에서 차집합은 '-' 나 'difference'로 연산할 수 있다. 파이썬의 차집합도 수학에서의 차집합과 마찬가지로 B집합이 가진 원소들을 A집합에서 뺀 C집합을 만들 수 있다.

```py
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
set3 = set1 - set2
set4 = set1.difference(set2)

>>> set1 = {1, 2, 3, 4}
>>> set2 = {3, 4, 5, 6}
>>> set3 = {1, 2}
>>> set4 = {1, 2}
```