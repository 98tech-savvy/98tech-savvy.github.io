---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 시간 복잡도"
excerpt: "백준 단계별로 풀어보기 11단계, 시간 복잡도 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 11단계, 시간 복잡도, O(n)]

toc: true
toc_sticky: true

date: 2024-01-09
last_modified_at: 2024-01-09
---

# 24262 - 알고리즘 수업 - 알고리즘의 수행 시간 1
```py
n = int(input())

print(1)
print(0)

```

# 24263 - 알고리즘 수업 - 알고리즘의 수행 시간 2
```py
n = int(input())

print(n)
print(1)

```

# 24264 - 알고리즘 수업 - 알고리즘의 수행 시간 3
```py
n = int(input())

print(n * n)
print(2)

```

# 24265 - 알고리즘 수업 - 알고리즘의 수행 시간 4
```py
n = int(input())

print(n * (n - 1) // 2)
print(2)

```

# 24266 - 알고리즘 수업 - 알고리즘의 수행 시간 5
```py
n = int(input())

print(n * n * n)
print(3)

```

# 24267 - 알고리즘 수업 - 알고리즘의 수행 시간 6
```py
n = int(input())
print((n * (n - 1) * (n - 2) // 6))
print(3)

```

# 24313 - 알고리즘 수업 - 점근적 표기 1 
```py
# O(g(n)) = {f(n) | 모든 n >= n_0에 대하여 f(n) <= c * g(n)인 양의 상수 c와 n_0이 존재함}
# >> n_0보다 큰 n에 대하여 f(n)이 c*g(n)보다 작거나 같음
# f(n) = a1*n + a0
a_1, a_0 = map(int, input().split(" "))
c = int(input())
n_0 = int(input())

# 7 7 8 1 예제 1) f(n) = 7n + 7, g(n) = n, c = 8, n0 = 1이다. f(1) = 14, c × g(1) = 8이므로 O(n) 정의를 만족하지 못한다.
# 7 7 8 10 예제 2) f(n) = 7n + 7, g(n) = n, c = 8, n0 = 10이다. 모든 n ≥ 10에 대하여 7n + 7 ≤ 8n 이므로 O(n) 정의를 만족한다.
# a_i 는 절댓값 0~100 이므로 음수가 될 수도 있음

if (a_1 * +n_0 + a_0) <= c * n_0 and a_1 <= c:
    print(1)
else:
    print(0)

```

