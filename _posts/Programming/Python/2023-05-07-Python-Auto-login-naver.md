---
title:  "[Python] 웹 사이트 자동화"
excerpt: "파이썬과 웹 스크래핑을 활용해 네이버의 로그인을 자동으로 해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, 웹 스크래핑, 웹 크롤링, 파이썬, 웹 사이트 자동화]

toc: true
toc_sticky: true

date: 2023-05-07
last_modified_at: 2023-05-07
---

# 이전 포스팅
이전 포스팅에 웹 스크래핑의 기본과 웹 스크래핑을 하는데 필요한 모듈들의 기초에 대해 공부했다.

이번에는 새 모듈들을 활용해서 네이버에 자동으로 로그인해보는 프로그램을 작성해보겠다.

request의 경우 동적인 홈페이지의 소스 코드를 제대로 긁어오지 못한다는 단점이 있다.
그럴 때 selenium을 사용해주면 동적인 소스 코드를 가져올 수 있다.

# 코드

```python
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.edge.options import Options
from selenium.webdriver.common.by import By

# 크롬 드라이버 자동 업데이트
from webdriver_manager.microsoft import EdgeChromiumDriverManager

import time
import pyautogui
import pyperclip

# 브라우저 꺼짐 방지
edge_options = Options()
edge_options.add_experimental_option("detach", True)

# 불필요한 에러 메세지 없애기
edge_options.add_experimental_option("excludeSwitches", ["enable-logging"])

service = Service(executable_path=EdgeChromiumDriverManager().install())
driver = webdriver.ChromiumEdge(service=service, options=edge_options)

# 웹페이지 해당 주소 이동
driver.maximize_window()
driver.implicitly_wait(5)
driver.get("https://nid.naver.com/nidlogin.login?mode=form&url=https%3A%2F%2Fwww.naver.com")

# 아이디 입력 창
id = driver.find_element(By.CSS_SELECTOR, "#id")
id.click()
pyperclip.copy("id")
pyautogui.hotkey("ctrl", "v")
time.sleep(2)

# 패스워드 입력 창
pw = driver.find_element(By.CSS_SELECTOR, "#pw")
pw.click()
pyperclip.copy("password")
pyautogui.hotkey("ctrl", "v")
time.sleep(2)


# 패스워드 입력 창
btnLogin = driver.find_element(By.CSS_SELECTOR, "#log\.login")
btnLogin.click()

```

완성된 코드이다. 굉장히 간단하면서도 처음보는 녀석들로 가득하다.

```python
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.edge.options import Options
from selenium.webdriver.common.by import By

# 크롬 드라이버 자동 업데이트
from webdriver_manager.microsoft import EdgeChromiumDriverManager

import time
import pyautogui
import pyperclip
```

이 부분의 모듈들을 설명하자면

자동화를 위한 selenium 모듈
웹 드라이버를 자동으로 설치해주고 업데이트해주기 위한 webdriver_manager 모듈
기본내장 시간 time모듈
핫키를 써주기위한 pyautogui 모듈
클립보드에 복사를 하기 위한 pyperclip 모듈이다.

```python
# 브라우저 꺼짐 방지
edge_options = Options()
edge_options.add_experimental_option("detach", True)

# 불필요한 에러 메세지 없애기
edge_options.add_experimental_option("excludeSwitches", ["enable-logging"])

service = Service(executable_path=EdgeChromiumDriverManager().install())
driver = webdriver.ChromiumEdge(service=service, options=edge_options)

# 웹페이지 해당 주소 이동
driver.maximize_window()
driver.implicitly_wait(5)
driver.get("https://nid.naver.com/nidlogin.login?mode=form&url=https%3A%2F%2Fwww.naver.com")

```

위의 선언한 모듈중 Options 객체 edge_options를 만들어주고

브라우저가 꺼지지않게 하기 위한 .add_experimental_option("detach", True), 터미널에 잡다한 에러메시지가 보기 싫다면 "excludeSwitches", ["enable-logging"]

그리고 driver로 엣지에 대한 변수를 선언해주고

maximize_window() 창 크기 최대화
implicitly_wait(5) 5초 동안 대기해줌 
get(네이버 로그인 주소) 네이버 로그인 주소를 브라우저(엣지)로 띄어줌

```python
# 아이디 입력 창
id = driver.find_element(By.CSS_SELECTOR, "#id")
id.click()
pyperclip.copy("id")
pyautogui.hotkey("ctrl", "v")
time.sleep(2)

# 패스워드 입력 창
pw = driver.find_element(By.CSS_SELECTOR, "#pw")
pw.click()
pyperclip.copy("password")
pyautogui.hotkey("ctrl", "v")
time.sleep(2)


# 패스워드 입력 창
btnLogin = driver.find_element(By.CSS_SELECTOR, "#log\.login")
btnLogin.click()
```

띄운 로그인 주소 창에서 이전에 배운 스크래핑을 활용해서 id텍스트박스, pw텍스트박스, 로그인버튼의 셀렉터값을 구해주고(find_element와 By사용)

- .click() 해당 요소를 클릭함
- pyperclip.copy("id") id값을 클립보드에 복사함
- pyautogui.hotkey("ctrl", "v") CTRL+V, 즉 윈도우에서 붙여넣기를 실행함
- time.sleep(2) 너무 빨리 입력하면 자동방지문자 창으로 넘어가기 때문에 2초동안 대기 시켜줌

의 공통적인 과정을 거쳐서 실행만 해서 로그인을 해보았다.