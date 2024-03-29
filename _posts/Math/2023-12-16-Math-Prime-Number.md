---
title:  "[수학 개념] 소수의 판별, 에라토스테네스의 체"
excerpt: "소수를 판별하는 방법에 대해 알아보자"

categories:
  - Math
tags:
  - [Math, 수학, 수학 개념, 에라토스테네스의 체, 소수, 소수의 판별, 소수 알고리즘, 소수 판별 알고리즘]

toc: true
toc_sticky: true

date: 2023-12-16
last_modified_at: 2023-12-16
---

# 소수란
**소수<sup>Prime Number</sup>**란 2보다 큰 자연수 중에서 **1과 자기 자신을 제외한 자연수로는 나누어떨어지지 않는 자연수를** 말한다. 예를 들어 3은 1과 3으로밖에 나누어지지 않으므로 3은 소수이며, 6은 1, 2, 3, 6의 약수를 가지고 있으므로 소수가 아니다.

# 소수를 구하는 코드

# 쉬운 방법
해당 수가 소수임을 판별하는 방법은 1과 자기 자신을 제외한 자연수로 나누어보는 것이다. 즉, N이 주어지면 N을 2부터 N-1까지의 모든 수로 나누어보고 나머지가 존재하지 않는 경우 소수가 아님을 판별할 수 있다.

```py
def isPrimeNumber(N):
    for i in range(2, N):
        if N % i == 0 # 나머지가 존재하지 않는다면
            return False # 소수가 아님
        return True # 맞을 경우 참을 반환
```

# 에라토스테네스의 체
에라토스테네스의 체 알고리즘은 소수를 판별할 때 사용하는 대표적인 알고리즘이다. 동작 방식은 다음과 같다.
1. 2부터 N까지의 모든 자연수를 나열한다
2. 남은 수 중에 처리하지 않은 가장 작은 수 i를 찾는다
3. 남은 수 중에 i의 배수를 모두 제거한다(i는 제거하지 않음)
4. 더 이상 반복할 수 없을 때까지 2번과 3번 과정을 반복한다.

숫자 18을 예시로 들어보자.
||||||
|--|--|--|--|--|
||2|3|4|5|
|6|7|8|9|10|
|11|12|13|14|15|
|16|17|18|||

남은 수 중에 아직 처리하지 않은 가장 작은 수(2)를 제외하고 그 수의 배수를 전부 제거한다(2, 4, 6, 8, 10, 12, 14, 16, 18).

||||||
|--|--|--|--|--|
||2|3||5|
||7||9||
|11||13||15|
||17||||

남은 수 중에 아직 처리하지 않은 가장 작은 수(3)를 제외하고 그 수의 배수를 전부 제거한다(3, 9, 15)

||||||
|--|--|--|--|--|
||2|3||5|
||7||||
|11||13|||
||17||||

남은 수 중에 아직 처리하지 않은 가장 작은 수(5)를 제외하고 그 수의 배수를 전부 제거한다

||||||
|--|--|--|--|--|
||2|3||5|
||7||||
|11||13|||
||17||||

남은 수 중에 아직 처리하지 않은 가장 작은 수(7)를 제외하고 그 수의 배수를 전부 제거한다

... 반복하면 2, 3, 5, 7, 11, 13, 17이 나오고 이 수들은 전부 **소수**임을 알 수 있다.

이 알고리즘을 파이썬으로 구현해보자.

## 에라토스테네스의 체 코드
```py
import math

n = int(input())
arr = [True for i in range(n + 1)]  # n만큼의 배열을 만들고 그 수를 전부 True로 채워줌

# 쉬운 방법에서 n의 제곱근(가운데 약수)만큼 확인해도 답이 나오는데 지장이 없어서 math.sqrt(n) 활용해 코드 개선
for i in range(2, int(math.sqrt(n)) + 1):
    if arr[i] == True:  # i가 소수일 때(남은 수)
        j = 2  # 배수
        while i * j <= n:
            arr[i * j] = False  # 수를 False로 바꿔줌
            j += 1

for i in range(2, n + 1):
    if arr[i]:
        print(i, end=" ")
```

에라토스테네스의 체 알고리즘의 시간복잡도는 O(NloglogN)이다.