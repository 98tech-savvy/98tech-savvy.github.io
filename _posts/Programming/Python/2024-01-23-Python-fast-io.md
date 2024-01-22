---
title:  "파이썬으로 빠른 입출력하기"
excerpt: "input, print를 대신할 빠른 입출력에 대해 알아보자"

categories:
  - Python
tags:
  - [Python, input, print, 인풋, 아웃풋, sys, sys.stdin.readline]

toc: true
toc_sticky: true

date: 2024-01-23
last_modified_at: 2024-01-23
---

프로그래밍 대회나 코딩 테스트에서, 파이썬으로 문제를 풀다보면 빠듯한 시간에 코드가 '시간 초과 오류'가 날 확률이 높다. 파이썬은 다른 언어에 비해 무거운 언어라 입출력 자체만으로도 시간 초과가 날 수도 있기 때문에, 파이썬으로 코딩 테스트나 대회에 나가기 위해서는 빠른 입출력을 위한 방법을 기본적으로 알아야 한다.

```py
import sys
input = sys.stdin.readline
print = sys.stdout.write 
```

위 세 줄로 ``input``과 ``print``를 ``sys.stdin.readline``과 ``sys.stdout.write``로 바꿔버린다. 그러면 원래 쓰던 것 처럼 input, print문을 사용해도 이전 것과 달리 빠른 입출력이 이루어지는 모습을 볼 수 있다.

# 주의할 점
1. ``input()`` 은 개행문자 ``\n``까지 읽어드리기 때문에 ``sys.stdin.readline``에서는 ``.rstrip()``으로 개행문자를 지워주어야한다.

2. ``print()``는 ``print("".join(변수)) + "\n"``처럼 변수를 저런식으로 넣고 개행문자도 직접 추가해주어야 한다