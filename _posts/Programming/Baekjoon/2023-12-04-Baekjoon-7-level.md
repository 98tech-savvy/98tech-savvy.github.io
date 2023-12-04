---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 2차원 배열"
excerpt: "백준 단계별로 풀어보기 7단계, 2차원 배열 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 7단계, 2차원 배열]

toc: true
toc_sticky: true

date: 2023-12-04
last_modified_at: 2023-12-04
---

# 2738 - 행렬 덧셈
```py
N, M = map(int, input().split(" "))

matA = []
for _ in range(N):
    element = list(map(int, input().split(" ")))
    matA.append(element)

matB = []
for _ in range(N):
    element = list(map(int, input().split(" ")))
    matB.append(element)

for i in range(N):
    for j in range(M):
        print(f"{matA[i][j] + matB[i][j]} ", end="")
    print("")
```

# 2566 - 최댓값
```py
table = []
for _ in range(9):
    num = list(map(int, input().split(" ")))
    table.append(num)

max_num = 0
max_width, max_height = 1, 1
for i in range(1, 10):
    if max(table[i - 1]) > max_num:
        max_num = max(table[i - 1])
        max_width = i
        max_height = table[i - 1].index(max_num) + 1
print(max_num)
print(max_width, max_height)
```

# 10798 - 세로읽기
```py
arr = []
max_letter = 0
for _ in range(5):
    letter = list(input())
    arr.append(letter)

    if max_letter < len(letter):
        max_letter = len(letter)

string = ""
for i in range(max_letter):
    for j in range(5):
        try:
            string += arr[j][i]
        except:
            pass

print(string)
```

# 2563 - 색종이
```py
table = []
for i in range(100):
    temp = []
    for j in range(100):
        temp.append(0)
    table.append(temp)

N = int(input())
for _ in range(N):
    x, y = map(int, input().split(" "))
    for i in range(10):
        for j in range(10):
            table[i + x][j + y] = 1

sum = 0
for i in range(100):
    sum += table[i].count(1)

print(sum)
```

