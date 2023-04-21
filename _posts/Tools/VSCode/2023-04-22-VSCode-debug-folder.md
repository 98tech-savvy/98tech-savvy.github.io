---
title:  "[VSCode] 디버그 시작 경로 변경 (디버그 폴더 변경)"
excerpt: "디버그 시작 경로를 변경해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - VSCode
tags:
  - [VSCode, Debug, 디버그, 디버깅 폴더 변경, No working directory found]

toc: true
toc_sticky: true

date: 2023-04-22
last_modified_at: 2023-04-22
---

# No working directory found
VSCode에서 디버그를 하면 원래는 잘 작동하던 상대경로가 No Working directory found! 같은 에러를 뿜는걸 볼 수 있다. **디버깅의 시작 경로가 바뀌어서 그런건데** 몇번의 클릭으로 간단히 바꿔줄 수 있다.

*상대 경로의 예시*

```pyhon
Weapon = pygame.image.load("PythonWorkspace/pygame/arcade_game/images/weapon.png")
bullet = pygame.image.load("PythonWorkspace/pygame/arcade_game/images/bullet.png")
```
<br><br>

# 해결 방법, 디버깅 시작 경로 변경
![image](https://user-images.githubusercontent.com/128434645/233734069-d1147430-09a5-486e-93ce-8300c7fe3945.png)

빨간색 동그라미의 버튼을 눌러준다. 그러면 '실행 및 디버그' 탭으로 이동한다.


![image](https://user-images.githubusercontent.com/128434645/233734292-ff9b4c4f-1d6e-4ab7-9bcc-af71ed21e1ec.png)

초록색 ▷ 버튼을 눌러주면 '구성' 을 추가할 수 있는데, 자신이 원하는 시작 경로로 설정해주고 디버깅을 다시 해보면 문제 없이 디버깅하고 터미널에 원하는 경로가 나오는 것을 볼 수 있다.
