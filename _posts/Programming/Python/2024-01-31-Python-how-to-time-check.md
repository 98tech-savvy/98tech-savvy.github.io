---
title:  "[Python] 프로그램 실행 시간 알아보기"
excerpt: "내 프로그램이 몇 초만에 끝나는지 궁금하다면"

categories:
  - Python
tags:
  - [Python, 파이썬, time, sys, 실행 시간, 종료 시간]

toc: true
toc_sticky: true

date: 2024-01-31
last_modified_at: 2024-01-31
---

가끔씩 코딩을 하거나 문제를 풀다보면 내가 짠 프로그램의 실행 속도가 어느 정도 되는지 궁금할 때가 있다. 그 때는 ``time` 모듈을 사용하면 되는데, 사용방법은 아래와 같다.

```py
import time
import sys

start = time.time()

input = sys.stdin.readline

N = list("1231231231453434352132")

temp = ""
for i in range(len(N)):
    for j in range(len(N) - 1):
        if N[j] < N[j + 1]:
            temp = N[j + 1]
            N[j + 1] = N[j]
            N[j] = temp

print("".join(N) + "\n")

end = time.time()

print(f"{end - start} sec")
```

먼저 코드의 첫 번째 줄에 start 변수를 만들고 시작 시간(``time.time()``은 코드 실행 시간을 저장함)을 저장하고 코드의 마지막 줄에 end 변수를 만들고 종료 시간을 기록해준 후 end - start로 종료 시간과 시작 시간을 뺄셈하면 프로그램의 실행 시간이 된다.

1. 코드의 시작에 start 변수를 만들고 시작 시간을 저장함
2. 코드의 끝에 end 변수를 만들고 종료 시간을 저장함
3. 코드의 맨 마지막에 end - start로 시간을 계산한 후 출력함