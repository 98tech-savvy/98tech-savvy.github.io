---
title:  "[Python] test"
excerpt: "ChatGPT를 openai 모듈로 불러와서 Python으로 코딩해서 대화해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, ChatGPT, OpenAI, 인공지능]

toc: true
toc_sticky: true

date: 2023-04-21
last_modified_at: 2023-04-21
---

# 사용한 이미지
그림판에서 크기만 조절하고 페인트칠해서 사용했다. 이 게임의 이미지만 바꿔줘도 옛날 고전게임의 느낌을 낼 수 있을것같다.

![background](https://user-images.githubusercontent.com/128434645/233638504-f46a50a0-c227-4c0a-86ab-69813f93e3f9.png)
백그라운드(배경)

![ball](https://user-images.githubusercontent.com/128434645/233638507-43337059-9c06-4a14-b577-75bed30bb204.png)
볼 크기 1
![ball2](https://user-images.githubusercontent.com/128434645/233638513-cd45c829-43e9-4707-a795-61e287ef8f3d.png)
볼 크기 2
![ball3](https://user-images.githubusercontent.com/128434645/233638516-45746c72-012d-44a6-ac0b-cce1e88207a7.png)
볼 크기 3


![bullet](https://user-images.githubusercontent.com/128434645/233638519-9ebd2a31-32ce-482c-8480-5d46b3e2cfe5.png)
총알


![character](https://user-images.githubusercontent.com/128434645/233638520-75a7af7d-e5ed-46e5-98d8-322232e08ffe.png)
캐릭터


![weapon](https://user-images.githubusercontent.com/128434645/233638523-5a20bc92-618b-46ae-a2cb-fba9e08863da.png)
무기

# 소스 코드

```python
import pygame, sys
from pygame.locals import *

pygame.init() #pygame 초기화
pygame.display.set_caption("공 부수기 게임") #제목 설정

#색깔 (R, G, B)
Red = (255, 0, 0)
Blue = (0, 0, 255)
Green = (0, 255, 0)
Black = (0, 0, 0)
White = (255, 255, 255)

#이미지, 폰트 로드

##메인 스크린
ScrWidth = 640
ScrHeight = 480
Screen = pygame.display.set_mode((ScrWidth, ScrHeight))
background = pygame.image.load("C:/Users/Seounb/Desktop/Workspace/PythonWorkspace/pygame/arcade_game/images/background.png")

##메인 폰트
FontType = pygame.font.SysFont("NanumGothic", 32)
mainFont = FontType.render("GAME OVER", True, Red, None)
mainFont_Rect = mainFont.get_rect()
mainFont_Rect.center = (ScrWidth/2, ScrHeight/2)

##캐릭터 이미지
Character = pygame.image.load("C:/Users/Seounb/Desktop/Workspace/PythonWorkspace/pygame/arcade_game/images/character.png")
Character_size = Character.get_rect().size
Character_width = Character_size[0]
Character_height = Character_size[1]
Character_xpos = ScrWidth/2 - Character_width
Character_ypos = ScrHeight - Character_height
Character_tox = 0
Character_toy = 0


##공 이미지
ball_images = [
     pygame.image.load("PythonWorkspace/pygame/arcade_game/images/Ball.png"),
     pygame.image.load("PythonWorkspace/pygame/arcade_game/images/Ball2.png"),
     pygame.image.load("PythonWorkspace/pygame/arcade_game/images/Ball3.png")
]

ball_speed_y = [-18, -15, -12, -9]

balls = []

#최초 발생 공
balls.append({
    "pos_x" : 50,
    "pos_y" : 50,
    "img_idx" : 0,
    "to_x" : 3,
    "to_y" : -6,
    "init_spd_y" : ball_speed_y[0]
})

#총알 사라짐, 공 정보 저장
bullet_to_remove = -1
ball_to_remove = -1

##무기 이미지
Weapon = pygame.image.load("PythonWorkspace/pygame/arcade_game/images/weapon.png")
bullet = pygame.image.load("PythonWorkspace/pygame/arcade_game/images/bullet.png")
bullet.get_rect().size
bullet_width = bullet
bullets = []
bullet_speed = 10

#FPS
clock = pygame.time.Clock()

#시간
total_time = 30
start_time = pygame.time.get_ticks()

#무한 루프문
running = True
while running:
    game_frame = clock.tick(60)

    Screen.blit(background, (0 ,0))

    for event in pygame.event.get():
        if event.type == QUIT:
            running = False
        #캐릭터 위치
        elif event.type == KEYDOWN:
            if event.key == K_RIGHT:
                Character_tox += 5
            elif event.key == K_LEFT:
                Character_tox -= 5
            #총알 발사
            elif event.key == K_SPACE:
                bullet_xpos = Weapon_xpos + (Character_width/7)
                bullet_ypos = Weapon_ypos
                bullets.append([bullet_xpos, bullet_ypos])

        elif event.type == KEYUP:
            if event.key == K_RIGHT:
                Character_tox = 0
            elif event.key == K_LEFT:
                Character_tox = 0



    # 경계값 제한
    if Character_xpos > ScrWidth - Character_width:
        Character_xpos = ScrWidth-Character_width
    elif Character_xpos < 0:
        Character_xpos = 0
    
    #총알 위치 조정
    bullets = [ [b[0], b[1] - bullet_speed] for b in bullets]
    
    #공 튕기기
    for ball_idx, ball_val in enumerate(balls): #enumerate 를 사용하면
    #인덱스값과 그에 해당하는 밸류값을 같이 가져와서 저장함
        ball_pos_x = ball_val["pos_x"]
        ball_pos_y = ball_val["pos_y"]
        ball_img_idx = ball_val["img_idx"]

        ball_size = ball_images[ball_img_idx].get_rect().size
        ball_width = ball_size[0]
        ball_height = ball_size[1]

        #튕기는 효과
        if ball_pos_x < 0 or ball_pos_x > ScrWidth-ball_width:
            ball_val["to_x"] = ball_val["to_x"] * -1
        #점프 효과
        if ball_pos_y >= ScrHeight - ball_height:
            ball_val["to_y"] = ball_val["init_spd_y"]
        else:
            ball_val["to_y"] += 0.5

        ball_val["pos_x"] += ball_val["to_x"]
        ball_val["pos_y"] += ball_val["to_y"]

    #충돌 처리
    CharacterRect = Character.get_rect()
    CharacterRect.left = Character_xpos
    CharacterRect.top = Character_ypos
    Character_xpos = Character_xpos + Character_tox

    #공, 캐릭터 충돌
    for ball_idx, ball_val in enumerate(balls):
        ball_pos_x = ball_val["pos_x"]
        ball_pos_y = ball_val["pos_y"]
        ball_img_idx = ball_val["img_idx"]

        ball_rect = ball_images[ball_img_idx].get_rect()
        ball_rect.left = ball_pos_x
        ball_rect.top = ball_pos_y

        if CharacterRect.colliderect(ball_rect):
            running = False
            break
    
    #공, 총알 충돌
    for bullet_idx, bullet_val in enumerate(bullets):
        bullet_xpos = bullet_val[0]
        bullet_ypos = bullet_val[1]

        bullet_rect = bullet.get_rect()
        bullet_rect.left = bullet_xpos
        bullet_rect.top = bullet_ypos

        if bullet_rect.colliderect(ball_rect):
            bullet_to_remove = bullet_idx
            ball_to_remove = ball_idx

            if ball_img_idx < 2:
                ball_with = ball_rect.size[0]
                ball_height = ball_rect.size[1]

                small_ball_rect = ball_images[ball_img_idx+1].get_rect()
                small_ball_width = small_ball_rect.size[0]
                small_ball_height = small_ball_rect.size[1]

                balls.append({
                "pos_x" : ball_pos_x + (ball_width/2) - (small_ball_width/2),
                "pos_y" : ball_pos_y + (ball_height/2) - (small_ball_height/2),
                "img_idx" : ball_img_idx + 1,
                "to_x" : -3,
                "to_y" : -6,
                "init_spd_y" : ball_speed_y[ball_img_idx + 1]
                })

                balls.append({
                "pos_x" : ball_pos_x + (ball_width/2) - (small_ball_width/2),
                "pos_y" : ball_pos_y + (ball_height/2) - (small_ball_height/2),
                "img_idx" : ball_img_idx + 1,
                "to_x" : 3,
                "to_y" : -6,
                "init_spd_y" : ball_speed_y[ball_img_idx + 1]
                })
            break
        else:
            continue
        break
    
    if bullet_to_remove > -1:
        del bullets[bullet_to_remove]
        bullet_to_remove = -1
    
    if ball_to_remove > -1:
        del balls[ball_to_remove]
        ball_to_remove = -1

    #TIMER
    elapsed_time = int((pygame.time.get_ticks() - start_time) / 1000)
    rendtimer = FontType.render("{}".format(total_time-elapsed_time), True, Red)

    if total_time - elapsed_time <= 0:
        running = False
    
    #BLIT
    for bullet_xpos, bullet_ypos in bullets:
        Screen.blit(bullet, (bullet_xpos, bullet_ypos))

    for idx, val in enumerate(balls):
        ball_pos_x = val["pos_x"]
        ball_pos_y = val["pos_y"]
        ball_img_idx = val["img_idx"]
        Screen.blit(ball_images[ball_img_idx], (ball_pos_x, ball_pos_y))

    Weapon_xpos = Character_xpos + (Character_width/2)
    Weapon_ypos = Character_ypos - (Character_height/2)

    Screen.blit(Character, (Character_xpos, Character_ypos))
    Screen.blit(Weapon, (Weapon_xpos, Weapon_ypos))
    Screen.blit(rendtimer, (10, 10))

    pygame.display.update()

Screen.blit(mainFont, mainFont_Rect)
pygame.display.update()
pygame.time.delay(2000)
```

