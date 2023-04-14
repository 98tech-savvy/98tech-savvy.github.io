---
title:  "[VSCode] 유용한 단축키들 모음"
excerpt: "세계에서 제일 많이 쓰이는 VSCode의 단축키들을 정리하고 알아보는 포스트"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - VSCode
tags:
  - [VSCode, Texteditor, VS코드, 비쥬얼스튜디오, 단축키]

toc: true
toc_sticky: true

date: 2023-04-15
last_modified_at: 2023-04-15
---
# 시작하기전에
코딩 공부를 하면서 VSCode를 사용하고있는데 예전에 공부했던 프로그램의 환경과는 많이 달라서 너무 편하고 마음에 들었다. 그래서 좀 더 세밀히 알아보기 위해서 포스팅을 하기로했다. VSCode에는 **주석처리** 라던가 **글자 한 번에 바꾸기**라던가 유용한 단축키와 기능들이 많다. 

# 바로가기 키(단축키) 설정
VSCode상의 ``파일 >> 기본설정 >> 바로가기 키`` or ``Ctrl + K >> Ctrl + S``로 나열된 단축키들을 볼 수 있으며 **해당 기능의 키보드 매핑또한 가능**하다.

많이 사용하는데 불편했던 단축키가 있다면 여기서 바꿔주는걸 추천한다.

# 많이 사용하는 단축키
내가 공부를 하며 많이 사용했던 단축키들을 모았다.

## F5, 디버그 시작
코딩을 하면서 에러가 났는지 연산을 잘못했는지 확인하기 위한 디버깅 버튼을 누르지 않고 F5만 눌러주면 편하게 디버그를 시작할 수 있다.

## Ctrl+F, 찾기
![image](https://user-images.githubusercontent.com/128434645/231786908-31d67f13-ac4e-4ec7-a9cb-362b6dbafe75.png)

찾기 창을 활성화 할 수 있다.

## Ctrl+H, 바꾸기
![image](https://user-images.githubusercontent.com/128434645/231787225-c48ff587-4c1f-41e2-89f7-6c79b56e6b5b.png)

찾기 창의 아래에 바꾸기 창이 활성화 된다. 찾기에서 찾은 단어를 바꾸기에 넣은 단어로 바꾸어준다.

## HOME, 행의 시작으로 이동
커서가 위치한 행의 첫 번째 위치(제일 왼쪽)으로 커서를 이동시켜준다.

## END, 행의 끝으로 이동
커서가 위치한 행의 마지막 위치(제일 오른쪽)으로 커서를 이동시켜준다.

## Ctrl+/, 주석 토글
![image](https://user-images.githubusercontent.com/128434645/231787969-19a48869-f73d-4e1f-b508-97cf075be267.png)

.md 파일을 작성하고있어서 '\<!--  -->'으로 바뀌어진 모습이다. Python의 경우 각 행마다 제일 왼쪽에 주석 문자인 '#'이 달린다.

## Ctrl+[, 내어쓰기
들여쓰기(Ctrl + ])는 Tab을 사용해서 잘 쓰지 않고, 전체적으로 코드의 탭을 하나씩 뺄 때 사용한다.

## Shift + Ctrl + 방향키, 한 단어씩 블럭설정
![image](https://user-images.githubusercontent.com/128434645/231795481-8c5c0d4b-caa1-4147-a48c-2e4ecce34fea.png)
Shift + 방향키는 한 글자씩 블럭설정. 한 단어씩 블럭(하얗게 되는 부분)설정이 되는데 직접
해보는게 이해가 빠르다.

## Alt + Click(마우스), 다중 커서
![image](https://user-images.githubusercontent.com/128434645/231796011-d2edb7fc-9469-4ef1-bf25-2f26c1785909.png)
클릭한 곳에 다중 커서를 둘 수 있다. 변수를 한 번에 수정할 때, 반복된 코드를 적어줄 때 사용한다.

## Ctrl + `(백틱), 터미널 열기/닫기
터미널을 열고 닫는다.

## Ctrl + B, 왼쪽 탐색기 켜기/끄기
왼쪽의 탐색기(폴더와 파일 부분)을 열고 닫는다.

## Ctrl + '+', Ctrl + '-', 폰트 사이즈 조절
폰트의 크기를 크게, 작게 바꿔준다. 눈 아플 때 사용하면 좋은 단축키.

## Ctrl + G, 해당 라인으로 이동
다른 사람들의 코드에 대한 설명을 볼 때 쓰면 좋다. 몇 번줄 ~ 의 설명에 몇 번줄~의 라인으로 바로 이동한다.

## Ctrl + Click(클릭) or F12, 해당 함수 정의문으로 바로 이동
해당 함수의 정의문으로(함수의 세부내용) 바로 이동한다.

## Alt + (↑,↓), 한 줄 이동
코드의 위치를 수정할 때 사용하면 좋다. 커서에 위치한 코드(한 줄)의 코드가 방향키 방향으로 이동한다.

## Shift + Alt + (↑,↓), 한 줄 복사
한 줄을 해당 방향으로 복사한다.

## Ctrl + X, 한 줄 삭제
잘라내기라고 보셔도 되고, 한 줄 삭제로 봐도 좋은 단축키. 커서에 위치한 부분의 라인을 삭제한다.

## Ctrl + Shift + L, 같은 단어 전체 선택
Greed 라는 변수가 있을 때, Greed를 토글하고 해당 단축키를 눌러주면 코드 전체에 위치한 Greed를 선택한다. 타이핑으로 수정도 가능.

## Ctrl + '.' ,없는 모듈 찾아주기
모듈이 없다고 에러가 나올 시, 혹은 선언된 변수가 없다고 에러가 나올 시 사용해주면 좋은 단축키.

# 그 외 단축키들
찾고있던 단축키가 없다면,

한글 [demun님의 github에 VSCode Tutorial](https://demun.github.io/vscode-tutorial/shortcuts/)
영어 [VSCode Key Bindings](https://code.visualstudio.com/docs/getstarted/keybindings)

를 참고하자.