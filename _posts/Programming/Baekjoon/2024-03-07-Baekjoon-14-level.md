---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 집합과 맵"
excerpt: "백준 단계별로 풀어보기 14단계, 집합과 맵 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 14단계, 집합과 맵, 집합과 맵 정답]
toc: true
toc_sticky: true

date: 2024-03-07
last_modified_at: 2024-03-07
---

# 10815 - 숫자 카드
```py
import sys

print = sys.stdout.write
input = sys.stdin.readline

N = int(input())
arr = list(map(int, input().split()))
arr.sort()

M = int(input())
table = list(map(int, input().split()))

for i in range(len(table)):
    answer = 0
    start = 0
    end = len(arr) - 1

    while start <= end:
        middle = (start + end) // 2

        if table[i] == arr[middle]:
            answer = 1
            break
        elif table[i] > arr[middle]:
            start = middle + 1
        elif table[i] < arr[middle]:
            end = middle - 1

    print("".join(str(answer) + " "))

```

# 14425 - 문자열 집합
```py
import sys

print = sys.stdout.write
input = sys.stdin.readline

N, M = map(int, input().split(" "))

findStr = [0] * N
for i in range(N):
    findStr[i] = str(input()).rstrip()

chkStr = [0] * M
for i in range(M):
    chkStr[i] = str(input()).rstrip()

answer = 0
for i in chkStr:
    if i in findStr:
        answer += 1

print("".join(str(answer)))

```

# 7785 - 회사에 있는 사람
```py
import sys

print = sys.stdout.write
input = sys.stdin.readline

n = int(input())
arr = set()

for i in range(n):
    name, io = input().split()

    if io == "enter":
        arr.add(name)
    else:
        arr.remove(name)

arr = sorted(arr, reverse=True)
for i in range(len(arr)):
    print("".join(arr[i]) + "\n")

```

# 1620 - 나는야 포켓몬 마스터 이다솜
```py
import sys

print = sys.stdout.write
input = sys.stdin.readline

N, M = map(int, input().split())

pokeDic = {}
for i in range(1, N + 1):
    name = str(input()).rstrip()
    pokeDic[i] = name
    pokeDic[name] = i

temp = [0] * M
for i in range(M):
    temp[i] = input().rstrip()

for i in range(M):
    if temp[i].isdigit():
        print("".join(pokeDic[int(temp[i])] + "\n"))
    else:
        print("".join(str(pokeDic[temp[i]]) + "\n"))

```

# 10816 - 숫자 카드 2
```py
import sys

input = sys.stdin.readline

N = int(input())
numCard = list(map(int, input().split(" ")))
M = int(input())
myCard = list(map(int, input().split(" ")))

answer = {}

for i in myCard:
    answer[i] = 0

for i in numCard:
    if i in answer:
        answer[i] += 1

for i in myCard:
    print(f"{answer[i]} ", end="")

```

# 1764 - 듣보잡
```py
# 사전순 - sorted
import sys

input = sys.stdin.readline

N, M = map(int, input().split(" "))

cantHear = [0] * N
for i in range(N):
    cantHear[i] = input().rstrip()

cantSee = [0] * M
for i in range(M):
    cantSee[i] = input().rstrip()

cantHear = set(cantHear)
cantSee = set(cantSee)

answer = sorted(list(cantHear & cantSee))
print(len(answer))
for i in range(len(answer)):
    print(answer[i])

```

# 1269 - 대칭 차집합
```py
import sys

input = sys.stdin.readline

N, M = map(int, input().split(" "))

A = set(map(int, input().split(" ")))
B = set(map(int, input().split(" ")))
C = (A - B) | (B - A)

print(len(C))
```

# 11478 - 서로 다른 부분 문자열의 개수
```py
import sys

input = sys.stdin.readline

S = input().rstrip()

answer = []

j = 1
for i in range(len(S)):
    for j in range(i, len(S)):
        answer.append(S[i : j + 1])

print(len(set(answer)))

```