---
title:  "[Python] 스케쥴 모듈(Schedule)로 특정 시간에 작업 예약하기"
excerpt: "스케쥴 모듈로 일정 시간마다 반복 작업을 할 수 있게 만들어보자"

categories:
  - Python
tags:
  - [Python, 파이썬, pip, schedule, 스케쥴, 예약 작업]

toc: true
toc_sticky: true

date: 2023-09-10
last_modified_at: 2023-09-10
---

사용하고있는 터미널에서 

``python.exe -m pip install schedule``를 입력해주면 스케쥴 모듈이 설치 완료된다.

```python
import schedule
import time

def work():
  print("Work :d")

schedule.every(10).second.do(work) # 10초
schedule.every(10).minutes.do(work) # 10분
schedule.every().hour.do(work) # 1시간
schedule.every(10).second.do(work) #10시간 

schedule.every().day.at("01:00").do(work) # 01시 실행
schedule.every().day.at("12:00").do(work) # 12시 실행

schedule.every().monday.do(work) # 월요일 실행

schedule.every().wednesday.at("09:00").do(work) # 수요일 9시 실행

# 무한 루프 문으로 스케쥴을 유지시켜준다
while True:
  schedule.run_pending()
  time.sleep(1)
```