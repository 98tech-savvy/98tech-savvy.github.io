---
title:  "[Python] 파이게임(pygame) 튜토리얼 - 출력 함수"
excerpt: "pygame의 출력 함수에 대해 알아보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, tutorial, 파이게임]

toc: true
toc_sticky: true

date: 2023-04-12
last_modified_at: 2023-04-12
---

# 게임을 만들고 싶다
프로그래밍을 배우게 된 계기는 여러 사람들마다 다르겠지만, 아마도 현재 대부분의 사람들은 영화에서 나오는 해커의 모습, 빌 게이츠나 스티븐 잡스의 성공한 모습, 혹은 게임을 즐기며 프로그램을 사용하며 '아! 나는 이런 아이디어가 있는데 구현할 수가 없네' 라는 생각을 하는 사람들이 있을 것이다.

나는 이 위에 모든 모습(해커, 개발로 성공한, 아이디어)을 이루고싶었고 파이썬을 배우며 언리얼엔진 만큼은 아니겠지만 pygame 이라는 모듈로 게임을 구현해낼 수 있다길래 Python에 대한 기초를 배우면서 pygame 모듈을 활용한 코딩을 기대했다.

이전에 C를 취미로 공부했을때는 아스키아트(문자를 사용해 그림을 표현하는 방식)로 점을 찍으며 아스키아트로 만든 피라미드를 만들곤했고 C 콘솔 환경에서 게임을 만드는 걸 생각해보았을 때, 위에서 설명했듯이 아스키아트로 문자를 찍고 내 갤러그에서 총을 쏘면 총알 대신 --- 가 나가고 부딪히면 \\*/ 같은 이펙트를 뿜어내는 구식, CUI게임을 만들 수 있을 것이다. 언리얼엔진같은 게임 엔진을 활용하면 3D의 멋진 그래픽과 물리엔진을 사용할 수 있겠지만 초심자의 진입 장벽이 높다.

이 '콘솔 환경과 게임 엔진'의 딜레마를 해결해줄 수 있는게 pygame이라고 하는데, pygame은 **콘솔 환경에서의 장점(소스코드와 동치관계, 접근성이 좋음)과 게임 엔진의 장점(키보드, 마우스등의 입력 관련 함수, 도형 그리기, 색 칠하기, 디스플레이 설정 등의 출력 관련 함수)**를 제공하기 때문에 CUI가 아닌 GUI에서 실행되고 python에 기반하기 때문에 절차적이 아닌 이벤트적으로 실행된다는 장점 또한 있을 것이다. 

이 튜토리얼은 [Youngwook Kim님의 pygame.org 튜토리얼](https://www.pygame.org/docs/tut/ko/%EB%B9%A8%EA%B0%84%EB%B8%94%EB%A1%9D%20%EA%B2%80%EC%9D%80%EB%B8%94%EB%A1%9D/%EA%B0%9C%EC%9A%94.html)을 참고했습니다.

# 출력 함수
pygame은 GUI(정확히는 2D GUI)를 기반으로 하기 때문에 CUI환경에서의 print, input은 사용하지 않는다. 그렇다면 어떻게 텍스트를 입,출력 받을 수 있을까?

CUI 에서는 print("Hello World!")로 Hello World!를 표현할 수 있다. 하지만 GUI환경에서는 텍스트는 최소 5개의 구성 성분(내용, 폰트, 크기, 색상, 좌표)를 필요로 하기 때문에 이 Hello World!를 표시하기위해서는 한 줄보다는 꽤 많은 줄의 코드를 짜야한다.

*pygame으로 Hello World!를 구현한 모습*
![image](https://user-images.githubusercontent.com/128434645/231084025-972d1eed-331a-49cd-96b1-4b2ca3c9edc1.png)
<br><br><br>

*Hello World!를 위의 사진처럼 표현하기 위한 소스코드*
```python
import pygame, sys
from pygame.locals import *

###색깔 지정 변수###
white = (255,255,255)
red = (255, 0, 0)
green = (0, 255, 0)

#pygame 초기화, 반드시 해주어야 하는 것
pygame.init()

#pygame 디스플레이 설정
Screen_width = 640 #가로 크기, 게임의 해상도 1920x1080같은 크기의 변수
Screen_height = 480 #세로 크기
Screen = pygame.display.set_mode((Screen_width, Screen_height))


pygame.display.set_caption("Hello World Caption") #프로그램 창의 제목을 설정
txtFont = pygame.font.Font(None, 32) #글꼴과 글자크기

#.render("Caption", 안티앨리어싱, 색상, 백그라운드 색상)
txt = txtFont.render("Hello World!", True, red, green) #Hello World!가 여기에 들어간다.

txtArea = txt.get_rect() #rect는 사각형이란 뜻으로 txt의 위치(x, y)를 구해줌
txtArea.center = (320, 240) #640의 절반과 480의 절반이니 중간에 위치할 것

while True: #게임이 실시간으로 반응해야하니 While True:
    Screen.fill(white) #뒷 배경을 하얀색으로
    Screen.blit(txt, txtArea) #텍스트를 표시해줌

    for event in pygame.event.get(): 
        if event.type == QUIT: #게임을 종료하면
            pygame.quit()
            sys.exit()
    
    pygame.display.update() #게임을 꾸준히 업데이트해줌(실시간)
```

# 소스코드 분석
그럼 소스코드를 하나 하나 분석해보도록하겠다.

## Header
``` python
import pygame, sys
from pygame.locals import*
```
이 구문은 당연하게도 pygame을 사용하려면 반드시 넣어줘야하는 구문이다. 이 프로젝트가 pygame모듈을 사용한 프로젝트이며, 사용자가 프로그램을 종료하고 싶을 때 종료해야 함으로 (34번째 라인에 sys.exit()을 사용하는걸 볼 수 있음)

``from pygame.locals import *`` 구문은 32줄의 QUIT같은 유용한 상수들을 선언없이 사용해주기 위해(편리하기위해) 선언해주는 **반필수적 요소**이다.

## Initial
``` python
###색깔 지정 변수###
white = (255,255,255)
red = (255, 0, 0)
green = (0, 255, 0)

#pygame 초기화, 반드시 해주어야 하는 것
pygame.init()

#pygame 디스플레이 설정
Screen_width = 640 #가로 크기, 게임의 해상도 1920x1080같은 크기의 변수
Screen_height = 480 #세로 크기
Screen = pygame.display.set_mode((Screen_width, Screen_height))


pygame.display.set_caption("Hello World Caption") #프로그램 창의 제목을 설정
txtFont = pygame.font.Font(None, 32) #글꼴과 글자크기

#.render("Caption", 안티앨리어싱, 색상, 백그라운드 색상)
txt = txtFont.render("Hello World!", True, red, green) #Hello World!가 여기에 들어간다.

txtArea = txt.get_rect() #rect는 사각형이란 뜻으로 txt의 위치(x, y)를 구해줌
txtArea.center = (320, 240) #640의 절반과 480의 절반이니 중간에 위치할 것
```
Initial문 이라고도 부르고, while True: 이전의 문장들에 대해 말한다. 이 곳에서는 전역 변수들을 초기화하거나 코드의 가독성을 높이기 위해 초기화되는 변수들이 존재한다. 특히
``pygame.init()``은 pygame을 사용하려면 반드시 사용해야하는 초기화 구문이므로 주의해주도록 하자.

## Always ~ Event
``` python
while True: #게임이 실시간으로 반응해야하니 While True:
    Screen.fill(white) #뒷 배경을 하얀색으로
    Screen.blit(txt, txtArea) #텍스트를 표시해줌

    for event in pygame.event.get(): 
        if event.type == QUIT: #게임을 종료하면
            pygame.quit()
            sys.exit()
    
    pygame.display.update() #게임을 꾸준히 업데이트해줌(실시간)
```
Always문(무한 반복문)부터 Event문(이벤트를 체크하는 반복문)이다.

Always문에서는 전역 변수를 계속 업데이트해주고 몇몇 함수들을 계속해서 호출해준다.

Event문에서는 특정 이벤트가 발생하면 이에 대한 처리가 이루어지는데, 이 코드의 경우에는 '게임을 종료하는 이벤트'가 있을 시 프로그램을 종료하는 이벤트가 짜여져있다.

``pygame.event.get()`` 함수는 Always문에서 발생한 이벤트들의 배열을 반환하고 이 이벤트들은 자동으로 **발생 시간순으로 정렬**된다. 그러므로 **for-in 문**을 써주면 Always문에서 발생하는 모든 이벤트들에 대해 순차적으로 처리할 수 있는 것이다.


마지막으로 ``pygame.display.update()`` 라는 함수는 모든 변수와 함수의 처리가 끝난 이후에 처리의 결과물들을 스크린에 출력하는 역할을 한다.