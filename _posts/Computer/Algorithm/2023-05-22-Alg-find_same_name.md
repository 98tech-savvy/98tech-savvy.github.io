---
title:  "[Alg] 동명이인 찾기 알고리즘"
excerpt: "같은 이름을 가진 서로 다른 사람들 찾기"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 동명이인, 동명이인 찾기, 같은 이름 찾기]

toc: true
toc_sticky: true
 
date: 2023-05-22
last_modified_at: 2023-05-22
---

이름들을 원소로 가진 리스트에서 동명이인들만을 찾아서 집합에 저장하는 알고리즘

{TOM, JERRY, JAKE, JILL, TOM} 이라는 원소들이 있다고 할 때
첫 번째 원소부터 뒤의 원소들을 차례대로 자신과 맞는지 검사한다.

TOM -> JERRY
TOM -> JAKE
TOM -> JILL
TOM -> TOM

이후 동명이인인 TOM을 결과에 저장하고 그 다음 원소인 JERRY부터 검사한다

JERRY -> JAKE
JERRY -> JILL
JERRY -> TOM

그 다음

JAKE -> JILL
JAKE -> TOM

그 다음

JILL -> TOM

이 때 마지막 원소인 TOM은 모든 원소들과 검사를 했기 때문에 굳이 검사를 하지 않는다.

1번째 원소 -> 검사 n-1번
2번째 원소 -> 검사 n-2번
.
.
.
n번째 원소 -> 검사 n-n번



```python
import random


def samename(names):
    num = len(names)  # 리스트 개수를 r에 저장
    print("리스트 개수 : {}".format(num))

    result = set()  # 결과를 집합(set)으로 저장함

    for i in range(0, num - 1):  # 동명이인을 처리하는 for문
        for j in range(i + 1, num):
            if names[i] == names[j]:
                result.add(names[i])
    return result


def main():
    names = ["Tom", "Jerry", "Jake", "Parin", "Jerry", "Tom", "Jill", "Zoi"]
    print(samename(names))


if __name__ == "__main__":
    main()
```

```python
    for i in range(0, num - 1):  # 동명이인을 처리하는 for문
        for j in range(i + 1, num):
            if names[i] == names[j]:
                result.add(names[i])
```

에서
``for i in range(0, num -1)``은 원소를 첫 번째부터 n-1번째(마지막 바로 전)까지 검사하겠다는 것이고

``for j in range(i+1, num)``은 첫 번째 원소(i)의 다음 번째(i+1)부터 마지막 원소(num)까지 검사하겠다는 것이다.


# 시간복잡도
빅오표기법으로 나타내면 O($n^2$) 이 된다.

이전의 포스팅에서 1+2+3+...+n 의 합은 $sqrt{n^2/3}$