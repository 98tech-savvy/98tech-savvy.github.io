---
title:  "[Python] selenium 기능 정리"
excerpt: "selenium의 기능 정리"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, selenium, selenium 기능 정리]

toc: true
toc_sticky: true

date: 2023-05-15
last_modified_at: 2023-05-15
---

이전에 크롬 자동화 방법에 대해 설명한 글이 있다. 

[웹 스크래핑](https://98tech-savvy.github.io/python/Python-Webscraper/)
[웹 사이트 자동화](https://98tech-savvy.github.io/python/Python-Auto-login-naver/)

위 글을 참고하고, 이 포스팅은 많이 쓸 것 같은 기능들을 정리해놓은 글이다.


# 동적 페이지 로딩 대기
```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.supprt import expected_conditions as EC

browser = webdriver.Chrome()
browser.maximize_window() # 창 크기 최대화
browser.get('Link') # 해당 링크를 열음

try:
  # 해당 요소가 로딩될 때 까지 10초를 기다림, 10초안에 로딩되면 대기 시간 종료
  elem = WebDriverWait(browser, 10).until(EC.presence_of_element_located((By.셀렉터, "요소 값"))) 
except:
```

# 동적 페이지 스크롤

## 첫 번째 방법
```python
import time
from selenium import webdriver

browser = webdriver.Chrome()
~

# 1920x1080해상도에서 1080만큼 스크롤을 내림
browser.execute_script('window.scrollTo(0, 1080')) 

# 화면 가장 아래로 스크롤을 내림
browser.execute_script('window.scrollTo(0, document.body.scrollHeight)')
```
## 두 번째 방법
```python
import time
from selenium import webdriver

browser = webdriver.Chrome()
~

# 현재 문서 높이
prev_height = browser.execute_script('return document.body.scrollHeight')

while True:
  browser.execute_script('window.scrollTo(0, document.body.scrollHeight)')

  time.sleep(2)

  # 내린 문서의 높이 저장
  curr_height = browser.execute_script('return document.body.scrollHeight')
  if curr_height == prev_height:
    break

  prev_height = curr_height
```

# 특정 영역 스크롤

클릭하면 자동으로 스크롤을 내려주지만, 내리는걸 직접 보고싶다거나 할 때 사용

# 첫 번째 방법, ActionChains

```python
import time
from selenium import webdriver
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.by import By

browser = webdriver.Chrome()

# CSS 셀렉터로 저장
elem = browser.find_element(By.CSS_SELECTOR, "요소 값")

# ActionChains
actions = ActionChains(browser)
actions.move_to_element(elem).perform()

```

## 두 번째 방법, 좌표 정보

```python
import time
from selenium import webdriver
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.by import By

browser = webdriver.Chrome()

# CSS 셀렉터로 저장
elem = browser.find_element(By.CSS_SELECTOR, "요소 값")

# 좌표 정보
xy = elem.location_once_scrolled_into_view


```

# 핸들
쉽게 말해서 브라우저 창을 바꿔주는 거라고 생각하면 된다.

이전에 웹 브라우저에서 자동화를 하나 할 때는 새 창을 하나 띄워놓고 했지만, 창을 하나 더 띄운다면 핸들이라는 녀석을 바꿔주어야 한다.

```python
import time
from selenium import webdriver

browser = webdriver.Chrome()
~
# 현재 윈도우 핸들 정보
curr_handle = browser.current_window_handle

browser.find_element(~).click() # 새 창이 열림(핸들이 하나 더 생김)

handles = browser.window_handles # 모든 핸들 정보
for handle in handles:
  print(handle) # 각 핸들 정보
  browser.switch_to.window(handle) # 각 핸들로 이동함
  print(browser.title)
  print()

browser.switch_to_window(curr_handle) # 원래 핸들로 돌아옴
```