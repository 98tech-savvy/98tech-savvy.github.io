---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 일반 수학"
excerpt: "백준 단계별로 풀어보기 8단계, 일반 수학 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 8단계, 일반 수학]

toc: true
toc_sticky: true

date: 2023-12-12
last_modified_at: 2023-12-12
---

# 2745 - 진법 변환
Z까지 35라면 0부터 시작해서 Z까지 ``index``의 값과 동일하다. 그것을 생각하면 짧게 코드를 작성할 수 있다

```py
base = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
N, B = input().split(" ")

total = 0
fact = 1
for i in range(0, len(N)):
    total += base.index(N[len(N) - i - 1]) * fact
    fact = fact * int(B)

print(total)
```

# 11005 - 진법 변환 2
```py
base = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
N, B = map(int, input().split(" "))

result = []
if N == 0:
    result.append(0)

while N > 0:
    result.append(base[N % B])
    N //= B

result = "".join(result)
print(result[::-1])
```

# 2720 - 세탁소 사장 동혁
```py
coin = [25, 10, 5, 1]

T = int(input())
for _ in range(T):
    cent = int(input())
    count = []
    for i in range(len(coin)):
        count.append(cent // coin[i])
        cent %= coin[i]

    for i in range(len(count)):
        print(f"{count[i]} ", end="")
```

# 2903 - 중앙 이동 알고리즘
```py
# 1번 증가할 때마다 한 변의 점의 갯수는 x*2-1

dot = 2  # 초기 상태의 한 변의 점의 갯수
N = int(input())
for i in range(1, N + 1):
    dot = dot * 2 - 1

print(dot**2)
```

# 2292 - 벌집
```py
# 1, 6, 12, 18, 24
# 1, 7, 19, 37, 61
N = int(input())

count = []
honeycomb = 1
temp = 0
while honeycomb < N:
    honeycomb += temp
    temp += 6
    count.append(honeycomb)

if N == 1:
    print(1)
else:
    print(len(count))
```

# 1193 - 분수찾기
```py
N = int(input())

count = 0
temp = 0
while temp < N:
    count += 1
    temp += count

temp -= N
# 홀수일때는 올라가고 짝수일때는 내려가고

arr = []
for i in range(count, 0, -1):
    arr.append((i, count - i + 1))

if count % 2 == 0:
    print(f"{arr[temp][0]}/{arr[temp][1]}")
else:
    print(f"{arr[len(arr) - (temp + 1)][0]}/{arr[len(arr)-(temp+1)][1]}")
```

# 2869 - 달팽이는 올라가고 싶다
```py
A, B, V = map(int, input().split(" "))
print(((V - A) - 1) // (A - B) + 2)
```


