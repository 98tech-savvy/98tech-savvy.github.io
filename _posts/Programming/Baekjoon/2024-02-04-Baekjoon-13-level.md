---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 정렬"
excerpt: "백준 단계별로 풀어보기 13단계, 정렬 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 13단계, 정렬, O(n)]

toc: true
toc_sticky: true

date: 2024-02-04
last_modified_at: 2024-02-04
---

# 2750 - 수 정렬하기
```py
N = int(input())
arr = []
for _ in range(N):
    arr.append(int(input()))

for i in range(N):
    for j in range(N - 1):
        if arr[j] > arr[j + 1]:
            temp = arr[j + 1]
            arr[j + 1] = arr[j]
            arr[j] = temp

for i in range(N):
    print(arr[i])
```

# 2587 - 대표값2
```py
# 평균 = sum(배열)/len(배열)
# 중앙값 = sort => 다섯 개 이므로 arr[2]

arr = []
for i in range(5):
    arr.append(int(input()))

# 버블 정렬로 오름차순으로 정렬
for i in range(5):
    for j in range(4):
        if arr[j] > arr[j + 1]:
            temp = arr[j + 1]
            arr[j + 1] = arr[j]
            arr[j] = temp

print(int(sum(arr) / len(arr)))  # 평균 출력
print(arr[2])  # 중앙값 출력
```

# 25305 - 커트라인
```py
"""
1 ≤ N ≤ 1\,000
1 ≤ k ≤ N
0 ≤ x ≤ 10\,000
"""

N, k = map(int, input().split(" "))
x = list(map(int, input().split(" ")))

for i in range(N):
    for j in range(N - 1):
        if x[j] < x[j + 1]:
            temp = x[j + 1]
            x[j + 1] = x[j]
            x[j] = temp

print(x[k - 1])
```

# 2751 - 수 정렬하기 2
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input().rstrip())

arr = []
for _ in range(N):
    arr.append(int(input()))

arr.sort()
for i in range(len(arr)):
    print("".join(str(arr[i])) + "\n")
```

# 10989 - 수 정렬하기 3
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input().rstrip())

Counting = [0] * 10001  # 카운팅 정렬, 범위가 1 <= X <= 10000 이므로 10001의 크기를 가진 배열을 0으로 초기화

for _ in range(N):
    s = int(input().rstrip())
    Counting[s] += 1

for i in range(10001):
    if Counting[i] != 0:
        for j in range(Counting[i]):
            print("".join(str(i)) + "\n")
```

# 1427 - 소트인사이드
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = list(input())

temp = ""
for i in range(len(N)):
    for j in range(len(N) - 1):
        if N[j] < N[j + 1]:
            temp = N[j + 1]
            N[j + 1] = N[j]
            N[j] = temp

print("".join(N))
```

# 11650 - 좌표 정렬하기
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input())

coordinates = [0] * N
for i in range(N):
    coordinates[i] = list(map(int, input().split(" ")))

coordinates.sort(key=lambda x: (x[0], x[1]))

for i in range(N):
    answer = str(coordinates[i][0]) + " " + str(coordinates[i][1]) + "\n"
    print("".join(answer))
```

# 11651 - 좌표 정렬하기 2
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input())

coordinates = [0] * N
for i in range(N):
    coordinates[i] = list(map(int, input().split(" ")))

coordinates.sort(key=lambda x: (x[1], x[0]))

for i in range(N):
    answer = str(coordinates[i][0]) + " " + str(coordinates[i][1]) + "\n"
    print("".join(answer))
```

# 1181 - 단어 정렬
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input())

arr = [0] * N
for i in range(N):
    arr[i] = str(input())

arr = list(set(arr))
arr.sort(key=lambda x: (len(x), x))

for i in range(len(arr)):
    print("".join(arr[i]))
```

# 10814 - 나이순 정렬
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input())

arr = [0] * N
for i in range(N):
    arr[i] = list(map(str, input().split(" ")))
    arr[i][0] = int(arr[i][0])

# 조건
# 1. 나이가 증가하는 순
# 2. 나이가 같으면 먼저 가입한 사람이 앞에 오는 순

arr.sort(key=lambda x: (x[0]))

for i in range(len(arr)):
    answer = str(arr[i][0]) + " " + arr[i][1]
    print("".join(answer))
```

# 18870 - 좌표 압축
```py
import sys

input = sys.stdin.readline
print = sys.stdout.write

N = int(input())
values = list(map(int, input().split()))

arr = [0] * N
for i in range(N):
    arr[i] = values[i]

setArr = list(set(arr))  # 중복된 값 제거
setArr.sort()  # 정렬

dictArr = {
    value: i for i, value in enumerate(setArr)
}  # 새로운 배열 setArr에 인덱스를 부여한 dictArr을 만듬

for value in arr:
    print("".join(str(dictArr.get(value))) + " ")
```

