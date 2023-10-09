---
title:  "재귀함수"
excerpt: "재귀함수란"

categories:
  - CS
tags:
  - [CS, Recursive function, 재귀 함수]

toc: true
toc_sticky: true

date: 2023-10-10
last_modified_at: 2023-10-10
---

# 부분곱이란?
$\prod$의 의미는 $\sum$와 유사한데, 아래 수식에서 볼 수 있듯이 주어진 숫자를 모두 곱하라는 뜻이다.
 

Python에서 
$\prod$을 구현하는 방법들은 아래와 같다.


```python
# with for loop
def prod_for(data: list) -> float:
    """product all elements in data with for loop"""

    res = 1
    for i in data:
        res *= i
    return res


# with recursion
def prod_rec(data: list) -> float:
    """product all elements in data with recursion"""

    return data[0] if len(data) == 1 else data[0] * prod_rec(data[1:])


# use built-in module
from math import prod

data = [1, 2, 3, 4, 5]

print(prod_for(data))
print(prod_rec(data))
print(prod(data))

120
120
120
```

# 재귀함수 
재귀함수(recursive function)는 아래 함수처럼 함수 내에서 자기 자신을 다시 호출하는 함수를 말한다.

```py
def prod_rec(data: list) -> float:
    """product all elements in data with recursion"""

    return data[0] if len(data) == 1 else data[0] * prod_rec(data[1:])


def factorial_rec(n: int):
    """returns factorial of number"""

    return 1 if n <= 1 else n * factorial_rec(n - 1)

Python의 최대 재귀 깊이(maximum recursion depth)는 기본적으로 1,000으로 설정되어 있는데, 아래와 같이 확인할 수 있다.

import sys

print(sys.getrecursionlimit())

1000
```

Python에서 최대 재귀 깊이를 수정하려면 아래와 같이 설정하면 된다.

```py
import sys

sys.setrecursionlimit(2000)

print(sys.getrecursionlimit())

2000
```

위와 같이 최대 재귀 스택 오버플로우로 인한 오류를 해결하기 위해서 꼬리재귀(tail recursion)이라는 것을 사용한다.

함수의 결과로 호출하는 함수가 자기 자신이고 재귀 호출이 끝난 뒤 추가적인 연산이 필요하지 않다면 꼬리재귀라고 볼 수 있다. 위에서 구현한 팩토리얼 함수를 꼬리재귀 형태로 변형하면 아래와 같다.

```py
def factorial_rec(n: int, res: int = 1) -> int:
    """returns factorial of number with recursion"""

    return res if n <= 1 else factorial_rec(n - 1, n * res)
```
꼬리재귀를 사용하려면 프로그래머가 꼬리재귀 형식으로 프로그래밍을 했는지와 별개로, 해당 언어가 꼬리재귀를 지원해야한다. Python은 꼬리재귀 최적화를 지원하지 않아서 위 함수를 사용해도 스택 오버플로우가 발생한다