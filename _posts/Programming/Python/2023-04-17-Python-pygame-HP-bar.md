---
title:  "[Python] 파이게임(pygame) 튜토리얼 - HP바(HP Bar) 만들기"
excerpt: "pygame의 draw를 이용해 HP바를 만들어보자."

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, HP바, HPbar, pygame.draw]

toc: true
toc_sticky: true

date: 2023-04-17
last_modified_at: 2023-04-17
---

# 이전의 포스팅
이전의 포스팅에서 우리들은 pygame의 입출력에 대해 공부했고 텍스트박스를 화면보호기처럼 움직이게 만들기도하고 방향키를 이용해 스스로 제어도 해보았다. 그러나 아직도 게임이라하기에는 모호한 면이 있다. 게임이라하면 목숨(HP)이 있어야 하지 않겠는가?

# HPbar 표시하기
일단 HP BAR를 그리기전에, 텍스트로 HP BAR를 표현해보도록 하겠다. 동작 방식은 방향키의 UP과 DOWN을 사용하면 현재 체력(nowHP)가 깎이는 방식으로 구현하겠다.

``` python
##############################
import pygame, sys
from pygame.locals import *

pygame.init()
##############################
#COLOR
white = (255, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)
##############################
pygame.display.set_caption("HP BAR")
ScreenWidth = 640
ScreenHeight = 480
Screen = pygame.display.set_mode((ScreenWidth, ScreenHeight))

maxHP = 10
txtHPbar_FONT = pygame.font.Font(None, 32)
txtHPbar = txtHPbar_FONT.render("{} / {}".format(maxHP, maxHP), True, red, white)
txtHPbar_Area = txtHPbar.get_rect()
txtHPbar_Area.center = (ScreenWidth/2, ScreenHeight/2)
nowHP = 5

while True:
    for event in pygame.event.get():
        if event.type == QUIT or nowHP == 0:
            pygame.quit()
            sys.exit()
        if event.type == KEYDOWN:
            if event.key == K_UP:
                if nowHP != maxHP:   
                    nowHP+=1
            elif event.key == K_DOWN:
                if nowHP > 0:
                    nowHP-=1


    txtHPbar = txtHPbar_FONT.render("{} / {}".format(nowHP, maxHP), True, red, white)
    
    Screen.fill(white)
    Screen.blit(txtHPbar, txtHPbar_Area)
    pygame.display.update() 
```

K_UP을 누르면 nowHP가 올라가고, K_DOWN을 누르면 nowHP가 줄어든다. maxHP만큼 올라가면 더 이상 증가하지 않고, nowHP가 0이 되면 게임을 종료한다.

# 도형을 시각화하는 방법
하지만 아직도 '텍스트'라는 점은 변함이 없다. TRPG를 하는게 아니라면, 우리들은 이미지를 상상하는게 아니라 그려주어야할 것이다.

물약 이미지로 체력을 대신하는 방법도 있겠지만, 아주 고전적인 방법으로 체력 바를 표현해보도록 하겠다.

pygame의 draw 함수를 이용하는 방식인데 이미지를 불러오는 것보다는 방식이 귀찮다.
``` python
##############################
import pygame, sys
from pygame.locals import *

pygame.init()
##############################

#COLOR
white = (255, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)
##############################

pygame.display.set_caption("HP BAR")
ScreenWidth = 640
ScreenHeight = 480
Screen = pygame.display.set_mode((ScreenWidth, ScreenHeight))

maxHP = 10
txtHPbar_FONT = pygame.font.Font(None, 32)
txtHPbar = txtHPbar_FONT.render("{} / {}".format(maxHP, maxHP), True, red, white)
txtHPbar_Area = txtHPbar.get_rect()
txtHPbar_Area.center = (ScreenWidth/2, ScreenHeight/2)

def main():
    nowHP = 5

    while True:
        for event in pygame.event.get():
            if event.type == QUIT or nowHP == 0:
                pygame.quit()
                sys.exit()
            if event.type == KEYDOWN:
                if event.key == K_UP:
                    if nowHP != maxHP:   
                        nowHP+=1
                elif event.key == K_DOWN:
                    if nowHP > 0:
                        nowHP-=1


        txtHPbar = txtHPbar_FONT.render("{} / {}".format(nowHP, maxHP), True, red, white)
        
        Screen.fill(white)
        Screen.blit(txtHPbar, txtHPbar_Area)
        drawHP(nowHP)

        pygame.display.update() 

def drawHP(HP):
    r = int((ScreenHeight - 40) / maxHP) # Screenheight-40의 값을 maxHP로 나누어준다. 위 아래 20씩 여분공간을 두고 maxHP의 개수를 표현하기 위해 나누어줌

    pygame.draw.rect(Screen, black, (20, 20, 20, 20 + ((maxHP - 0.5) * r)))
    #3번째 인자는 (X, Y, 가로, 세로)이다. 20, 20의 위치부터 검정으로 20, 20+((maxHP-0.5)*r)을 한다는 뜻 

    for i in range(maxHP):
        if nowHP >= (maxHP - i):
            pygame.draw.rect(Screen, red, (20, 20 + (i*r), 20, r))
        pygame.draw.rect(Screen, white, (20, 20 + (i * r), 20, r), 1)
    
    return

if __name__ == '__main__':
    main()
```

하나하나씩 살펴보자.
```python
def main():
    ~
def drawHP(HP):
```
모든 코드를 main에 두면 코드가 난잡하고 어지러워지기때문에, main과 drawHP라는 함수를 나누었다. main은 코드의 전반적인 진행을 하고 drawHP는 이번에 HPbar를 그림으로 그리는 기능을 구현한다.
<br>

```python
if __name__ == '__main__':
    main()
```
기능을 분할시켜주었으니 어디가 메인인가?라는 것을 컴퓨터에 전달해주어야 한다. 이 프로그램의 메인일 때 main()함수를 호출한다. 라는 의미를 담고있다
<br>

```python
    r = int((ScreenHeight - 40) / maxHP) # Screenheight-40의 값을 maxHP로 나누어준다. 위 아래 20씩 여분공간을 두고 maxHP의 개수를 표현하기 위해 나누어줌

    pygame.draw.rect(Screen, black, (20, 20, 20, 20 + ((maxHP - 0.5) * r)))
    #3번째 인자는 (X, Y, 가로, 세로)이다. 20, 20의 위치부터 검정으로 20, 20+((maxHP-0.5)*r)을 한다는 뜻 
```
r 은 nowHP를 스크린상에 표현하기 위한 개수를 만들기 위해 선언해주었다. -40은 위 아래 20을 뜻한다.

``pygame.draw.rect(Screen, black, (20, 20, 20, 20 + ((maxHP - 0.5) * r)))``
pygame.draw.rect 함수를 사용하면 도형을 표현할 수 있다.
``pygame.draw.rect(표시할 화면, 색깔, (X, Y, 가로, 세로), 두께)``
이며 '세로'에 해당하는 부분에 maxHP를 표시할 수 있게 길게 표현해주었다.<br>

```python
    for i in range(maxHP):
        if nowHP >= (maxHP - i):
            pygame.draw.rect(Screen, red, (20, 20 + (i*r), 20, r))
        pygame.draw.rect(Screen, white, (20, 20 + (i * r), 20, r), 1)
    
    return
```
1부터 전역변수 maxHP만큼 반복하고, nowHP가 'maxHP-i'값 보다 크면 실행한다. 즉
```
nowHP=5 maxHP=10

nowHP=5 maxHP-1(9)
nowHP=5 maxHP-2(8)
nowHP=5 maxHP-3(7)
nowHP=5 maxHP-4(6)
nowHP=5 maxHP-5(5) # 여기서부터 실행함
nowHP=5 maxHP-6(4)
...
```
그리고 draw.rect 함수를 통해 y값에 20 + (i * r)을 해주어 표시할 HP의 위치를 해주고 r(아까 선언한 nowHP 한 칸을 표현하기위한))을 세로의 값에 두어 빨강색 HP바를 표시해주었다.

그리고 아래의 draw.rect(~화이트~)문으로 두께를 1칸 늘려 하얀색 테두리를 표시해준것이다. 두께에 해당하는 1<<값을 키워보면 HPbar 전체가 얇아지는걸 볼 수 있다.

전체적으로 drawHP 함수를 보면

1. HP의 한 칸에 해당하는 r 값을 구해준다.
2. 큰 검은색 직사각형으로 maxHP를 표현해준다.
3. 작은 빨간색 직사각형들로 nowHP를 표현한다.

의 코드를 작성했음을 알 수 있다.

# 정리
아직까지는 게임이라고는 볼 수 없지만 하나 하나 기능이 늘어가다보면 게임을 만들 수 있을 것이다.