---
title:  "Selenium 셀레니움 div 스크롤하기"
excerpt: "웹 페이지 안의 div를 스크롤 하는 방법"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, Scarper, 스크랩, 크롤링, 스크래퍼]

toc: true
toc_sticky: true

date: 2023-06-28
last_modified_at: 2023-06-28
---

공부의 일환으로 댓글을 스크랩해오는 스크래퍼 기능을 만들고 있었다.

그러다가 div 박스 안에 구현된 댓글 리스트를 스크롤 했어야 했는데 이게 아무리 원래 했던 방법인

```python
# 현재 스크롤 위치 가져오기
scroll_position = 0
scroll_height = browser.execute_script("return document.documentElement.scrollHeight")

# 페이지 끝까지 스크롤 다운
while scroll_position < scroll_height:
    # 스크롤 다운
    browser.execute_script("window.scrollTo(0, document.documentElement.scrollHeight);")

    # 대기 시간 부여
    time.sleep(2)

    # 스크롤 위치와 높이 갱신
    scroll_position = scroll_height
    scroll_height = browser.execute_script("return document.documentElement.scrollHeight")
```

당연히 되지 않았다. **문서의 <body> 부분이라 div 박스를 내릴 수는 없었다** 그래서 구글링해서 div 박스 자체를 건드리는 코드를 찾았다.

```python
# 페이지 스크래핑을 위한 반복문
while True:
    # div 스크롤 하기
    browser.execute_script("arguments[0].scrollBy(0, 4000)", inner_page)
    time.sleep(1)
```