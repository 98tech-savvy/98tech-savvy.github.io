---
title:  "파이게임(pygame) 튜토리얼 - 게임 만들기"
excerpt: "지금까지 배운 pygame을 활용해서 진짜 게임을 만들어보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, pygame, 게임만들기, game, 튜토리얼]

toc: true
toc_sticky: true

date: 2023-04-19
last_modified_at: 2023-04-19
---

# 지금까지 배운 내용
지금까지 텍스트박스를 움직이게하고, 키보드로 움직여보고, 입출력함수에 대해 배우고, 그림을 그려 HP바를 표현하고 마우스의 클릭이벤트를 활용하는 등 기본적인 게임을 플레이하는데 필요한 기능은 전부 배운 것 같다. 이제는 진짜로 게임이라 할만한 것을 만들어보아야할 때다.
<br><br>

# 무슨 색깔이 더 많아? 셀렉트게임
5x5의 보드안에 빨간색과 검정색들의 블록들이 랜덤으로 만들어지고, 블록들의 색깔이 뭐가 더 많은지에 대해 버튼을 눌러서 맞으면 HPbar가 올라가고 틀리면 HPbar가 낮아지는 게임을 만들 것이다. 그 전에 썼던 코드에서 보드를 생성하고 그 보드에 빨간색과 검정색들의 블록이 랜덤으로 생성되는 코드를 적당히 합치면 만들어질 것이다.

# 코드 뜯어보기

만든 함수들은 main(), drawHP(), drawBoard(), randBoard() buttons() 함수다.

## main()

```python
def main():
    nowHP = 5
    board, b_red, b_black = randBoard(boardSize)

    while True:
        txtHP = txtfont.render("{} / {}".format(nowHP, maxHP), True, red, white)

        Screen.fill(white)
        Screen.blit(txtHP, txtHPArea)

        drawHP(nowHP)
        drawBoard(board)
        buttons()

        for event in pygame.event.get():
            if event.type == QUIT or nowHP == 0:
                pygame.quit()
                sys.exit()

            if event.type == MOUSEBUTTONUP: #버튼 이벤트
                x, y = event.pos

                if pygame.Rect(320, 400, 50, 50).collidepoint(x, y):
                    if b_red >= b_black:
                        if nowHP != maxHP:
                            nowHP += 1
                        board, b_red, b_black = randBoard(boardSize)
                    elif b_red < b_black:
                        if nowHP != 0:
                            nowHP -= 1
                        board, b_red, b_black = randBoard(boardSize)
                elif pygame.Rect(250, 400, 50, 50).collidepoint(x, y):
                    if b_red <= b_black:
                        if nowHP != maxHP:
                            nowHP += 1
                        board, b_red, b_black = randBoard(boardSize)
                    elif b_red > b_black:
                        if nowHP != 0:
                            nowHP -= 1
                        board, b_red, b_black = randBoard(boardSize)


        pygame.display.update()
```

1. nowHP의 값을 정해주고 2차원 배열의 board와 빨강과 검정의 개수를 셀 b_red, b_black 변수를 randboard()로부터 반환한 값을 저장해주었다. 

2. 무한 루프문이 시작되면

3. txtHP를 렌더링되어서 상단에 위치하게 하고 fill과 blit로 화면을 표시해준다.

4. 그 다음 만든 함수들 (drawHP, drawBoard, buttons) 함수를 호출해주어 HP바, 보드, 버튼을 그려주고

5. for event in pygame.event.get(): 문으로 이벤트들을 처리한다.

6. 이벤트는 종료할때와 버튼을 눌렀을 때의 이벤트를 만들어주었다.
pygame.Rect().collidepoint() 는 Rect(사각형)안에 마우스커서가 위치해있을때(collidepoint(x,y)) 이벤트를 발생한다.
이 때 개수를 센 b_red와 b_black을 비교해서 nowHP를 증감시키고, 다른 보드를 그려주기 위해 randBoard 함수를 호출해준다.

## drawHP():

```python
def drawHP(HP):
    r = int((ScrHeight - 40) / maxHP)
    pygame.draw.rect(Screen, black, (20, 20, 20, 20 + (maxHP-0.5) * r))

    for i in range(maxHP):
        if HP >= (maxHP-i):
            pygame.draw.rect(Screen, red, (20, 20+(i*r), 20, r))
    pygame.draw.rect(Screen, white, (20, 20, 20, 20 + (maxHP-0.5) * r), 1)
```
이전의 포스팅에서 설명했으니 넘어가겠다.

## randBoard():

```python
def randBoard(size):
    board = []
    b_red = 0
    b_black = 0

    for x in range(size):
        column = []
        for y in range(size):
            column.append(randint(0,1))
        board.append(column)
    
    for x in range(size):
        for y in range(size):
            if board[x][y] == 1:
                b_red += 1
            elif board[x][y] == 0:
                b_black += 1
    
    return board, b_red, b_black
```
보드를 그리는 함수는 아니고, 보드의 배열[x][y] 값에 랜덤 함수를 사용해 0 or 1을 넣어주고
그 board[x][y]가 1일 때는 b_red에 1을 추가하고 0일 때는 b_black에 1을 추가해준다.

## drawBoard():

```python
def drawBoard(board):
    r = 50
    LEFT = (ScrWidth/2)-(boardSize*(r/2))
    UP = (ScrHeight/2)-(boardSize*(r/2))
    
    for x in range(boardSize):
        for y in range(boardSize):
            LEFT_X = x * r + LEFT
            UP_Y = y * r + UP 
            if board[x][y] == 1:
                color = red
            elif board[x][y] == 0:
                color = black
               
            pygame.draw.rect(Screen, color, (LEFT_X, UP_Y, r, r))
```
randBoard()에서 return한 board를 인자로 받아서 실제로 그려주는 역할을 한다. LEFT와 UP은 보드 전체 테두리의 위치의 변수고 LEFT_X와 UP_Y 는 그려주는 사각형의 위치이다.

## buttons():

```python
def buttons():
    r = 50
    colors = [red, black]
    num = 2
    margin = 20
    for i in range(num):
        pygame.draw.rect(Screen, colors[i], ((ScrWidth/2)-(r*i+margin*i), ScrHeight - 80, r, r))
        pygame.draw.rect(Screen, white, (((ScrWidth/2)-(r*i+margin*i)+2, ScrHeight - 80+2, r-4, r-4)), 1)
```
이 또한 넘어가도록 하겠다.

# 완성된 코드

```python
import pygame, sys
from pygame.locals import *
from random import *

#colors###########################
red = (255, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)

white = (255, 255, 255)
black = (0, 0, 0)
##################################

pygame.init()
pygame.display.set_caption("RED/BLACK SELECT GAME")

ScrWidth = 640 
ScrHeight = 480
Screen = pygame.display.set_mode((ScrWidth, ScrHeight))

maxHP = 10
txtfont = pygame.font.Font(None, 32)
txtHP = txtfont.render("{} / {}".format(maxHP, maxHP), True, red, white)
txtHPArea = txtHP.get_rect()
txtHPArea.center = (ScrWidth/2, 40)

boardSize = 5

##################################

def main():
    nowHP = 5
    board, b_red, b_black = randBoard(boardSize)

    while True:
        txtHP = txtfont.render("{} / {}".format(nowHP, maxHP), True, red, white)

        Screen.fill(white)
        Screen.blit(txtHP, txtHPArea)

        drawHP(nowHP)
        drawBoard(board)
        buttons()

        for event in pygame.event.get():
            if event.type == QUIT or nowHP == 0:
                pygame.quit()
                sys.exit()

            if event.type == MOUSEBUTTONUP: #버튼 이벤트
                x, y = event.pos

                if pygame.Rect(320, 400, 50, 50).collidepoint(x, y):
                    if b_red >= b_black:
                        if nowHP != maxHP:
                            nowHP += 1
                        board, b_red, b_black = randBoard(boardSize)
                    elif b_red < b_black:
                        if nowHP != 0:
                            nowHP -= 1
                        board, b_red, b_black = randBoard(boardSize)
                elif pygame.Rect(250, 400, 50, 50).collidepoint(x, y):
                    if b_red <= b_black:
                        if nowHP != maxHP:
                            nowHP += 1
                        board, b_red, b_black = randBoard(boardSize)
                    elif b_red > b_black:
                        if nowHP != 0:
                            nowHP -= 1
                        board, b_red, b_black = randBoard(boardSize)


        pygame.display.update()

def drawHP(HP):
    r = int((ScrHeight - 40) / maxHP)
    pygame.draw.rect(Screen, black, (20, 20, 20, 20 + (maxHP-0.5) * r))

    for i in range(maxHP):
        if HP >= (maxHP-i):
            pygame.draw.rect(Screen, red, (20, 20+(i*r), 20, r))
    pygame.draw.rect(Screen, white, (20, 20, 20, 20 + (maxHP-0.5) * r), 1)


def drawBoard(board):
    r = 50
    LEFT = (ScrWidth/2)-(boardSize*(r/2))
    UP = (ScrHeight/2)-(boardSize*(r/2))
    
    for x in range(boardSize):
        for y in range(boardSize):
            LEFT_X = x * r + LEFT
            UP_Y = y * r + UP 
            if board[x][y] == 1:
                color = red
            elif board[x][y] == 0:
                color = black
               
            pygame.draw.rect(Screen, color, (LEFT_X, UP_Y, r, r))


def randBoard(size):
    board = []
    b_red = 0
    b_black = 0

    for x in range(size):
        column = []
        for y in range(size):
            column.append(randint(0,1))
        board.append(column)
    
    for x in range(size):
        for y in range(size):
            if board[x][y] == 1:
                b_red += 1
            elif board[x][y] == 0:
                b_black += 1
    
    return board, b_red, b_black

def buttons():
    r = 50
    colors = [red, black]
    num = 2
    margin = 20
    for i in range(num):
        pygame.draw.rect(Screen, colors[i], ((ScrWidth/2)-(r*i+margin*i), ScrHeight - 80, r, r))
        pygame.draw.rect(Screen, white, (((ScrWidth/2)-(r*i+margin*i)+2, ScrHeight - 80+2, r-4, r-4)), 1)

if __name__ == "__main__":
    main()
```

# 정리
코드를 따라하지않고 머릿속으로 그리면서 프로그래밍을 해보았는데 내가 그리는 코드에 진행된다는게 흥미롭고 하나하나 함수가 완성될 때마다 재미를 느꼈다. rect대신 이미지를 활용한다면 좀 더 고퀄리티의 게임을 만들 수 있을 것 같다. 사운드를 넣어준다던가, 스코어 보드를 만든다던가 하는 식으로 말이다.