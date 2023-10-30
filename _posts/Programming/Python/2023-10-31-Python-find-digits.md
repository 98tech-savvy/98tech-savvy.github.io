---
title:  "[Python] 숫자의 자릿수 분리하기"
excerpt: "자릿수를 분리하는 방법"

categories:
  - Python
tags:
  - [Python, digits, 자릿수, 각 자릿수 찾기, 각 자릿수 구하기, 자리수, 자릿수 분리, 자리수 분리]

toc: true
toc_sticky: true

date: 2023-10-31
last_modified_at: 2023-10-31
---

[백준 2588번: 곱셈](https://www.acmicpc.net/problem/2588)의 문제를 살펴보면, 자릿수를 분리해야하는 과정이 필요하다. 파이썬에서는 어떻게 자릿수를 분리할 수 있을까?

### 자릿수를 분리하는 여러 가지 방법

#### 1. map 함수 활용

```py
num = 123456
numDigits = list(map(int, str(number)))

print(numDigits)

>>> Terminal
[1, 2, 3, 4, 5, 6]
```

위의 코드는 변수 ``num``에 저장된 ``123456``을 ``map``함수를 활용해 ``문자열 123456``으로 바꿔준 후에 ``int``형태로 나누어 ``list``로 저장한 것이다. 이렇게 하면 문자열 → 숫자로 변환하는 방법을 한 번에 해결할 수 있어 편리하다.

#### 2. 수식 활용

```py
n2 = int(input())

tempList = []
for _ in range(len(str(n2))):
    tempList.append(n2 % 10)
    n2 //= 10
tempList.reverse() # 저장된 리스트의 자릿수를 보기좋게 뒤집어줌 (ex: 198 -> (8, 9, 1) -> (1, 9, 8))
print(tempList)
```

``n2``의 길이만큼 반복문을 진행하고 그 안에서 ``tempList``의 요소를 하나씩 추가한다. 이 때 요소의 값은 ``n2 % 10``이며 추가한 이후에 ``n2``의 값을 10으로 나눈 몫을 저장한다