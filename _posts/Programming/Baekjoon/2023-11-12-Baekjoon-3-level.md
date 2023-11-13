---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 반복문"
excerpt: "백준 단계별로 풀어보기 3단계, 반복문 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 3단계, 반복문]

toc: true
toc_sticky: true

date: 2023-11-12
last_modified_at: 2023-11-12
---

# 2739 - 구구단

```py
num = int(input())

for i in range(1, 10):
    print(f"{num} * {i} = {num*i}")
```

# 10950 - A+B -3

```py
T = int(input())

for i in range(0, T):
    n1, n2 = map(int, input().split(" "))
    print(n1 + n2)
```

# 8393 - 합

```py
n = int(input())

temp = n
for i in range(n):
    n += temp - (i + 1)
    
print(n)
```

# 25304 - 영수증

```py
totalPrice = int(input())
totalCount = int(input())

for i in range(totalCount):
    Price, Count = map(int, input().split(" "))
    totalPrice -= Price * Count

if totalPrice == 0:
    print("Yes")
else:
    print("No")
```

# 25314 - 코딩은 체육과목입니다

```py
num = int(input())
if int(num % 4) == 0 and num <= 1000:
    for i in range(0, int(num / 4)):
        print("long ", end="")
    print("int")
```

# 15552 - 빠른 A+B

```py
import sys

input = sys.stdin.readline

T = int(input())

for i in range(T):
    n1, n2 = map(int, input().split(" "))
    print(n1 + n2)
```

# 11021 - A+B -7

```py
# 백준 11021 - A+B -7

T = int(input())
for i in range(T):
    A, B = map(int, input().split(" "))
    print(f"Case #{i+1}: {A+B}")
```

# 11022 - A+B -8

```py
T = int(input())

for i in range(T):
    A, B = map(int, input().split(" "))
    print(f"Case #{i+1}: {A} + {B} = {A+B}")
```

# 2438 - 별 찍기 -1

```py
num = int(input())

for i in range(0, num):
    for j in range(0, i + 1):
        print("*", end="")
    print("")
```

# 2439 - 별 찍기 -2

```py
num = int(input())

for i in range(0, num):
    for j in range(0, num - (i + 1)):
        print(" ", end="")
    for k in range(0, i + 1):
        print("*", end="")
    print("")
```

# 10952 - A+B -5

```py
while 1:
    A, B = map(int, input().split(" "))
    if A == 0 and B == 0:
        break

    print(A + B)
```

# 10951 - A+B -4

```py
while 1:
    try:
        A, B = map(int, input().split(" "))
        print(A + B)
    except:
        break
```