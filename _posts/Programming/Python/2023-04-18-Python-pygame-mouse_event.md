---
title:  "[Python] 파이게임(pygame) 튜토리얼 - 버튼 만들기"
excerpt: "pygame을 활용해서 특정한 위치에서의 마우스 이벤트를 처리하는 함수를 만들어보자."

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, 버튼, 버튼 구현]

toc: true
toc_sticky: true

date: 2023-04-18
last_modified_at: 2023-04-18
---

# 또 다른 입력장치, 마우스
키보드로 텍스트도 움직여보고, HP바도 조절해보았지만 보통의 컴퓨터의 입력장치에는 키보드를 제외하고도 '마우스'라는 친구가 있다. 이 마우스라는 친구를 사용해서 HP바를 조절하는 버튼을 만들어보자.

# 코드 추가하기
우리들은 이전의 포스팅에서 drawHP와 main함수를 만들었었다. 우리들은 새로운 버튼을 그려줘야하니 새로운 버튼을 그리는 함수 drawbuttons를 구현해보자.

1. 우리들은 새로운 버튼을 도형으로 그릴 것이고
2. 그 도형의 위치에 해당하는 곳에 마우스를 클릭했을 때
3. HP바가 증/감하는 코드를 만들것이다.

## 새로운 버튼 그리기

```python
#일단 도형을 그리자
def drawbuttons():
  r = 45 #버튼의 반지름
  r_margin = 10 #버튼끼리의 간격

  colors = [red, black] #버튼의 색깔을 달리하기 위한 리스트(for문에 활용예정)

  num = 2 #버튼의 개수
  margin = int((ScreenWidth - ((num*r)+((num-1)*r_margin))) / 2)#int로 해주는 이유는 화면을 표시하는 좌표가 정수형이라서.

  for i in range(0, num):
    LEFT = margin + (i*r) + (i*r_margin)
    UP = ScreenHeight - 10
    pygame.draw.rect(Screen, colors[i], (LEFT, UP, r, r))
    pygame.draw.rect(Screen, white, (LEFT+2, UP+2, r-4, r-4))

```

``margin = int((ScreenWidth - ((num*r)+((num-1)*r_margin))) / 2)``

ScreenWidth(화면의 가로길이)에서 ((num \* r)+((num - 1) \* r_margin))을 빼주고 2로 나누어준다.
여기서 (num \* r)+((num - 1) \* r_margin) 은 버튼의 길이와 버튼의 여백의 총합이고 2로 나누어주는 이유는 버튼을 중앙에 표시해주기 위해서다.<br><br><br>

## 도형의 위치에 해당하는 곳에 마우스 클릭 이벤트 만들기

```python
def main():
  drawbuttons()

  for event in pygame.event.get():
      ~
      if event.type == MOUSEBUTTONUP:
          x, y = event.pos
          if pygame.Rect(270, 425, 45, 45).collidepoint(x, y):
              if nowHP != maxHP:
                  nowHP += 1 
          elif pygame.Rect(325, 425, 45, 45).collidepoint(x, y):
              if nowHP != 0:
                  nowHP -= 1
```

MOUSEBUTTONUP 이라는 이벤트는 '마우스를 클릭했을 때'의 이벤트다. 반대로 '마우스를 뗐을 때'의 이벤트는 MOUSEBUTTONDOWN 이다.

클릭한 위치의 좌표를 x, y에 담아주고,
위에 그려진 도형의 좌표안에 x, y값이 들어 있을 때 이벤트를 발생하는 식의 진행이다.<br><br><br>

# 완성된 코드
```python
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
            elif event.type == KEYDOWN:
                if event.key == K_UP:
                    if nowHP != maxHP:   
                        nowHP+=1
                elif event.key == K_DOWN:
                    if nowHP > 0:
                        nowHP-=1
            elif event.type == MOUSEBUTTONUP:
                x, y = event.pos
                if pygame.Rect(270, 425, 45, 45).collidepoint(x, y):
                    if nowHP != maxHP:
                        nowHP += 1 
                elif pygame.Rect(325, 425, 45, 45).collidepoint(x, y):
                    if nowHP != 0:
                        nowHP -= 1


        txtHPbar = txtHPbar_FONT.render("{} / {}".format(nowHP, maxHP), True, red, white)
        
        Screen.fill(white)
        Screen.blit(txtHPbar, txtHPbar_Area)
        drawHP(nowHP)
        drawButtons()

        pygame.display.update() 

def drawHP(HP):
    r = int((ScreenHeight - 40) / maxHP) # Screenheight-40의 값을 maxHP로 나누어준다. 위 아래 20씩 여분공간을 두고 maxHP의 개수를 표현하기 위해 나누어줌

    pygame.draw.rect(Screen, black, (20, 20, 20, 20 + ((maxHP - 0.5) * r)))
    #3번째 인자는 (X, Y, 가로, 세로)이다. 20, 20의 위치부터 검정으로 20, 20+((maxHP-0.5)*r)을 한다는 뜻 

    for i in range(maxHP):
        if HP >= (maxHP - i):
            pygame.draw.rect(Screen, red, (20, 20 + (i*r), 20, r))
        pygame.draw.rect(Screen, white, (20, 20 + (i * r), 20, r), 1)
    
    return

def drawButtons():
    r = 45 #버튼의 반지름
    r_margin = 10 #버튼들간의 간격

    colors=[red, black] #for문을 활용하기위한 colors 리스트

    num = 2 #버튼의 개수
    #r*num = 버튼의 개수, r_margin*(num-1) 은 여백의 총합
    margin = int((ScreenWidth - ((r*num) + (r_margin*(num-1)))) / 2)

    for i in range(0, num):
        left = margin + (i * r) + (i * r_margin)
        up = ScreenHeight - r - 10
        pygame.draw.rect(Screen, colors[i], (left, up, r, r))
        pygame.draw.rect(Screen, white, (left+2, up+2, r-4, r-4), 2)

if __name__ == '__main__':
    main()
```
<br>

# 정리
기능에 따라 함수를 나누어주고, 각 이벤트에 따라 코드를 정리해주면 간단한 게임을 만드는데는 어려움이 없는 것 같다.


