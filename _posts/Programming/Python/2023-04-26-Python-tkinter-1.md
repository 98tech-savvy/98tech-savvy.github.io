---
title:  "tkinter에 대해 알아보자"
excerpt: "파이썬의 기본 모듈 중 하나인 GUI를 구성할 수 있는 tkinter에 대해 알아보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, tkinter, module, 파이썬 tkinter]

toc: true
toc_sticky: true

date: 2023-04-26
last_modified_at: 2023-04-26
---

# GUI 프로그래밍
예전에 취미로 인터넷에서 추천받은 책으로 공부했던 C와 C++ 기초서적은 콘솔 창에서 *의 피라미드를 만들고, 콘솔창으로 계산기를 만드는 둥의 재미는 있지만 윈도우의 계산기와 비교해보자니 만족도가 떨어지는 그런 공부를 했다. 그래서인지 비쥬얼베이직6는 기초부터 직관적인 버튼과 텍스트, 그림들이 내 코드에 반응하는걸 봐서 그런지 좀 더 재밌게 공부했던 것 같다. 파이썬에서는 모듈을 활용해 GUI 프로그래밍을 구현할 수 있는데, 그 중 하나인 tkinter를 소개하겠다.

# tkinter
tkinter는 파이썬에서 기본으로 제공해주는 GUI 관련 모듈이다. tkinter말고도 wxPython, PySide, PyQt같은 여러 gui 모듈이 있지만 가장 쉽고 빠르게 개발할 수 있는 tkinter를 공부해보겠다.

파이썬을 설치하며 기본적으로 설치되는 모듈이기 때문에 따로 인스톨해줄 필요가 없다.

# 기본

```python
from tkinter import *
```

를 선언해주면 tkinter를 사용할 수 있다.

```python
root = Tk()
root.mainloop()
```

root 라는 변수에 Tk클래스 객체를 생성해주고, 그리고 root.mainloop()로 메인루프 선언을 해준다. 메인루프는 키보드나 마우스, 화면 Redraw같은 다양한 이벤트로부터 오는 메시지를 받고 전달하는 역할을 해준다.

# 위젯

|위젯|설명|
|---|---|
|Button|버튼|
|Label|텍스트/이미지 표시|
|CheckButton|체크박스|
|Entry|한 줄 텍스트 박스|
|Text|여러 줄 텍스트 박스|
|ListBox|리스트 박스|
|RadioButton|옵션 버튼|
|Message|Label과 비슷하게 텍스트를 표시하나 팝업창으로 띄움|
|Scale|슬라이스 바|
|Scrollbar|스크롤 바|
|Menu|메뉴|
|Menubutton|메뉴 버튼|
|Toplevel|새 윈도우 창을 띄울 때 사용한다|
|Frame|컨테이너 위젯(다른 위젯들을 그룹화할 때)|
|Canvas|그래프와 점으로 그림을 그릴 수 있다|

Tkinter에는 제한된 핵심 위젯들만을 제공한다. 위의 표는 그 위젯의 이름과 설명이다.

## geometry

geometry로 창의 크기와 어디에 창을 띄울지 선언해줄 수 있다.

```python
from tkinter import *

root = Tk()
root.geometry("640x480+100+300") #WidthxHeight+X+Y
root.mainloop()
```
![image](https://user-images.githubusercontent.com/128434645/234459693-cf243a66-e5cb-403a-b4e4-2ec1d89b3f7e.png)

화면의 X=100, Y=300에 위치하는 곳에 640x480의 창을 띄운 것을 확인할 수 있다.

## title

위의 프로그램 사진에 보면 '98tech-savvy'라는 제목이 정해져있는데, title로 프로그램의 제목을 정해줄 수 있다.

```python
root.title("98tech-savvy")
```

## resizable

프로그램의 테두리에 마우스를 갖다대면, 창 크기를 조절할 수 있어 마우스 커서가 반응하는 모습을 볼 수 있다. 만약 프로그램을 만들 때 창 크기를 고정하고싶다면

```python
root.resizable(False, False) #가로, 세로
```

를 해주면 된다. 여기서 첫 번째 인자는 가로를, 두 번째 인자는 세로를 뜻한다.

## pack()

```python
btn1 = Button(root, text="버튼1")
btn1.pack()
```

단순히 위의 코드 btn1 = Button(~)만 작성해주고 디버깅을 해보면 실행된 프로그램 창에 버튼이 보이지 않는다. 버튼이나 리스트 박스, 체크 박스 등 여러가지 위젯등을 보여주기 위해서는 위젯의 변수.pack()을 해주어야한다.

## Button

말 그대로 버튼을 생성해준다.

``Button(마스터(root), 옵션들)`` 로 간단하게 설명할 수 있는데, 마스터에는 Tk클래스 객체를, 옵션들에는 text, padx, width 같은 여러가지 버튼을 설정해주는 옵션을 추가해주면 된다.

```python
from tkinter import *

root = Tk()
root.title("98tech-savvy")
root.resizable(False, False)
root.geometry("640x480+100+100")

btn1 = Button(root, text="버튼111111111111", padx=10, pady=10)
btn2 = Button(root, text="버튼222222222222", width=10, height=5)
btn3 = Button(root, text="버튼333333333333", bg="red", fg="yellow")

btn1.pack()
btn2.pack()
btn3.pack()
root.mainloop()

```

1. btn1
btn1은  padx 와 pady로 **여백**을 설정해주었다. 자세한건 아래에서 설명하겠다.

2. btn2
btn2은 width와 height로 **크기**를 설정해주었다.

3. btn3
btn3은 fg(**f**ore**g**round)와 bg(**b**ack**g**round)로 컬러를 설정해주었다.


![image](https://user-images.githubusercontent.com/128434645/234461166-a34354cd-1524-4d69-a5e5-f9a3b855d2ce.png)

위 사진을 보면 버튼1과 버튼2의 차이점이 보인다. 그리고 이것은 padx,y와 width,height의 차이점이다.

버튼1의 경우 텍스트의 **크기에 따라 버튼이 늘어나는데**,
버튼2의 경우는 텍스트가 버튼의 크기를 벗어났음에도 불구하고 그 **크기를 유지한다**.

버튼3은 백그라운드 컬러와 포어그라운드 컬러를 설정해준 값으로 빨강색 배경화면에 노란색 글자를 보여주고있음을 알 수 있다.

버튼은 단순히 보여주기 위한 것이 아니라 기능이 있어야한다. command=로 기능을 지정해주겠다.

```python
def defcmd():
  print("버튼이 클릭되었음")

btn1 = Button(text="버튼", command=defcmd)
btn1.pack()
```
![image](https://user-images.githubusercontent.com/128434645/234462713-786b583d-67f8-4f73-9d39-ba881eb455ef.png)

버튼을 누르니 터미널에 "버튼이 클릭되었음"이 출력됨을 볼 수 있다.

## label
레이블은 단순하게 텍스트나 이미지를 표시해줄 수 있다.

```python
from tkinter import *

root = Tk()
root.title("98tech-savvy")
root.geometry("640x480+100+300") #가로x세로+x좌표+y좌표 : 해상도 가로x세로 / 화면의 x좌표 y좌표에 뜸
root.resizable(False, False) #가로, 세로 크기 변경 불가

label1 = Label(root, text="gg")
label1.pack()

photo = PhotoImage(file="PythonWorkspace/gui_basic/img.png")
label2 = Label(root, image=photo)
label2.pack()
```

![image](https://user-images.githubusercontent.com/128434645/234463051-a07205c2-8ef7-4774-948f-9bd592d37ad9.png)

'gg'와 이미지를 성공적으로 보여주고 있다.

버튼을 누르면 체크 모양의 이미지가 X모양의 이미지로 바뀌는 기능을 구현해보자.

```python
from tkinter import *

root = Tk()
root.title("98tech-savvy")
root.geometry("640x480+100+300")  # 가로x세로+x좌표+y좌표 : 해상도 가로x세로 / 화면의 x좌표 y좌표에 뜸
root.resizable(False, False)  # 가로, 세로 크기 변경 불가

label1 = Label(root, text="gg")
label1.pack()

photo = PhotoImage(file="PythonWorkspace/gui_basic/img.png")
label2 = Label(root, image=photo)
label2.pack()


def changelabel():
    global photo2
    photo2 = PhotoImage(file="PythonWorkspace/gui_basic/x.png")
    label2.config(image=photo2)


btn1 = Button(text="클릭", command=changelabel)
btn1.pack()

root.mainloop()

```

``def changelabel():`` 함수를 보면, ``global photo2``로 전역변수 처리를 해준걸 볼 수 있다. **가비지 컬렉션<sup>garbage collection</sup>**이라는 녀석 때문인데, 이 녀석은 필요없는 변수를 처리하기위한 기능을 가지고있다. 그래서 함수의 실행이 끝나면 지역변수들을 처리하는데, 이 때 지역변수를 처리해버리면 photo2가 사라져버리기 때문에 전역변수 처리를 해주어서 가비지 컬렉션이 청소를 못하게 막는 역할을 한다.

## text
텍스트는 텍스트를 보여줄 수도 입력할 수도 있는 텍스트박스 기능을 가지고 있다.

```python
txt1 = Text(root, width=30, height=30)
txt1.pack()

txt1.insert(END, "기본 값")
```
의 방법으로 텍스트박스를 만들 수 있고, ``변수.insert(END, "내용")``으로 프로그램이 실행될 때 기본 값을 지정해줄 수 있다. 여기서 END의 자리에 0이들어가면 제일 첫 번째 자리, END는 제일 마지막 자리(인덱스값)으로 바뀐다.

## entry
entry는 비밀번호를 입력한다던가 아이디를 입력한다는 둥의 여러 라인이 필요없고 한 라인만 있으면 될 때 사용하는 텍스트박스이다. text와 기능은 동일하나 줄바꿈(enter)가 불가능하다.

```python
txt1 = Text(root, width=30, height=30)
txt1.pack()

txt1.insert(END, "기본 값")

e1 = Entry(root, width=30)
e1.pack()

def btncmd():
    #내용 출력
    print(txt1.get("1.0", END)) #1: 1번째 라인, 0: 0번째 column 위치
    print(e1.get())

    #내용 삭제
    txt1.delete("1.0", END)
    e1.delete(0, END)

btn2 = Button(root, text="클릭", command=btncmd)
btn2.pack()
```

변수.get으로 해당 변수의 내용을 읽어낼 수 있고, .delete로 해당 내용을 지울 수 있다.

여기서 "1.0"이 뜻하는 건 1번째 라인에 0번쨰 column 위치를 뜻하고, END는 끝에서 가져온다는 뜻이다.

## checkbox

```python
from tkinter import *

root = Tk()
root.title("98tech-savvy")
root.geometry("640x480+100+300") #가로x세로+x좌표+y좌표 : 해상도 가로x세로 / 화면의 x좌표 y좌표에 뜸
root.resizable(False, False) #가로, 세로 크기 변경 불가

chkvar = IntVar() #chkvar에 int형으로 값을 저장함
chkbox1 = Checkbutton(root, text="오늘 하루 보지 않기", variable=chkvar)
chkbox1.select() #선택함
chkbox1.deselect() #선택을 해제함

chkbox1.pack()


def btncmd():
    print(chkvar.get())

btn1 = Button(root, text="클릭", command=btncmd)
btn1.pack()

root.mainloop() 
```

체크박스가 체크가 되었는지, 체크가 되지 않았는지는 ``variable=chkvar``라는 코드로 저장해주는데, 이 때 값을 저장해주기 위해 chkvar라는 변수를 IntVar()로 int형으로 값을 저장해준다.

.select는 체크박스를 체크하고
.deselect는 체크박스를 해제한다.

## listbox
listbox는 직원의 이름,급여 정보나 딸기, 사과같은 과일의 종류등을 표현할 때 적합한 위젯이다.

```python
from tkinter import *

root = Tk()
root.title("98tech-savvy")
root.geometry("640x480+100+300") #가로x세로+x좌표+y좌표 : 해상도 가로x세로 / 화면의 x좌표 y좌표에 뜸
root.resizable(False, False) #가로, 세로 크기 변경 불가

lstbox1 = Listbox(root, selectmode=SINGLE, height=0) #height의 개수만큼 리스트박스의 값을 보여줌(insert index값만큼)
lstbox1.insert(0, "사과")
lstbox1.insert(1, "배")
lstbox1.insert(2, "딸기")
lstbox1.pack()

def btncmd():
    # lstbox1.delete(0) #END는 맨 뒤를 삭제, 0은 맨 앞을 삭제 (index 값 위치 삭제)
    # print("리스트에는 {}개가 있어요.".format(lstbox1.size()))
    # print("{} ~ {} 리스트 : {}".format(lstbox1.get(0),lstbox1.get(2),lstbox1.get(0, 2)))
    print("선택된 항목 : {}".format(lstbox1.curselection())) #선택한 index값을 반환함

btn1 = Button(root, text="클릭", command=btncmd)
btn1.pack()
```

``
lstbox1 = Listbox(root, selectmode=SINGLE, height=0) #height의 개수만큼 리스트박스의 값을 보여줌(insert index값만큼)``

설명에 있다시피 height의 개수만큼 index를 보여주고, selectmode=SINGLE,EXTENDED 등으로 어떻게 선택할건지 고를 수 있다. SINGLE은 1개만 선택할 수 있고, EXTENDED는 여러개를 선택할 수 있다.

- 리스트박스변수.size로 리스트박스의 크기를(index의 크기) 구해올 수 있다.
- 부분을 구하고 싶다면 .get 함수를 사용하면 된다.
- 리스트박스변수.curselection으로 선택한 index값을 반환할 수도 있다.

## radiobutton
라디오 버튼은 체크박스와는 다르게 여러가지 중에 1개를 선택할 수 있는 버튼이다.

```python
from tkinter import *

root = Tk()
label1 = Label(root, text="메뉴를 선택하세요")

burger_var = IntVar()
btn_burger1 = Radiobutton(root, text="햄버거", value=1, variable=burger_var)
btn_burger2 = Radiobutton(root, text="치킨버거", value=2, variable=burger_var)
btn_burger3 = Radiobutton(root, text="치즈버거", value=3, variable=burger_var)

btn_burger1.pack()
btn_burger2.pack()
btn_burger3.pack()

root.mainloop()
```

![image](https://user-images.githubusercontent.com/128434645/234464953-5df6dc64-5ef8-4c22-95ea-729807ed3640.png)


value는 String형식으로 저장할 수도 있다. String형식으로 저장하므로 varibale=burger_var의 burger_var의 저장형식 또한 StringVar()로 저장해주어야하고,

burger_var.get으로 값을 얻어오면 라디오버튼에 선택한 값을 얻을 수 있다.

## combobox
생년월일을 입력할 때, ▽를 누르면 1900~2023까지 나오는 형식의 리스트를 본 적이 있을 것이다. 이것을 '콤보박스'라고 부르고 생년월일을 입력한다거나 어떤 값을 특정지어 선택할 때 사용한다.

콤보박스는 tkinter.ttk 안에 존재하므로 따로 import를 해주어야한다.

```python
import tkinter.ttk as ttk
from tkinter import *

root = Tk()

values = [str(i) + "일" for i in range(1, 32)]
cbbox1 = ttk.Combobox(root, height=5, values=values, state="readonly")
cbbox1.pack()

root.mainloop()

```

values에 for문으로 1일~31일까지로 값을 지정해주고 height로 콤보박스를 펼쳤을 때 보일 개수를 지정해주었다. .set으로 초기내용을 지정해줄 수도 있다. 또 state로 기본세팅을 해줄 수 있는데, readonly의 경우 "읽기 전용"으로 만든다는 뜻이다.

![image](https://user-images.githubusercontent.com/128434645/234465995-13e8a104-7783-4aed-8b6f-26a4a173bc75.png)


## progressbar
무언가를 다운로드받는다거나, 업데이트를 진행한다거나 등의 작업을 할 때 프로그램에서 '프로그레스 바'라는 녀석이 천천히 진행되거나 계속해서 반복하며 왔다갔다 하는 모습을 봤었을것이다. tkinter에는 progressbar라는 위젯으로 그 기능을 구현할 수 있다.

```python
import tkinter.ttk as ttk
from tkinter import *
import time

root = Tk()

p_var1 = DoubleVar()
pgbar1 = ttk.Progressbar(root, maximum=100, length=150, mode="determinate", variable=p_var1)
# 1 = 10ms
pgbar1.pack()


def btncmd():
    for i in range(1, 101):
        time.sleep(0.01)
        p_var1.set(i)
        pgbar1.update()


btn1 = Button(root, text="클릭", command=btncmd)
btn1.pack()

root.mainloop()
```

프로그레스바 또한 ttk로 만들어줄 수 있으며

maximum = 최대값 설정
length = 프로그레스바의 길이 설정
mode = determinate와 indeterminate가 있다.

determinate의 경우 왼쪽부터 올라가는 바
indeterminate의 경우 왼쪽 오른쪽을 번갈아가며 부딪히는 바

variable = 값을 저장할 변수, 이 곳에는 DoubleVar()를 저장해주는데 그 이유인즉슨 프로그레스바가 항상 정수형태로 올라가는게 아니기 때문에 실수형 변수로 저장해준다.

.update()로 프로그레스바의 진행 정도를 표시해줄 수 있으며
for문과 .set()으로 DoubleVar인 p_var1의 값을 세팅해주었다. 실행해보면 천천히 진행되는 프로그레스바를 볼 수 있다(time.sleep으로 약간의 딜레이도 주었음)
.stop 으로 프로그레스바를 정지시킬 수 있다.

## menu

![image](https://user-images.githubusercontent.com/128434645/234468011-de37d5f0-0613-4ecd-b4fd-ca15cf6efc71.png)

VSCode의 윗부분, 바로 '메뉴 부분'이다. tkinter로 이 메뉴창을 구현할 수 있다.

```python
import tkinter.ttk as ttk
from tkinter import *
import time

root = Tk()
root.geometry("640x480")
menu = Menu(root)

menu_file = Menu(menu, tearoff=0)
edit_file = Menu(menu, tearoff=0)


def create_new_file():
    print("새 파일을 만듬")


menu_file.add_command(label="New File", command=create_new_file)
menu_file.add_command(label="New Window")
menu_file.add_separator()
menu_file.add_command(label="Open File", state="disable")

edit_file.add_command(label="Undo")
edit_file.add_command(label="Cut")
edit_file.add_separator()
edit_file.add_command(label="Paste")

menu.add_cascade(label="File", menu=menu_file)
menu.add_cascade(label="Edit", menu=edit_file)

root.config(menu=menu)
root.mainloop()

```

![image](https://user-images.githubusercontent.com/128434645/234468774-a8840f70-6d9a-42c6-b80f-9e2b59ce8564.png)

쉽게 설명하자면 메뉴의 시작부분 File, Edit는 add_cascade로
메뉴의 하위메뉴는 add_command로 설정해준다.

tearoff=0 은 1로 설정해주면 위에 점선(--------)이 나타나는데, 눌렀을 때 하위 메뉴의 팝업창이 뜬다.
state 로 기본값 (ON/OFF)를 설정할 수 있고

체크박스나 라디오버튼등을 메뉴에 활용할 수 있다.

![image](https://user-images.githubusercontent.com/128434645/234469140-66658495-8020-4746-8678-64ba8b23f61c.png)

*라디오 버튼을 메뉴에 활용한 모습*

## Messagebox

```python
import tkinter.messagebox as msgbox
from tkinter import *

root = Tk()
root.geometry("640x480")


def info():
    msgbox.showinfo("알림", "정상적으로 실행됨")


def warn():
    msgbox.showwarning("경고", "프로그램 경고")


def err():
    msgbox.showerror("에러", "에러 뜸")


def okcancel():
    msgbox.askokcancel("확인/취소", "어쩌실래요")


def question():
    msgbox.askquestion("질문", "어쩌실래요")


def retrycancel():
    msgbox.askretrycancel("다시시도", "어쩌실래요")


Button(root, command=info, text="알림").pack()
Button(root, command=warn, text="경고").pack()
Button(root, command=err, text="에러").pack()

Button(root, command=okcancel, text="확인/취소").pack()
Button(root, command=question, text="예/아니요").pack()
Button(root, command=retrycancel, text="다시시도").pack()

root.mainloop()
```

메시지박스는 tkinter.messagebox라는 녀석을 import해주어야 한다.

msgbox에 .showerror, .showinfo, .askokcancel, .askquestion 등과 같은 여러가지 기능들은 목적에 따라 사용해주면 된다. 여기서 확인은 True, 취소는 False, 계속은 None등의 값으로 나오므로 값을 처리하고 싶을 때는
변수를 할당해주고 그 값에 따라 처리해주면된다.

예제

```python
def okcancel():
  response = msgbox.askokcancel("확인/취소", "눌러보세요")

  if response == 1:
    print("True")
  elif respone == 0:
    print("False")
```

------------------------

## frame

프레임은 위젯들을 구분해주기위한 공간을 만들어준다.

```python
import tkinter.messagebox as msgbox
from tkinter import *

root = Tk()
root.geometry("640x480")

frame1 = LabelFrame(root, text="숫자", relief="solid", bd=1)
frame1.pack(side=RIGHT, fill=BOTH, expand=True)

Button(frame1, text="1").pack()
Button(frame1, text="2").pack()
Button(frame1, text="3").pack()

frame1 = LabelFrame(root, text="문자", relief="solid", bd=1)
frame1.pack(side=LEFT, fill=BOTH, expand=True)

Button(frame1, text="A").pack()
Button(frame1, text="B").pack()
Button(frame1, text="C").pack()

root.mainloop()

```

Frame이나 LabelFrame같은 객체를 사용해주기 위한 변수를 선언하고, bd나 relief로 옵션을 지정해준다.
pack()안의 옵션들은 위치, 크기, 확장성 등의 옵션이다

## scrollbar

스크롤바는 리스트박스와 연계되어 자주 사용되는 위젯 중 하나이다.

```python
import tkinter.messagebox as msgbox
from tkinter import *

root = Tk()
root.geometry("640x480")

frame = Frame(root)
frame.pack()

scrollbar = Scrollbar(frame)
scrollbar.pack(side=RIGHT, fill=Y)

listbox = Listbox(frame, selectmode=EXTENDED, height=10, yscrollcommand=scrollbar.set)
for i in range(1, 32):
    listbox.insert(END, str(i) + "일")
listbox.pack()

scrollbar.config(command=listbox.yview)

root.mainloop()

```

하나의 프레임에 리스트박스와 스크롤바를 같이 넣어주고, 스크롤바를 보여줄 때 fill=Y로 설정해주면 스크롤바가 프레임에 맞게 꽉 맞춰서 나온다.

리스트박스에서 yscrollcommand=scroolbar.set과 scrollbar.config(command=listbox.yview)를 같이 해주지 않으면 스크롤바가 움직여도 다시 돌아오고 리스트박스와 반응이 없어지기 때문에 리스트박스와 같이 반응시켜주기위해 두 코드를 넣어주어야한다.

## 그리드
'격자'라는 뜻을 가지고있는데, 말 그대로 프로그램의 창이 있다고 했을 때

```
┌───┬───┬───┬───┐
│0,0│0,1│0,2│0,3│
│1,0│1,1│1,2│1,3│
│2,0│2,1│2,2│2,3│
│3,0│3,1│3,2│3,3│
└───┴───┴───┴───┘
```

의 순서대로 나눠져있다고 생각하면된다.

우리들이 사용했던 side=LEFT나 side=RIGHT 같은 코드들이 위 그리드를 사용해 나뉘어진다.
.grid의 옵션 row=num, column=num 으로 직접 저 격자의 위치에 넣어줄 수도 있다.
sticky=N+E+W+S 로 북동서남 방향으로 버튼같은 위젯들의 크기를 늘려줄 수 있다.

