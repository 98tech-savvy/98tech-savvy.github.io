---
title:  "[Python] 런타임 계산하기"
excerpt: "time과 datetime함수를 사용하기"

categories:
  - Python
tags:
  - [Python, 파이썬, time, datetime, 런타임 계산, calculate runtime]

toc: true
toc_sticky: true

date: 2023-09-08
last_modified_at: 2023-09-08
---

1. time 사용
Python에는 내장 모듈 ``time``이 존재한다. 이 ``time``을 활용해서 코드의 전체, 일부의 런타임을 잴 수 있다.

```python
import time
startTime = time.time()

# 코드 ~

runTime = time.time() - startTime

print(f"런타임 : {runTime:.3f}")
```

2. datetime 사용
Python에는 또 다른 내장 모듈 ``datetime``이 존재한다. 이 ``datetime``을 사용하면 날짜 변경으로 인한 계산 오류 등을 예방할 수 있다.

```python
from datetime import datetime

startTime = datetime.now().replace(microsecond=0)

# 코드 ~

endTime = datetime.now().replace(microsecond=0)

print(endTime - startTime)
```