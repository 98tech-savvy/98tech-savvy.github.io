---
title:  "내 컴퓨터의 User-agent 확인하기"
excerpt: "스크래핑에 사용하는 User-agent를 확인하는 사이트"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, Scarper, 스크랩, 크롤링, 스크래퍼, User-agent]

toc: true
toc_sticky: true

date: 2023-06-16
last_modified_at: 2023-06-16
---


[What is my User-agent](https://www.whatismybrowser.com/detect/what-is-my-user-agent/)

위 링크에 들어가면 아래의 사진과 같은 사이트가 뜨게 된다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/9df17561-c98f-4b72-8aef-303a39e13a0e)

여기서 USER-AGENT 라고 적혀있는 부분을 python에 적어주면 된다.

셀레니움에서 USER-AGENT를 적용하는 방법은

```python
options = webdriver.EdgeOptions()

options.add_argument(
    "--user-agent=YOUR_USER-AGENT"
)
```

와 같이 추가해주면 된다.