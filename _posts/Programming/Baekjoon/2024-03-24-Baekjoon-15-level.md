---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 약수, 배수와 소수 2"
excerpt: "백준 단계별로 풀어보기 15단계, 약수, 배수와 소수 2 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 15단계, 약수, 배수와 소수 2, 약수, 배수와 소수 2 정답]
toc: true
toc_sticky: true

date: 2024-03-24
last_modified_at: 2024-03-24
---

# 1934 - 최소공배수
```py
import sys

input = sys.stdin.readline


def gcd(a, b):
    while b > 0:
        a, b = b, a % b
    return a


T = int(input())
arr = [0] * T
for i in range(T):
    arr[i] = list(map(int, input().split(" ")))
    gcd_result = gcd(arr[i][0], arr[i][1])
    print(gcd_result * (arr[i][0] // gcd_result) * (arr[i][1] // gcd_result))

```

# 13241 - 최소공배수
```py
def gcd(a, b):
    while b > 0:
        a, b = b, a % b
    return a


a, b = map(int, input().split(" "))

print((a * b) // gcd(a, b))

```

# 1735 - 분수 합
```py
import sys

input = sys.stdin.readline

A, B = map(int, input().split(" "))
C, D = map(int, input().split(" "))

denominator = B * D
molecule = A * D + B * C


def gcd(A, B):
    while B > 0:
        A, B = B, A % B
    return A


gcd_result = gcd(denominator, molecule)
print(f"{int(molecule/gcd_result)} {int(denominator/gcd_result)}")

```

# 2485 - 가로수
```py
import sys

input = sys.stdin.readline

N = int(input())

# 가로수 크기, 가로수 간격을 저장하고 정렬
gapList = [0] * (N - 1)
gap = int(input())
for i in range(N - 1):
    num = int(input())
    gapList[i] = num - gap
    gap = num


# 최대공약수
def gcd(a, b):
    while b > 0:
        a, b = b, a % b
    return a


isGcd = gapList[0]
for i in range(1, len(gapList)):
    isGcd = gcd(isGcd, gapList[i])

# 최소수
cnt = 0
for i in range(len(gapList)):
    cnt += gapList[i] // isGcd - 1

print(cnt)
```

# 4134 - 다음 소수
```py
import sys
import math

input = sys.stdin.readline


def primeNumber(x):
    if x < 2:
        return False
    for i in range(2, int(math.sqrt(x) + 1)):
        if x % i == 0:
            return False

    return x


T = int(input())

for i in range(T):
    num = int(input())
    while True:
        if primeNumber(num) == False:
            num += 1
        else:
            break

    print(num)

```

# 1929 - 소수 구하기
```py
import sys

input = sys.stdin.readline


def prime_number(m, n):
    primes = [False, False] + [True] * (n - 1)  # 0,1은 False

    for i in range(2, int(n ** (0.5) + 1)):
        if primes[i] == True:
            for j in range(i * 2, n + 1, i):  # i*2 부터 n+1까지 i 단위로 반복함
                primes[j] = False

    for index in range(m, n + 1):
        if primes[index]:
            print(index)


m, n = map(int, input().split(" "))

prime_number(m, n)

```

# 4948 - 베르트랑 공준
```py
import sys

input = sys.stdin.readline

arr = [0] * 2 + [1] * 246912 # 123456까지 수 제한이 있으므로 2n의 범위인 246912까지 배열 선언

for i in range(2, 246913):
    if arr[i]:
        for j in range(i * 2, 246913, i): # 에라토스테네스의 체에서 소수의 배수를 없애는 순서
            arr[j] = 0

while True:
    num = int(input())
    if num == 0:
        break
    print(sum(arr[num+1:num*2+1]))
```

# 17103 - 골드바흐 파티션
```py
import sys

input = sys.stdin.readline

# 에라토스테네스의 체로 미리 소수를 담아두는 배열을 만듬
arr = [0] * 2 + [1] * 999999
for i in range(2, 1000001):
    if arr[i]:
        for j in range(i * 2, 1000001, i):
            arr[j] = 0

T = int(input())  # 테스트 케이스

for i in range(T):
    count = 0  # 정답을 담을 변수
    N = int(input())
    for j in range(2, N//2+1):
        if arr[j] and arr[N - j]:
            count += 1
    print(count)

```

# 13909 - 창문 닫기
```py
# import sys

# input = sys.stdin.readline

# for N in range(27):
#     arr = [0] * N

#     for i in range(N):
#         for j in range(i + 1, N, i + 1):
#             arr[j - 1] = 1 if arr[j - 1] == 0 else 0
#     print(f"{N} : {sum(arr)}")

n = int(input())
print(int(n**0.5))

```

