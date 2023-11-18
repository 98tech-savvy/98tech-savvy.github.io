---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 1차원 배열"
excerpt: "백준 단계별로 풀어보기 4단계, 1차원 배열 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 4단계, 1차원 배열]

toc: true
toc_sticky: true

date: 2023-11-18
last_modified_at: 2023-11-18
---

# 10807 - 개수 세기
```py
arrSize = int(input())
if arrSize >= 1 and arrSize <= 100:
    arr1 = list(map(int, input().split(" ")))

    findNum = int(input())
    findNumCnt = 0
    if findNum >= -100 and findNum <= 100:
        for i in range(0, len(arr1)):
            if arr1[i] == findNum:
                findNumCnt += 1
print(findNumCnt)
```

# 10871 - X보다 작은 수
``map``함수를 이용해 입력받고 입력받은 ``map``객체를 ``list``형태로 변환해주면 쉽게 끝나는 문제

```py
N, X = map(int, input().split(" "))
arrA = list(map(int, input().split(" ")))

for i in range(N):
    if arrA[i] < X:
        print(f"{arrA[i]} ", end="")
```

# 10818 - 최소, 최대
```py
# 백준 10818 - 최소, 최대

T = int(input())

arr = list(map(int, input().split(" ")))
print(f"{min(arr)} {max(arr)}")

```

# 2562 - 최댓값
최댓값 찾기 알고리즘을 이용하면 쉽게 풀 수 있다. 값을 입력받고, 입력받은 값의 첫 번째 ``arr[0]``을 ``max`` 변수에 저장한다. 그리고 반복문으로 입력받은 값만큼 반복시키고 ``arr[i]``의 값이 ``max``의 값보다 클 경우 ``max``에 ``arr[i]``를 저장한다.

```py
# 백준 2562 - 최댓값

arr = []
for i in range(0, 9):
    arr.append(int(input()))

max = arr[0]
for i in range(0, 9):
    if max < arr[i]:
        max = arr[i]

print(max)
print(arr.index(max)+1)
```

# 10810 - 공 넣기
```py
# 백준 10810 - 공 넣기

bucketSize, balls = map(int, input().split(" ")) # 바구니(양동이)와 공의 갯수를 정해줌
buckets = [0] * (bucketSize) # buckets 라는 1차원 배열을 선언하고 숫자 0을 bucektSize만큼 추가함

for _ in range(balls): # 반복문에 반복숫자를 사용할 일이 없으면 _(언더바) 사용
    i, j, k = map(int, input().split(" ")) # i바구니 ~ j바구니, 공의 숫자 k
    for x in range(i, j+1):
        buckets[x-1] = k # 배열의 인덱스는 0부터 시작하므로 1을 빼줌, 만약 이 1도 거슬린다면 배열의 갯수 자체를 bucketSize+1을 해주면 print할 때 문제는 없음

for bucket in buckets:
    print(bucket, end=" ") # 문자의 끝을 기본인 개행문자(\n)이 아닌 " "(공백)으로 바꿔줌
```

# 10813 - 공 바꾸기
```py
# 백준 10813 - 공 바꾸기

N, M = map(int, input().split(" "))

buckets = []
for i in range(0, N + 1):
    buckets.append(i)  # 바구니의 자리에 바구니 번호에 맞는 숫자를 넣어줌

for _ in range(M):
    i, j = map(int, input().split(" "))  # 바꿀 바구니의 번호 입력

    temp = buckets[i]
    buckets[i] = buckets[j]
    buckets[j] = temp

buckets.remove(0) # 배열의 첫 번째 인덱스 0을 없애줌
for bucket in buckets:
    print(bucket, end=" ")
```

# 5597 - 과제 안 내신 분..?
```py
# 백준 5597 - 과제 안 내신 분..?

students = []
for i in range(31):
    students.append(i)
students.remove(0)

for i in range(28):
    n = int(input())
    students.remove(n)

print(min(students))
print(max(students))
```

# 3052 - 나머지
```py
# 백준 3052번 - 나머지

arr1 = []
for i in range(0, 10):
    arr1.append(int(input()) % 42)

print(len(set(arr1)))
```

# 10811 - 바구니 뒤집기
```py
# 백준 10811 - 바구니 뒤집기

N, M = map(int, input().split(" "))

buckets = []
for i in range(0, N + 1):
    buckets.append(i)

for _ in range(M):
    i, j = map(int, input().split(" "))

    temp = []
    for x in range(i, j + 1):
        temp.append(buckets[x])
    temp.reverse()
    for x in range(len(temp)):
        buckets[i + x] = temp[x]

buckets.remove(0)

for bucket in buckets:
    print(bucket, end=" ")
```

# 1546 - 평균
```py
# 백준 1546번 - 평균

subjectCnt = int(input())  # 시험 본 과목의 개수 N
tempScore = list(map(int, input().split(" ")))
maxScore = max(tempScore)

newList = []
for score in tempScore:
    newList.append(score / maxScore * 100)
avg = sum(newList) / subjectCnt
print(avg)
```
