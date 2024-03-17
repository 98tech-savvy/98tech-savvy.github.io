---
title:  "[Python] 파이썬 range 함수"
excerpt: "range 함수에 대해 알아보자"

categories:
  - Python
tags:
  - [Python, 파이썬, range, 레인지, 범위, 반복문]

toc: true
toc_sticky: true

date: 2024-03-18
last_modified_at: 2024-03-18
---

# range
range 함수는 연속된 숫자로 객체를 만드는 함수이다. range의 함수는 매개변수로 총 3개를 입력받을 수 있는데, 첫 번째와 세 번째가 생략가능한 형태로 사용될 수 있다.

``range(param1, param2, param3)``

1. ``param1``
range의 시작 범위를 지정하는 매개변수이다. 0일때는 생략이 가능하다

2. ``param2``
range의 마지막 범위를 지정하는 매개변수이다. 지정된 숫자 바로 앞까지 객체를 생성한다

3. ``param3``
range의 간격을 지정하는 매개변수이다. 생략하면 기본값인 1이 부여되며, 3을 부여했을 때에는 3, 6, 9 식으로 숫자가 증가하는 방식이다.

```py
>>>print(list(range(0, 2)))
[0, 1]
>>>print(list(range(3)))
[0, 1, 2]
>>>print(list(range(3, 11, 3)))
[3, 6, 9]
```