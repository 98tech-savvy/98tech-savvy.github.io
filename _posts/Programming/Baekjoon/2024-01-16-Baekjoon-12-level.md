---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 브루트 포스"
excerpt: "백준 단계별로 풀어보기 12단계, 브루트 포스 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 12단계, 브루트 포스, O(n)]

toc: true
toc_sticky: true

date: 2024-01-16
last_modified_at: 2024-01-16
---

# 2798 - 블랙잭
```py
N, M = map(int, input().split(" "))
arr = list(map(int, input().split(" ")))

temp = 0
for i in range(N - 2):
    for j in range(i + 1, N - 1):
        for k in range(j + 1, N):
            sumArr = sum((arr[i], arr[j], arr[k]))
            if sumArr > M:
                pass
            elif sumArr <= M:
                if temp < sumArr:
                    temp = sumArr

print(temp)
```

# 2231 - 분해합
```py
# 216만큼 작은 수 반복, str으로 숫자 나눠서 for 문으로 다시 더 한 값이 맞을 때 break하고 출력

N = int(input())

cons = []
for i in range(1, N):
    sum = i
    list_str = list(str(i))
    for string in list_str:
        sum += int(string)

    if sum == N:
        cons.append(i)

if len(cons) == 0:
    print(0)
else:
    print(min(cons))
```

# 19532 - 수학은 비대면강의입니다
```py
a, b, c, d, e, f = map(int, input().split(" "))

for i in range(-999, 1000):
    for j in range(-999, 1000):
        if ((a * i) + (b * j) == c) and ((d * i) + (e * j) == f):
            print(i, j)
            break
```

# 1018 - 체스판 다시 칠하기
```py
# 8 <= N, M <= 50
N, M = map(int, input().split(" "))

table = []
for i in range(N):
    table.append(input())

answer = []
for i in range(N - 7):
    for j in range(M - 7):
        white = 0
        black = 0
        for x in range(i, i + 8):
            for y in range(j, j + 8):
                if (x + y) % 2 == 0:
                    if table[x][y] != "W":
                        white += 1
                    if table[x][y] != "B":
                        black += 1
                else:
                    if table[x][y] != "B":
                        white += 1
                    if table[x][y] != "W":
                        black += 1

        answer.append(white)
        answer.append(black)

print(min(answer))

```

# 1436 - 영화감독 숌
```py
N = int(input())
cnt, num = 0, 665
while True:
    num += 1
    if str(num).count("666") >= 1:
        cnt += 1

    if cnt == N:
        break

print(num)
```

# 2839 - 설탕 배달
```py
N = int(input())  # 3 <= N <= 5000

answer = []
for i in range(1001):  # 5 * 1000 = 5000
    for j in range(1668):  # 3 * 1667 = 5001
        if i * 5 + j * 3 == N:
            answer.append(i + j)

if len(answer) == 0:
    print(-1)
else:
    print(min(answer))
```