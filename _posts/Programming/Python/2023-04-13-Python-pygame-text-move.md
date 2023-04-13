---
title:  "[Python] 파이게임(pygame) 튜토리얼 - 텍스트 움직이기, 시간을 고정하는 방법"
excerpt: "pygame의 이전 글은 고정된 사진같았다(게임같지 않았다). 텍스트를 마치 화면보호기처럼 움직여보고 화면이 업데이트 될 때 시간을 고정하는 방법(FPS)에 대해 알아보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, 화면보호기, 텍스트 움직이기, move_text]

toc: true
toc_sticky: true

date: 2023-04-13
last_modified_at: 2023-04-13
---

# 이전의 소스코드

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

이전의 프로그램을 실행해보면 그냥 배경과 텍스트가 있는 화면이 종료하기 전까지 가만히 계속 있는 그런 '그림'같은 프로그램이었다. '게임'이랑은 거리가 멀다. 게임이라하면 움직임이 있고 사용자와의 상호작용으로 플레이하는 재미가 있는 장르인데 세상에 텍스트만 쳐다보고 있는 게임은 없을것이다. 화면에서 애니메이션을 구현해보자.
<br><br><br>

# 텍스트 움직이기

## 구상하기
예제를 보기 전에 생각해보자. 화면 안의 고정된 텍스트를 움직이려면 어떻게 해야할까? 위의 코드를 보면
``` python
Screen = pygame.display.set_mode((Screen_width, Screen_height))
...
txtArea.center = (320, 240)
```
이 두 줄을 찾을 수 있다.

첫 번째 줄의 set_mode는 플레이할 화면의 크기를 지정해주는 코드이고 두 번째 줄의 txtArea.center = (320, 240)은 txtArea의 위치를 지정해주는 코드이다. 그래서 텍스트는 화면의 크기(640, 480)의 중앙 (320, 240)에 떠있음을 볼 수 있다.

그 말은 텍스트나, 혹은 그림이나 프로그램안에서 고유한 $x$ 값과 $y$값을 가진다는 소리다!

학창시절에 수학시간에 그래프가 $x, y$값을 바꿔주면 축에서 움직여져서 그려졌던 그래프의 그림과 실제 애니메이션은 그림을 겹겹이 그려 부드러운 움직임을 표현한다는 걸 더해서 생각해보면 **텍스트나 그림의 $x, y$값을 조금씩 변경해주고 그 $x, y$값을 계속해서 표현해주면,  움직임을 구현할 수 있을 것**이다. 계속해서 표현해주는 역할은 ``pygame.display.update()``이 해주기 때문에 우리들은 $x, y$값을 조금씩 변경하면 **아마도** 텍스트가 서서히 움직일 것이다.

## 실현하기
그런데 $x, y$값이 계속 더해주거나 빼준다면 어느새 화면의 틀 안에서 벗어나 보이지 않는 곳으로 떠나버릴것이다. 그러므로 우리들은 이 순서로 텍스트박스가 먼 우주로 떠나지 않게 붙잡아줄 것이다.
<br><br>

1. 화면의 텍스트의 $x, y$값이 서서히 증가하거나 감소함<br><br><br>
2. 화면에서 사라지지 않도록 화면에 고정시켜줘야함<br><br><br>
3. 화면에 닿으면 증가하는 값이 반전됨 (+에서 -로, -에서 +로)<br><br><br>


$x, y$값을 증감시켜주기 위해 우리들은 25번째 줄의 ``txtArea.center = (320, 240)`` 에서 $x, y$를 설정해주는 부분의 변수를 만들어주고 ``while True:``문에 증감시켜주는 코드를 짜줄 것이다.
```python
txtArea = txt.get_rect() #rect는 사각형이란 뜻으로 txt의 위치(x, y)를 구해줌
txtArea_x = Screen_width / 2 #txtArea의 시작 X값
txtArea_y = Screen_height / 2 #txtArea의 시작 Y값
txtArea.center = (txtArea_x, txtArea_y) #640의 절반과 480의 절반이니 중간에 위치할 것
```
txtArea의 x, y값을 지정해주는 변수를 만들고 그 변수의 값은 화면의 크기의 절반, 즉 **중앙**에 위치하도록 절반으로 나누어주었다.
그리고 txtArea의 위치를 (txtArea_x, txtArea_y)로 수정했다.

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
txtArea_x = Screen_width / 2 #txtArea의 시작 X값
txtArea_y = Screen_height / 2 #txtArea의 시작 Y값
txtArea.center = (txtArea_x, txtArea_y) #640의 절반과 480의 절반이니 중간에 위치할 것

move_x = 0 #이동시킬 x값
move_y = 0 #이동시킬 y값
moveRight = 1 #시작할 때 X값을 오른쪽으로 이동시킨다. 0은 왼쪽
moveUp = 1 #시작할 때 Y값을 위로 이동시킨다. 0은 왼쪽

while True: #게임이 실시간으로 반응해야하니 While True:
    if moveRight == 1:
        move_x += 1
        if move_x >= txtArea_x-75:
            moveRight = 0
    elif moveRight == 0:
        move_x -= 1
        if move_x <= -txtArea_x+75:
            moveRight = 1
    if moveUp == 1:
        move_y += 1
        if move_y >= txtArea_y-15:
            moveUp = 0
    elif moveUp == 0:
        move_y -= 1
        if move_y <= -txtArea_y+15:
            moveUp = 1

    txtArea.center = (txtArea_x + move_x, txtArea_y + move_y)

    for event in pygame.event.get(): 
        if event.type == QUIT: #게임을 종료하면
            pygame.quit()
            sys.exit()
    
    Screen.fill(white) #뒷 배경을 하얀색으로
    Screen.blit(txt, txtArea) #텍스트를 표시해줌

    pygame.display.update() #게임을 꾸준히 업데이트해줌(실시간)
```
25~32줄은 txtArea가 중앙에 오도록 변수를 설정해줬고 (txtArea_x, txtArea_y)
이동시킬 x, y값을 할당할 변수(move_x, move_y)와 테두리에 부딪혔을 때 경로를 바꿔줄 변수(moveRight, moveUp)들을 추가해주었다

반복문에서는
```python
while True: #게임이 실시간으로 반응해야하니 While True:
    if moveRight == 1:
        move_x += 1
        if move_x >= txtArea_x-75:
            moveRight = 0
    elif moveRight == 0:
        move_x -= 1
        if move_x <= -txtArea_x+75:
            moveRight = 1
    if moveUp == 1:
        move_y += 1
        if move_y >= txtArea_y-15:
            moveUp = 0
    elif moveUp == 0:
        move_y -= 1
        if move_y <= -txtArea_y+15:
            moveUp = 1

    txtArea.center = (txtArea_x + move_x, txtArea_y + move_y)
```
x, y값을 증감시키고 테두리에 부딪혔을 때 x, y값이 반전되는 코드를 추가했다.
txtArea_x, txtArea_y 옆의 +75 +15등과 같은 숫자는 텍스트박스의 크기(75x15)를 포함해서 계산해준 값이다.

*처음에는 Screen_width,height 와 0으로 값을 조절해줬는데 처음 위치한 중앙의 오른쪽 아래에서만 텍스트박스가 움직여서 +txtArea와 -txtArea를 해주니 해결되었다(추측 : 아마도 center 함수는 스크린 안에서의 위치를 지정해주는게 아니라 직접 rect의 위치를 지정해주는 함수같다. 그니까 스크린 따로, txtArea 따로의... 그래서 640x480의 스크린에서 +320 -320, +240 -240으로 해줘야하는 것 같다).*

실행해보니 코드는 문제없이 구동한다. 문제는 +1과 -1이 '속도'를 제한해주지 않아서 매우 빠르게 커지고 작아져 텍스트박스의 텍스트가 잘 보이지도 않는다.

# FPS, 화면이 업데이트 될 때 시간을 고정하는 방법
이 코드의 ``while:True:``문은 우리들이 바란다고 컴퓨터 시간의 1초에 맞춰 한 번씩 실행되는 방식이 아니다. 우리들은 직접 **고정 속도**라는 개념을 추가해줘야한다. 그러면 이 '고정 속도'는 어떻게 컴퓨터에서 설정해줄 수 있을까?

FPS를 설정해주면 되는데, FPS는 **Frame Per Second**라는 뜻으로 **1초에 화면이 얼마나 자주 바뀌는지**를 의미한다. 무한루프 ``While True:``문에서 화면을 업데이트해주는 함수 ``pygame.display.update()``한 번 들어가있으므로 이 프로그램에서 **FPS는 1초에 Always문이 몇 번 실행되는가?로 정의할 수 있을 것이다.** 즉, 딜레이 기능을 한다.

1. 시간을 고정해준다
```python
변수 = pygame.time.Clock()
```
2. 시간을 정해준다
```python
변수.tick(FPS)
```

라는 단순한 순서로 FPS를 설정해줄 것이다.

# 완성된 코드
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
txtArea_x = Screen_width / 2 #txtArea의 시작 X값
txtArea_y = Screen_height / 2 #txtArea의 시작 Y값
txtArea.center = (txtArea_x, txtArea_y) #640의 절반과 480의 절반이니 중간에 위치할 것

move_x = 0 #이동시킬 x값
move_y = 0 #이동시킬 y값
moveRight = 1 #시작할 때 X값을 오른쪽으로 이동시킨다. 0은 왼쪽
moveUp = 1 #시작할 때 Y값을 위로 이동시킨다. 0은 왼쪽

Clock = pygame.time.Clock() #게임이 시작되기 전 속도를 고정시킴

while True: #게임이 실시간으로 반응해야하니 While True:
    if moveRight == 1:
        move_x += 1
        if move_x >= txtArea_x-75:
            moveRight = 0
    elif moveRight == 0:
        move_x -= 1
        if move_x <= -txtArea_x+75:
            moveRight = 1
    if moveUp == 1:
        move_y += 1
        if move_y >= txtArea_y-15:
            moveUp = 0
    elif moveUp == 0:
        move_y -= 1
        if move_y <= -txtArea_y+15:
            moveUp = 1

    txtArea.center = (txtArea_x + move_x, txtArea_y + move_y)

    for event in pygame.event.get(): 
        if event.type == QUIT: #게임을 종료하면
            pygame.quit()
            sys.exit()
    
    Screen.fill(white) #뒷 배경을 하얀색으로
    Screen.blit(txt, txtArea) #텍스트를 표시해줌

    pygame.display.update() #게임을 꾸준히 업데이트해줌(실시간)
    Clock.tick(60) #60fps 로 실행하게 설정, 반드시 update 함수의 뒤에 와야한다.
```

``Clock = pygame.time.Clock()``으로 시간을 고정해주는 변수를 만들어주고, ``update()``의 아랫줄에 ``Clock.tick(60)``으로 60프레임으로 구동하는 프로그램을 만들었다. 실행해보면 60fps에 맞춰 부드럽게 움직이는 텍스트박스를 볼 수 있다.

***※ : tick함수는 화면이 몇 번 업데이트되는지를 계산하는 함수이기 때문에 반드시 update함수의 뒤에 와주어야 한다!***
