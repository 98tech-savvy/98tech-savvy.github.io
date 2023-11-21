---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 문자열"
excerpt: "백준 단계별로 풀어보기 5단계, 문자열 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 5단계, 문자열]

toc: true
toc_sticky: true

date: 2023-11-22
last_modified_at: 2023-11-22
---

# 27866 - 문자와 문자열

```py
S = input()
i = int(input())

print(S[i - 1])
```

# 2743 - 단어 길이 재기

```py
txt1 = input()

print(len(txt1))
```

# 9086 - 문자열

```py
T = int(input())

for _ in range(T):
    string = input()
    print(f"{string[0]}{string[len(string)-1]}")

```

# 11654 - 아스키 코드

```py
textToAscii = input()
print(ord(textToAscii))
```

# 11720 - 숫자의 합

```py
N = int(input())
num = input()

sum = 0
for i in range(N):
    sum += int(num[i])

print(sum)
```

# 10809 - 알파벳 찾기

```py
S = input()

for i in "abcdefghijklmnopqrstuvwxyz":
    print(S.find(i), end=" ")
```

# 2675 - 문자열 반복

```py
T = int(input())

for _ in range(T):
    R, S = input().split(" ")

    P = ""

    for i in range(len(S)):
        for j in range(int(R)):
            P += S[i]
    print(P)
```

# 1152 - 단어의 개수

```py
text = input().split(" ")
text = list(filter(None, text))

print(len(text))
```

# 2908 - 상수

```py
n1, n2 = map(list, input().split(" "))
n1.reverse()
n2.reverse()

n1 = "".join(n1)
n2 = "".join(n2)

if n1 > n2:
    print(n1)
else:
    print(n2)
```

# 5622 - 다이얼

```py
dial = [
    ["A", "B", "C"],
    ["D", "E", "F"],
    ["G", "H", "I"],
    ["J", "K", "L"],
    ["M", "N", "O"],
    ["P", "Q", "R", "S"],
    ["T", "U", "V"],
    ["W", "X", "Y", "Z"],
]

S = input()
total = 0
for x in range(len(S)):
    for i in range(len(dial)):
        for j in range(len(dial[i])):
            if dial[i][j] == S[x]:
                total += dial.index(dial[i]) + 3
print(total)
```

# 11718 - 그대로 출력하기

```py
while True:
    try:
        print(input())
    except:
        break
```