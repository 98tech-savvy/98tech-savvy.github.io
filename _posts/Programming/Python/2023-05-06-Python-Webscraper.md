---
title:  "웹 스크래핑"
excerpt: "파이썬을 활용해 웹 사이트의 데이터를 가져오는 프로그램을 만들어보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, 웹 스크래핑, 웹 크롤링, WebScraper, re, requests]

toc: true
toc_sticky: true

date: 2023-05-06
last_modified_at: 2023-05-06
---

# 웹 스크래핑과 웹 크롤링의 차이점
웹 스크래핑과 웹 크롤링의 차이점은 웹 크롤링은 웹 페이지의 링크를 통해서 계속해서 정보를 찾아나가지만 웹 스크래핑은 특정 웹 사이트에서만 데이터를 추적한다는 차이가 있다. 또 스크래핑의 경우 원하는 데이터만 추출하는 기술이기 때문에 웹 크롤링과 다르게 중복된 데이터를 지워줘야하는 구문을 추가해주지 않아도 된다.

**웹 크롤링 - 기존의 복사본을 만듬**
**웹 스크래핑 - 분석을 위한 특정 데이터를 추출하거나 새로운 것을 만듬**

웹 스크래핑을 수행하기 위해서는 웹 크롤링 같은 작업을 선행해주어야 한다.

# VSCODE
VSCODE에서 웹 테스트를 편하게 하기 위해서 **OPEN IN BROWSER** 확장 기능을 설치해주었다.

```
이름: open in browser
ID: techer.open-in-browser
설명: This allows you to open the current file in your default browser or application.
버전: 2.0.0
게시자: TechER
VS Marketplace 링크: https://marketplace.visualstudio.com/items?itemName=techer.open-in-browser
```

VSCODE의 탐색기에서 웹 파일(html)에 우클릭을 했을 때 OPEN IN ... BROWSER 가 생기고 이 버튼을 통해 html을 좀 더 빠르게 열 수 있다.

VSCODE를 사용하기 전에는 NOTEPAD++로 html파일을 구경하곤했었는데, VSCODE로 html파일을 작성하니 이렇게 편하다고? 하며 놀랐다. 시작(ex <html>)을 입력하면 자동으로 끝(ex </html>)코드를 추가해주고 큰 따옴표까지 자동으로 달아주고 커서마저 그 안에 위치한 걸 보고있자니.. 감격스러웠다!

# xpath
html에는 수 많은 태그가 있고, 태그 안에 태그가 있고 그 태그안에 또 다른 태그가 있고(**부모, 자식 관계**라고도 한다).. 식으로 만들어진다. 예를들어 ``/html/body/div/div/div/div/div/span/a...``식으로 말이다. 만약 사이트가 더 커지고 복잡해진다면 위의 예시보다 더 길어질 것이 분명하다. 이 때 사용하는 것이 **xpath**인데, 쉽게 말해서 **학번, 군번**같은 자신을 나타내주는 증명번호? 라고 생각해주면 된다. 만약 내가 찾을게 '로그인'이라면 ``//*[@id ="login"]/a`` 등의 유저가 지정해준 id(xpath)값으로 접근하는 식으로 쉽게 찾아낼 수 있다. 

**xpath 는 경로를 간략하게 나타낸 것이고, full xpath는 경로를 전부 나타낸 것이다**

# requests
터미널에서 ``pip install requests``를 통해 requests 모듈을 설치해주고,

```python
import requests

res = requests.get("http://naver.com")

print(res.status_code)
```

를 해보면 '200'을 출력하는 것을 볼 수 있다. 이 때 200이면 정상, 403이면 접근불가를 뜻 한다.

정상적으로 접근했는지를 보려면

```python
if res.status_code == requests.codes.ok:
    print("정상")
else:
    print("문제가 생김 {}".format(res.status_code))
```

를 해줄 수도 있지만 간단하게

```python
res.raise_for_status()
```

를 통해 정상적으로 접근했는지를 알아낼 수도 있다.
정상적으로 접근했다면 받아온 페이지를 확인할 수 있는데,

```python
print(res.text)
```
를 하면 받아온 페이지의 코드를 확인할 수 있다.

터미널에서 보면 굉장히 난잡한데 파일로 받아보면 좀 더 쉽게 확인할 수 있다.

```python
with open("mycopyhtml", "w", encoding="utf8") as f:
    f.write(res.text)
```

## 403이 뜨는 이유
사이트에서 데이트를 얻어올 때, 사이트에 접속하게 될텐데 이 때 사이트는 우리들의 헤더정보(출입정보)를 얻어낼 수 있다. 이 때 웹스크래핑을 방지해놓았다면(데이터 탈취, 서버 과부하등의 이유) 403이 뜨는 것이다.

# 정규식
[정규식](https://98tech-savvy.github.io/computer/CS-Programming-language-process/#%EC%A0%95%EA%B7%9C%EC%8B%9D)은 링크의 게시글에서 찾아볼 수 있듯이 '언어를 지정하기 위한 언어'이다. 주민등록번호의 뒷 자리, 차량의 번호 등 문자열의 일정한 패턴을 표현하는 일종의 형식 언어인데, python에서는 ``import re``를 통해 정규식 모듈을 사용할 수 있다.

```python
import re

p = re.compile("ca.e")

# . : 하나의 문자를 의미 (ex: ca.e ---> care, cafe, case)
# ^ : 문자열의 시작을 의미 (ex: ^el ---> eliminate, elepant)
# $ : 문자열의 끝을 의미 (ex: se$ ---> case, base)

m = p.match("cafe")
print(m.group())
```

p는 보통 패턴을 뜻한다. 그래서 패턴이 ca.e이고
m을 통해 cafe가 p의 패턴에 맞는지 매칭시켜본다. 일치한다면(cafe는 일치함)정상적으로 출력하고 caffe라면 비정상이므로 애트리뷰트 에러를 발생시킬 것이다.

에러를 발생시키지않고싶다면

```python
m = p.match("매칭시킬 문장")

if m:
    print(m.group())
else:
    print("매칭되지 않음")
```

식으로 표현할 수 있다. match함수는 **주어진 문자열의 처음부터 일치하는지 확인**하는 함수이기 때문에 careless 같은 경우는 care를 프린트하지만 'i don't care'같은 문장은 "매칭되지 않음"을 프린트 하는걸 볼 수 있다.

i don't care에서 care를 찾고 싶다면

``m = p.search("")``처럼 search함수를 사용해주면 된다. search함수는 문자열 중에 일치하는게 있는지 확인하는 함수이다.

i don't care를 그대로 출력하고 싶다면

``m.string()``을 해주면 된다.

|코드|설명|
|---|---|
|---M|---|
|group|일치하는 문자열 반환|
|string|입력받은 문자열 반환|
|start|일치하는 문자열의 시작 index 반환|
|end|일치하는 문자열의 끝 index 반환|
|span|일치하는 문자열의 시작과 끝 index 반환|
|---P|---|
|match|문자열의 처음부터 일치하는지 확인해서 반환|
|search|문자열 중에 일치하는 것을 반환|
|findall|일치하는 모든 것을 리스트 형태로 반환|

즉 re모듈을 활용하기 위해서는

1. p = re.compile("원하는 형태")
정규식 활용

2. m = p.match~search("비교할 문자열") or lst = p.findall("비교할 문자열")

정규식에 대해 더 공부하고 싶다면 [w3school](https://www.w3schools.com/)을 활용해주면 좋다. 영어가 가능하신 분들이 보기 편할 듯 하다.

# User Agent
[User Agent, What is my browser?](https://www.whatismybrowser.com/detect/what-is-my-user-agent/)의 링크에 들어가보면 자신의 User Agent를 확인할 수 있는데, 접속하는 브라우저(웨일, 크롬, 엣지 등등)에 따라 자신의 User Agent가 달라진다.

위의 [403이 뜨는 이유 헤더 부분](http://98tech-savvy.github.io/python/Python-Webscraper/#403%EC%9D%B4-%EB%9C%A8%EB%8A%94-%EC%9D%B4%EC%9C%A0)을 보면 사이트는 헤더 정보를 읽어서 접근을 거부할 수 있다고 설명했다. 이 때 자신의 User Agent를 입력해주면, 접근 거부된 사이트에서 접근을 할 수 있다.

```python
import requests
url = "URL 주소"
headers = {"User-Agent":"자신의 User-Agent 주소"}

res=requests.get(url, headers=headers)
res.raise_for_status()

with open("mycopyhtml.html", "w", encodig='utf8') as f:
    f.write(res.text)
```

문제없이 접근 거부되었던 사이트에 접근이 허용되어 올바르게 웹 정보를 얻어낸 걸 확인할 수 있다.

# 웹 스크래퍼 실전
웹 스크래핑을 하기 위해 ``pip install beautifulsoup4`` 와 ``pip install lxml``을 터미널에 입력해서 beautifulsoup4와 lxml모듈을 설치해준다. beautifulsoup4는 웹스크래핑을 위한 패키지, lxml은 구문을 분석하기 위한 파서<sup>parser</sup> 이다.

# 선택자
CSS에서 선택자란 **선택을 해주는 요소**를 뜻한다. 선택자의 종류도 여러가지가 있는데

- 전체 선택자
- 태그 선택자
태그의 이름으로 선택함 \<h1>제목\</h1>의 선택자 : h1
- 클래스 선택자
\<div class="info_group"> 인포메이션 \</div>의 선택자 : .info_group
- ID 선택자
\<div id="articlebody"> 본문 내용 \</div>의 선택자 : #articlebody
- 복합 선택자
- 속성 선택자
- 가상 선택자

등 여러가지 선택자가 존재한다

# 네이버 증권 사이트 스크래핑 하기

네이버 증권 사이트의 웹 정보를 스크래핑해서 엑셀 파일로 저장하고 출력하는 코드를 작성해보겠다.

```python
from bs4 import BeautifulSoup
import requests
import time
import openpyxl

# # 알파벳 저장 리스트
# alphabet = []
# for i in range(97, 123):
#     alphabet += chr(i)

# 엑셀 파일
xl = openpyxl.Workbook()

xlws = xl.create_sheet("주식 크롤링 데이터")

xlws["A1"] = "종목"
xlws["B1"] = "현재가"
xlws["C1"] = "평균 매입가"
xlws["D1"] = "잔고 수량"
xlws["E1"] = "평가 금액"
xlws["F1"] = "평가 손익"
xlws["G1"] = "수익률"

# 가져올 종목 코드 리스트
codes = ["005930", "001570", "000270"]  # 삼성전자  # 금양  # 기아
codescount = len(codes)
for idx, code in enumerate(codes):
    url = f"https://finance.naver.com/item/sise.naver?code={code}"
    res = requests.get(url)
    res.raise_for_status()  # requests 오류 발생 확인

    soup = BeautifulSoup(res.content, "lxml", from_encoding="utf8")

    nowPrice = soup.select_one("#_nowVal").text.replace(",", "")
    nowName = soup.select_one(".wrap_company>h2>a").text

    xlws["A{}".format(idx + 2)] = nowPrice
    xlws["B{}".format(idx + 2)] = nowName

xl.save("scraper.xlsx")

```