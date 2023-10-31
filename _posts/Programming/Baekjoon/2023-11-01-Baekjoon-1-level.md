---
title:  "백준 단계별로 풀어보기 - 입출력과 사칙연산"
excerpt: "백준 단계별로 풀어보기 1단계, 입출력과 사칙연산 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 1단계, 입출력과 사칙연산]

toc: true
toc_sticky: true

date: 2023-11-01
last_modified_at: 2023-11-01
---

# 2557 - Hello World

```py
print("Hello World!")
```

# 1000 - A+B

```py
num1, num2 = map(int, input().split(" "))

print(num1+num2)
```

# 1001 - A-B

```py
num1, num2 = map(int, input().split(" "))

print(num1-num2)
```

# 10998 - A*B

```py
num1, num2 = map(int, input().split(" "))

print(num1*num2)
```

# 1008 - A/B

```py
num1, num2 = map(int, input().split(" "))

print(num1/num2)
```

# 10869 - 사칙연산

```py
num1, num2 = map(int, input().split(" "))

print(num1 + num2)
print(num1 - num2)
print(num1 * num2)
print(int(num1 / num2))
print(num1 % num2)
```

# 10926 - ??!

```py
alreadyId = input()

print(f"{alreadyId}??!")
```

# 18108 - 1998년생인 내가 태국에서는 2541년생?!

```py
num1 = int(input())

print(num1 - 543)
```

# 10430 - 나머지

```py
n1, n2, n3 = map(int, input().split())

print((n1 + n2) % n3)
print(((n1 % n3) + (n2 % n3)) % n3)
print((n1 * n2) % n3)
print(((n1 % n3) * (n2 % n3)) % n3)
```

# 2588 - 곱셈

```py
n1 = int(input())
n2 = int(input())

tempN2 = n2
tempList = []
for _ in range(len(str(n2))):
    tempList.append(n2 % 10)
    n2 //= 10

print(n1 * tempList[0])
print(n1 * tempList[1])
print(n1 * tempList[2])
print(n1 * tempN2)
```

# 11382 - 꼬마 정민

```py
n1, n2, n3 = map(int, input().split(" "))

print(n1 + n2 + n3)
```

# 10171 - 고양이

```py
print("\    /\\")
print(" )  ( ')")
print("(  /  )")
print(" \(__)|")
```

# 10172 - 개

```py
print("|\_/|")
print("|q p|   /}")
print('( 0 )"""\\')
print('|"^"`    |')
print("||_/=\\\\__|")
```