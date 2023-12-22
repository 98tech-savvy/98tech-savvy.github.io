---
title:  "[Python] collections 모듈의 Counter 함수 알아보기"
excerpt: "빈도수를 알아내는 내장 함수 Counter"

categories:
  - Python
tags:
  - [Python, collections, Counter, 빈도 수, 빈도 수 알아내기, 내장 함수]

toc: true
toc_sticky: true

date: 2023-12-23
last_modified_at: 2023-12-23
---

파이썬에는 강력하고 기본적인 내장함수들이 많이 있다. 그 중에 ``collections``모듈의 ``Counter``함수에 대해 알아보자.

# Counter
``collections``모듈의 ``Counter``함수는 별도의 패키지 설치가 없어도 파이썬만 설치되어 있다면 임포트해서 사용할 수 있는 기본 내장 함수이다.

아래와 같은 코드로 사용할 수 있으며
``from collections import Counter``

```py
from collections import Counter

A = ["A", "B", "B", "A", "A", "A", "B", "C"]
countA = Counter(A)

print(countA)

-------------------------------
>> Counter({'A': 4, 'B': 3, 'C': 1})
```

``Counter({'A': 4, 'B': 3, 'C': 1})``와 같이 딕셔너리 형태로 각각의 수를 카운트해줘서 저장하는 모습을 볼 수 있다.

> 여러 형태의 데이터를 인자로 받고 먼저 중복된 데이터가 배열을 인자로 넘기고 각 원소를 카운트한 후 딕셔너리 형태로 반환함

문자열을 인자로 넘길 시에는 각각의 문자에 대해 카운트를 센다.

## 실전 사용
실전에서 사용할 때에는 대부분 **빈도 수**를 찾기 위해 많이 사용한다. '가장 많이 쓰는 숫자' 라던가 '가장 적게 쓰는 숫자' 라던가를 찾을 때 말이다. 이 때 ``Counter``함수에는 ``most_common``이라는 데이터의 개수가 많은 순대로 리턴해주는 메서드를 제공하고있다.

```py
from collections import Counter

print(Counter("Hello world").most_common(n=2)) # n의 개수에 따라 얼마나 많은 데이터를 리턴할 것인지 선택 2일때는 데이터가 많은 1등, 2등을 리턴한다

--------------------------------
>> [('l', 3), ('o', 2)]
```

## 산술 연산자 사용
``Counter``객체는 특이하게도 객체끼리에 산술 연산자를 사용할 수 있다.
예를 들어

```py
counter1 = Counter(["A", "B", "A"])
counter2 = Counter(["A", "B", "B"])
```
가 있다면 이 두객체를 더해서

```py
print(counter1 + counter2)
---------------------------
>> Counter({'A': 3, 'B': 3})
```
이라는 출력 결과를 나오게 할 수도 있고, 뺄셈도 가능하다. 이 때 뺄셈의 결과로 ``0``이나 음수가 나온 경우에 최종 카운터 객체에서 제외가 된다.