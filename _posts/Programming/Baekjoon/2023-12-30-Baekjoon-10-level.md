---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 기하: 직사각형과 삼각형"
excerpt: "백준 단계별로 풀어보기 10단계, 기하: 직사각형과 삼각형 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 10단계, 기하, 직사각형과 삼각형]

toc: true
toc_sticky: true

date: 2023-12-30
last_modified_at: 2023-12-30
---

# 27323 - 직사각형
```py
A = int(input())
B = int(input())

print(A*B)
```

# 1085 - 직사각형에서 탈출
```py
x, y, w, h = map(int, input().split(" "))

arr = [x, y, w - x, h - y]
print(min(arr))
```

# 3009 - 네 번째 점
```py
from collections import Counter

arrX = []
arrY = []
for _ in range(3):
    x, y = map(int, input().split(" "))
    arrX.append(x)
    arrY.append(y)

countX = Counter(arrX).most_common(n=2)
countY = Counter(arrY).most_common(n=2)

print(countX[1][0], countY[1][0])
```

# 15894 - 수학은 체육과목 입니다
```py
# 밑변 + 1층당 길이 3

n = int(input())

print(n + n * 3)
```

# 9063 - 대지
```py
N = int(input())

arrX = []
arrY = []
for _ in range(N):
    x, y = map(int, input().split(" "))
    arrX.append(x)
    arrY.append(y)

print((max(arrX) - min(arrX)) * (max(arrY) - min(arrY)))
```

# 10101 - 삼각형 외우기
```py
n1 = int(input())
n2 = int(input())
n3 = int(input())

if n1 + n2 + n3 != 180:
    print("Error")
else:
    if n1 == n2 == n3:
        print("Equilateral")
    elif n1 == n2 or n1 == n3 or n2 == n3:
        print("Isosceles")
    elif n1 != n2 and n1 != n3 and n2 != n3:
        print("Scalene")
```

# 5073 - 삼각형과 세 변
```py
while True:
    n1, n2, n3 = map(int, input().split(" "))
    arr = []
    arr.append(n1)
    arr.append(n2)
    arr.append(n3)

    if n1 == n2 == n3 == 0:
        break
    else:
        if max(arr) >= (sum(arr) - max(arr)):
            print("Invalid")
        else:
            if n1 == n2 == n3:
                print("Equilateral")
            elif n1 == n2 or n1 == n3 or n2 == n3:
                print("Isosceles")
            elif n1 != n2 and n1 != n3 and n2 != n3:
                print("Scalene")
```

# 14215 - 세 막대
```py
# 길이를 줄일 수는 있지만, 늘릴 수는 없음
# 삼각형이 될 수 있는 조건 : 두 변의 길이의 합이 나머지 한 변의 길이보다 커야함(가장 긴 변 < 나머지 두 변)
arr = list(map(int, input().split(" ")))

if max(arr) >= (sum(arr) - max(arr)):
    arr[arr.index(max(arr))] = (sum(arr) - max(arr)) - 1
    print(sum(arr))
else:
    print(sum(arr))

```

