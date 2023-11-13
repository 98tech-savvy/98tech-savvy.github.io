---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 조건문"
excerpt: "백준 단계별로 풀어보기 2단계, 조건문 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 2단계, 조건문]

toc: true
toc_sticky: true

date: 2023-11-04
last_modified_at: 2023-11-04
---

# 1330 - 두 수 비교하기

```py
n1, n2 = map(int, input().split(" "))

if n1 > n2:
    print(">")
elif n1 < n2:
    print("<")
else:
    print("==")
```

# 9498 - 시험 성적

```py
score = int(input())

if 90 <= score <= 100:
    print("A")
elif 80 <= score <= 89:
    print("B")
elif 70 <= score <= 79:
    print("C")
elif 60 <= score <= 69:
    print("D")
else:
    print("F")
```

# 2753 - 윤년

```py
year = int(input())

if year % 4 == 0 and (year % 100 != 0 or year % 400 == 0):
    print("1")
else:
    print("0")
```

# 14681 - 사분면 고르기

```py
x = int(input())
y = int(input())

if 0 < x <= 1000:
    if 0 < y <= 1000:
        print("1")
    if -1000 <= y < 0:
        print("4")
elif -1000 <= x < 0:
    if 0 < y <= 1000:
        print("2")
    if -1000 <= y < 0:
        print("3")
```

# 2884 - 알람 시계

```py
H, M = map(int, input().split(" "))

if M < 45:
    if H == 0:
        H = 23
        M += 60
    else:
        H -= 1
        M += 60

print(f"{H} {M-45}")
```

# 2525 - 오븐 시계

```py
H, M = map(int, input().split(" "))
addM = int(input())

while (M + addM) > 59:
    H += 1
    addM -= 60

if H > 23:
    H = int(H % 24)

print(f"{H} {M+addM}")
```

# 2480 - 주사위 세 개

```py
n1, n2, n3 = map(int, input().split(" "))
reward = 0

if n1 == n2 == n3:
    reward = 10000 + (n1) * 1000
elif n1 == n2 or n1 == n3 or n2 == n3:
    if n1 == n2 or n1 == n3:
        reward = 1000 + (n1) * 100
    else:
        reward = 1000 + (n3) * 100
else:
    reward = max(n1, n2, n3) * 100

print(reward)
```