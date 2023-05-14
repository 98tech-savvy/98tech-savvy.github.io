---
title:  "[Python] 업무자동화(RPA) 2편 - 윈도우 자동화"
excerpt: "Python으로 회사의 반복적인 업무를 자동화 해보자. 윈도우 자동화하기"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, 윈도우]

toc: true
toc_sticky: true

date: 2023-05-14
last_modified_at: 2023-05-14
---


# pyautogui
pyautogui는 파이썬의 인기있는 모듈 중에 하나이다. 이 모듈을 사용하면 키보드와 마우스 입력을 할 수도 있고, 이미지를 찾아내 그 위치를 반환시킬 수도 있다.

``pip install pyautogui``를 터미널에 입력해 설치할 수 있으며 [PyAutoGUI documentation](https://pyautogui.readthedocs.io/en/latest/)에서 여러가지 기능들을 확인할 수 있다.

# 사용 방법
pyautogui를 사용하면 마우스를 클릭하거나, 키보드를 입력하거나 등의 여러가지 이벤트를 수행할 수 있다. 하지만 한글은 지원이 되지 않기 때문에 만약 한글로 키보드 입력을 시도했다면 공백을 표시하는 것을 볼 수 있을 것이다. **만약 한글 텍스트를 입력하고 싶다면**

``pip install pyperclip``을 터미널에 입력해 pyperclip을 설치해준 다음 pyperclip 모듈로 클립보드에 한글 텍스트를 저장하고 붙여넣기 하는 식으로 사용하면 된다.

이전의 [업무자동화(RPA) 1편 - 엑셀](https://98tech-savvy.github.io/python/CS-RPA-1-EXCEL/) 에서 학생들의 데이터를 받아서 성적을 표시해주는 엑셀파일을 만들었다. 이 엑셀파일의 데이터를 가지고 파워포인트에 카드형식으로 저장해주는 프로그램을 만들어보자.

# 완성된 코드

ppt와 엑셀을 자동으로 실행시켜주지는 않지만 필요한 파일을 띄워놓으면 자동으로 성적을 입력해주는 프로그램을 만들었다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/4ac64242-61f7-4225-a645-faae20537cca)


```python
import pyautogui

test = 0
if test == 1:
    pyautogui.mouseInfo()
else:
    # 현재 화면 크기를 반환하는 변수 Width [0] Height [1]
    now_display_size = pyautogui.size()

    # 엑셀을 저장할 변수
    excel = pyautogui.getWindowsWithTitle("Excel")[0]
    print(excel)
    # 파워포인트를 저장할 변수
    ppt = pyautogui.getWindowsWithTitle("PowerPoint")[0]
    print(ppt)

    # 반복할 횟수
    repeat_count = 10
    # 엑셀/파워포인트 활성화 시키고 화면 왼쪽, 오른쪽으로 나누기
    if excel.isActive == False:
        excel.activate()

    excel.maximize()
    pyautogui.hotkey("win", "left")

    pyautogui.sleep(1)

    if ppt.isActive == False:
        ppt.activate()

    ppt.maximize()
    pyautogui.hotkey("win", "right")

    # 데이터 복사

    # 엑셀 학번 위치 반환
    student_id = [113, 376]
    # 엑셀 총점 위치 반환
    student_total_score = [723, 379]
    # 엑셀 성적 위치 반환
    student_record = [749, 380]

    # 엑셀 셀 간의 간격 크기
    cell_interval = 30

    # 파워포인트 학번 위치 반환
    student_ppt_id = [1618, 563]
    # 파워포인트 총점 위치 반환
    student_ppt_total_score = [2450, 558]
    # 파워포인트 성적 위치 반환
    student_ppt_record = [2041, 721]

    # 자동화

    for i in range(0, repeat_count):
        excel.activate()
        pyautogui.click(student_id, duration=0.25)
        pyautogui.hotkey("ctrl", "c")

        ppt.activate()
        pyautogui.doubleClick(student_ppt_id, duration=0.25)
        pyautogui.hotkey("ctrl", "v")

        student_id[1] += cell_interval

        excel.activate()
        pyautogui.click(student_total_score, duration=0.25)
        pyautogui.hotkey("ctrl", "c")
        ppt.activate()
        pyautogui.doubleClick(student_ppt_total_score, duration=0.25)
        pyautogui.hotkey("ctrl", "v")

        student_total_score[1] += cell_interval

        excel.activate()
        pyautogui.click(student_record, duration=0.25)
        pyautogui.hotkey("ctrl", "c")
        ppt.activate()
        pyautogui.doubleClick(student_ppt_record, duration=0.25)
        pyautogui.hotkey("ctrl", "v")

        student_record[1] += cell_interval

        pyautogui.click(1899, 347)  # 빈 공간 클릭
        pyautogui.hotkey("down") # ppt 슬라이드를 넘겨줌

```

단순한 매크로를 만드는 프로그래밍을 해보았다. 단순히 마우스의 위치와 클릭만 해줄게 아니라 그 창을 활성화 시켜주고 창을 적절한 크기에 갖다주는것이 중요한 것 같다.