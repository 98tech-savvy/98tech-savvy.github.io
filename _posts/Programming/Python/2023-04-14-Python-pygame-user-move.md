---
title:  "파이게임(pygame) 튜토리얼 - 키 이벤트를 활용해 스스로 텍스트를 제어해보자"
excerpt: "pygame의 키 이벤트를 활용해 스스로 텍스트박스를 제어해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, 화면보호기, 방향키로 움직이기, 입력]

toc: true
toc_sticky: true

date: 2023-04-14
last_modified_at: 2023-04-14
---

# 프로그램과 게임
우리들은 이전 포스팅에서 텍스트박스를 화면 내에서 만들어내고, 그 텍스트박스를 마치 화면보호기처럼 움직여보는 코드를 짜보았다. 그런데 우리들이 흔히 아는 게임들은 키보드와 마우스 같은 입력장치를 통해 진행하는데, 저 위의 코드들은 단순히 관측만 할 뿐이라 게임이라하기는 모호하다. 저건 게임이라기보다는 프로그램이다. **프로그램은 0개 이상의 입력과 1개 이상의 출력으로 이루어진 것들을 말한다.** 그러나 모든 **게임은 입력이 필요**하고 우리들은 그걸 '게임을 플레이한다'라고 표현한다.

# 텍스트박스를 움직여보자

## 구상하기
텍스트박스를 움직이려면 어떻게 해야할까? 이전 포스팅과 똑같이 텍스트박스의 x, y값을 조정해주면 끝나는 일이다. 그런데 단순히 **x, y값을 증감**하는게 아니라 **KEY EVENT를 통한 x, y값의 증감**이 되어야한다.

제일 먼저 작성했었던 이 구문을 보자.
```python
for event in pygame.event.get():
    if event.type == QUIT:
```
- for event in pygame.event.get():
파이게임내에서 이벤트가 발생할 경우 event안에 넣어 순차적으로 처리하겠다는 의미이다.

- if event.type == QUIT:
이벤트의 타입이 QUIT(종료)일 경우 해당 이벤트를 발생하겠다는 의미이고, 여기서 QUIT은 HEADER라인의
``from pygame.locals import *`` 문으로 원래의 'pygame.QUIT'을 간략화 한것이다. 

그러면 이벤트가 일어나는 곳은 저 for문의 안에, 이벤트의 타입은 event.type으로 넣어주면 된다는 사실을 알았다.
```python
for event in pygame.event.get():
    if event.type == KEYDOWN:
        if event.key == K_RIGHT:
            ~
```
for문 안에서, 우리들은 KEYDOWN이라는 이벤트가 일어날시 라는 구문을 추가했다. 여기서 KEYDOWN은 '키를 눌렀을 시'를 말하고, event.key 라는 이벤트는 만약 KEYDOWN의 이벤트의 key가 ~라면 이라는 뜻으로 볼 수 있다. K_RIGHT는 키보드의 오른쪽 방향키를 뜻한다.

그럼 이제 이 구문에 RIGHT일때는 오른쪽, LEFT는 왼쪽, UP은 위, DOWN은 아래의 코드를 추가해서 방향키로 textbox를 움직여 볼 것이다.
```python
        elif event.type == KEYDOWN:
            if event.key == K_UP:
                txtMove_Y -= 1
            elif event.key == K_DOWN:
                txtMove_Y += 1
            elif event.key == K_RIGHT:
                txtMove_X += 1
            elif event.key == K_LEFT:
                txtMove_X -= 1
        elif event.type == KEYUP:
            if event.key == K_UP:
                txtMove_Y = 0
            elif event.key == K_DOWN:
                txtMove_Y = 0
            elif event.key == K_RIGHT:
                txtMove_X = 0
            elif event.key == K_LEFT:
                txtMove_X = 0
```
KEYDOWN은 눌렀을 때, KEYUP은 누른 키를 뗐을 때라는 타입이다. txtMove_X와 txtMove_Y의 값을 키에 맞게 증감시켜주고 뗐을 때 증가하는 변수를 0으로 초기화해준다.

그리고 while True:문에 아래의 코드를 넣어 txtBox_Area의 center값을 증감시켜준다.
``` python
while True:
    txtBox_Area.centerx += txtMove_X
    txtBox_Area.centery += txtMove_Y
```

그리고 이렇게하면 방향키를 누르기만해도 그 방향으로 텍스트박스가 사라져버린다. 이 텍스트박스를 화면안에 가둬주기 위해 아래의 코드를 넣어주었다.
```python
    if txtBox_Area.centerx >= Screen_width:
        txtBox_Area.centerx = Screen_width
    elif txtBox_Area.centerx <= 0:
        txtBox_Area.centerx = 0
    elif txtBox_Area.centery >= Screen_height:
        txtBox_Area.centery = Screen_height
    elif txtBox_Area.centery <= 0:
        txtBox_Area.centery = 0
```
~~*이 코드에는 개선점이 있는데 txtBox의 크기를 계산해서 if문에 추가해줘야한다는것이다.*~~

# 완성된 코드
```python
#HEADER
import pygame, sys
from pygame.locals import *

#INITIAL
pygame.init() #파이게임 초기화

pygame.display.set_caption("Hello World MOVE")
Screen_width = 640
Screen_height = 480
Screen = pygame.display.set_mode((Screen_width, Screen_height))

yellow = (255, 255, 0)
black = (0, 0, 0)
white = (255, 255, 255)

txtFont = pygame.font.Font(None, 32)
txtBox = txtFont.render("Hello World", True, yellow, black)
txtBox_Area = txtBox.get_rect()
txtBox_Area.center = (Screen_width/2, Screen_height/2)
txtMove_X = 0
txtMove_Y = 0

#ALWAYS ~ EVENT
while True:        
    Screen.fill(white)
    Screen.blit(txtBox, txtBox_Area)

    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == KEYDOWN:
            if event.key == K_UP:
                txtMove_Y -= 1
            elif event.key == K_DOWN:
                txtMove_Y += 1
            elif event.key == K_RIGHT:
                txtMove_X += 1
            elif event.key == K_LEFT:
                txtMove_X -= 1
        elif event.type == KEYUP:
            if event.key == K_UP:
                txtMove_Y = 0
            elif event.key == K_DOWN:
                txtMove_Y = 0
            elif event.key == K_RIGHT:
                txtMove_X = 0
            elif event.key == K_LEFT:
                txtMove_X = 0

    if txtBox_Area.centerx >= Screen_width:
        txtBox_Area.centerx = Screen_width
    elif txtBox_Area.centerx <= 0:
        txtBox_Area.centerx = 0
    elif txtBox_Area.centery >= Screen_height:
        txtBox_Area.centery = Screen_height
    elif txtBox_Area.centery <= 0:
        txtBox_Area.centery = 0

    # txtBox_Area.center = (Screen_width/2 + txtMove_X, Screen_height/2 + txtMove_Y)
    txtBox_Area.centerx += txtMove_X
    txtBox_Area.centery += txtMove_Y

    pygame.display.update()
```