---
title:  "[Python] Selenium 셀레니움 element를 찾지 못할 때"
excerpt: "셀레니움의 find_element 를 해도 요소를 찾지 못한다."

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, Scarper, 스크랩, 크롤링, 스크래퍼]

toc: true
toc_sticky: true

date: 2023-06-18
last_modified_at: 2023-06-18
---

네이버 지도같은 동적 사이트에서, 크롤링을 하기 위해 셀레니움을 활용해 요소 찾기를 시도했는데, 아무리 바꿔도, 셀렉터를 바꿔도 찾지 못한다

그럴 때는 내가 찾는 프레임의 body 안에 그 요소가 없는건데, html에는 iframe이라는 기술이 있어 html안에 다른 html을 집어넣을 수 있다.

그 iframe에 접근하는 방법
```python
frame = browser.find_element(By.CSS_SELECTOR, "iframe#searchIframe")

browser.switch_to.frame(frame)
```

searchIframe 이라는 iframe에 접근해서 switch_to.frame() 을 통해 프레임을 iframe으로 바꿔주었다.

여기서 찾는 요소를 시도하면 찾을 수 있을 것이다.