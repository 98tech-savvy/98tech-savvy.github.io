---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 심화 1"
excerpt: "백준 단계별로 풀어보기 6단계, 심화 1 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 6단계, 심화 1]

toc: true
toc_sticky: true

date: 2023-11-30
last_modified_at: 2023-11-30
---

# 25083 - 새싹

```py
print("         ,r'\"7")
print("r`-_   ,'  ,/")
print(" \. \". L_r'")
print("   `~\\/")
print("      |")
print("      |")
```

# 3003 - 킹, 퀸, 룩, 비숍, 나이트, 폰

```py
king, queen, rook, bishop, knight, pawn = map(int, input().split(" "))
king2, queen2, rook2, bishop2, knight2, pawn2 = 1, 1, 2, 2, 2, 8

print(
    f"{king2-king} {queen2-queen} {rook2-rook} {bishop2-bishop} {knight2-knight} {pawn2-pawn}"
)
```

# 2444 - 별 찍기 - 7

```py
N = int(input())
temp = N
for i in range(N):
    for x in range(N - 1):
        print(" ", end="")
    for y in range(2 * i + 1):
        print("*", end="")
    print("")
    if N != 1:
        N -= 1

for i in range(temp):
    for x in range(i + 1):
        print(" ", end="")
    for y in range(2 * temp - 3):
        print("*", end="")
    print("")
    temp -= 1
```

```py
N = int(input())

for i in range(1, N + 1):
    print(" " * (N - i) + "*" * (i * 2 - 1))
for i in range(1, N):
    print(" " * i + "*" * ((N - i) * 2 - 1))
```

# 10988 - 팰린드롬인지 확인하기

```py
word = list(str(input()))

if list(reversed(word)) == word:
    print("1")
else:
    print("0")
```

# 1157 - 단어 공부

```py
word = list(str(input().upper())) # 받아온 문자열을 전부 대문자로 바꾸고 리스트형에 집어넣음
filter_word = list(set(word))

cnt = []
for filter_cnt in filter_word:  # set으로 중복값을 제거한 리스트의 요소를 하나씩 꺼내옴
    count = word.count(filter_cnt)
    cnt.append(count)

if cnt.count(max(cnt)) > 1:
    print("?")
else:
    print(filter_word[cnt.index(max(cnt))])
```

# 2941 - 크로아티아 알파벳

```py
croatia = ["c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="]
string = input()
string2 = []

for _ in range(len(string)):
    for alphabet in croatia:
        if alphabet in string:
            string2.append(alphabet)
            string = string.replace(alphabet, " ", 1)
            break

string = string.split(" ")
string = "".join(string)
string = list(map(str, string))

for i in range(len(string)):
    string2.append(string[i])

print(len(string2))
```

# 1316 - 그룹 단어 체커

```py
N = int(input())
cnt = N

for i in range(N):
    word = input()
    for j in range(len(word) - 1):
        if word[j] == word[j + 1]:
            pass
        elif word[j] in word[j + 1 :]:
            cnt -= 1
            break

print(cnt)

```

# 25206 - 너의 평점은

```py
# 전공평점은 전공과목별 (score * grade)의 합을 sum(score)으로 나눈 값

subjectData = []
sumScore = 0
sumGrade = 0
sumTotal = 0
for i in range(20):
    infoData = []
    subject, score, grade = input().split(" ")

    infoData.append(subject)
    infoData.append(float(score))
    infoData.append(grade)

    subjectData.append(infoData)

    # 과목평점을 점수로 바꿔주는 코드
    if subjectData[i][2] == "A+":
        subjectData[i][2] = 4.5 * subjectData[i][1]
    elif subjectData[i][2] == "A0":
        subjectData[i][2] = 4.0 * subjectData[i][1]
    elif subjectData[i][2] == "B+":
        subjectData[i][2] = 3.5 * subjectData[i][1]
    elif subjectData[i][2] == "B0":
        subjectData[i][2] = 3.0 * subjectData[i][1]
    elif subjectData[i][2] == "C+":
        subjectData[i][2] = 2.5 * subjectData[i][1]
    elif subjectData[i][2] == "C0":
        subjectData[i][2] = 2.0 * subjectData[i][1]
    elif subjectData[i][2] == "D+":
        subjectData[i][2] = 1.5 * subjectData[i][1]
    elif subjectData[i][2] == "D0":
        subjectData[i][2] = 1.0 * subjectData[i][1]
    elif subjectData[i][2] == "F":
        subjectData[i][2] = 0.0 * subjectData[i][1]
    elif subjectData[i][2] == "P":
        subjectData[i][1] = 0
        subjectData[i][2] = 0 * subjectData[i][1]

    sumScore += subjectData[i][1]
    sumGrade += subjectData[i][2]

sumTotal = sumGrade / sumScore
print(sumTotal)
```