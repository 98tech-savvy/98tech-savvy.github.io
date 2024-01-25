---
title:  "[Python] 람다(lambda)에 관하여"
excerpt: "람다(lambda)에 대해 알아보자"

categories:
  - Python
tags:
  - [Python, 파이썬, key lambda, lambda, 람다]

toc: true
toc_sticky: true

date: 2024-01-26
last_modified_at: 2024-01-26
---

# 람다(lambda)
람다 형식은 인공지능 분야나 AutoCad라는 설계 프로그램에서 쓰이는 Lisp 언어에서 물려받은 함수형 프로그래밍에서 중요한 개념 중 하나로 함수를 한 줄 만으로 구현할 수 있게 해주는 형식을 말하며, 사용 방식은 아래와 같다.

```py
lambda 매개변수 : 표현식
```

``lambda``함수를 활용하면 함수를 간단하게 정의할 수 있다는 장점이 있다.

예를 들어 파이썬으로 ``x+y``를 처리하는 함수를 만들어보자.

```py
def add(x, y):
    return x + y
```

위의 함수도 간단하지만 ``lambda``를 활용하면 아래와 같이 한 줄로 표현할 수 있다.

```py
add = lambda x,y : x+y
```

# 람다(lambda) 함수의 활용

## map()
map 함수는 함수와 리스트를 인자로 받는다.
```py
map(func, list))
```

함수와 리스트를 인자로 받고, 리스트로부터 원소를 하나씩 꺼내서 함수를 적용시킨 다음, 그 결과를 새로운 리스트에 담아준다. 예제를 보자.

```py
list(map(int, input().split(" ")))
```
입력을 " "로 구분해서 받은 이후 입력받은 인자들은 ``int``형으로 하나씩 변환시키고 입력받은 결과물 ``map`` 객체를 다시 ``list``형으로 변환시켜준다.

```py
>>> map(lambda x: x ** 2, range(5))
[0, 1, 4, 9, 16]
```

위 코드는 ``lambda``와 같이 사용되었는데, 1 ~ 5가 순서대로 ``lambda``행을 거쳐 처리된 x가 출력된 모습을 볼 수 있다.

## filter()
filter 함수는 함수와 리스트를 인자로 받는다.
```py
filter(func, list)
```

``filter()`` 함수는 시퀀스(리스트, 튜플 등)의 모든 요소 중 조건에 맞는 원소들을 반환하는 함수이다. ``lambda``와 함께 사용하면 코드를 간결하게 작성할 수 있다는 장점이 있다.

예를 들어 리스트 ``l = [1, 2, 3, 4, 5]``에서 홀수만을 추출하고 싶다면

```py
l = [1, 2, 3, 4, 5]
l_2 = list(filter(lambda x: x % 2 == 1, l))
print(l_2)

>>> [1, 3, 5]
```
와 같이 활용할 수 있다.

## reduce()
reduce 함수는 함수와 시퀀스를 인자로 받는다.
```py
reduce(func, sequence)
```

시퀀스는 문자열, 리스트, 튜플 등을 말하며 reduce 함수는 모든 요소를 누적적으로 계산한 결과를 반환한다. lambda와 같이 사용하면 아래와 같이 사용할 수 있다.

```py
from functools import reduce

l = [1, 2, 3, 4, 5]

result = reduce(lambda x, y : x + y, l)
print(result)

>>> 15
```

lambda 함수로 x + y 형식을 지정해줬고, 그 결과 리스트의 모든 요소를 더한 값 15를 반환한 모습을 볼 수 있다. 쉽게 말해 reduce 함수와 lambda를 같이 사용해 lambda로 계산 방식을 지정해줄 수 있다고 할 수 있다.

## sorted()
sorted 함수는 함수와 시퀀스를 인자로 받는다.
```py
sorted(func, sequence)
```

sorted 함수는 시퀀스(리스트, 튜플 등)의 원소를 정렬한 결과를 반환한다. 이 때 lambda와 함께 활용하면 정렬 기준을 지정할 수 있다. 예를 들어보자.

```py
l = ["What" "is" "happened"]
l_2 = sorted(l, key=lambda x: len(x))
print(l_2)

>>> ["is", "What", "happend"]
```

길이 순으로 정렬하는 코드를 예제로 들어보았다.


