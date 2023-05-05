---
title:  "[Python] tkinter로 이미지 합치기 프로그램 만들기"
excerpt: "tkinter의 기본은 전부 배웠으니 이제 tkinter를 활용해서 이미지를 합쳐서 하나의 이미지로 만들어주는 프로그램을 만들어보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, tkinter, image combine, 이미지 합치기, 이미지 합치는 방법]

toc: true
toc_sticky: true

date: 2023-05-05
last_modified_at: 2023-05-05
---

# 설계, 윈도우 메모장의 생김새
![image](https://user-images.githubusercontent.com/128434645/236360731-7178ec60-6bfa-45a1-8f44-e8eab67b97c5.png)

이미지를 합치는 프로그램의 완성 사진이다. 기능은 단순하게 이 정도가 있다

- 파일을 추가해서 리스트에 넣기
- 파일을 삭제하기
- 저장 경로 지정해주기
- 옵션 1 : 이미지 크기 조정하기
- 옵션 2 : 이미지 간격 조정하기
- 옵션 3 : FORMAT(PNG, JPG, BMP) 형식 지정하기
- 프로그레스 바 연동하기

이미지를 조정해주고 추가해주기 위해서 Pillow 모듈을 사용했다.

# 완성된 코드

```python
from tkinter import *
import tkinter.ttk as ttk
import tkinter.messagebox as msgbox
from tkinter import filedialog
from PIL import Image
import os

root = Tk()

PVERSION = "1.0"
PROGRAM_NAME = "IMAGE COMBINE PROGRAM - {}".format(PVERSION)
FIRST_SAVE_PATH = "C:/"

root.title("{}".format(PROGRAM_NAME))


def add_file():
    files = filedialog.askopenfilenames(
        title="IMAGE SELECT",
        filetypes=(("PNG", "*.png"), ("JPG", "*.jpg"), ("BMP", "*.bmp"), ("All file", "*.*")),
        initialdir="PythonWorkspace/game_basic",
    )

    # LIST_FILE
    for file in files:
        list_file.insert(END, file)


def del_file():
    for i in reversed(list_file.curselection()):
        list_file.delete(i)


def save_path():
    path = filedialog.askdirectory(title="SAVE PATH")
    print(path)
    if path == "":
        return

    txt_save_path.delete(0, END)
    txt_save_path.insert(0, path)


def start():
    try:
        print(
            "WIDTH = {}\nDISTANCE = {}\nFORMAT = {}\n\nSAVE PATH = {}\n".format(
                cbbox_width.get(), cbbox_distance.get(), cbbox_format.get(), txt_save_path.get()
            )
        )

        if list_file.size() == 0:  # IF EMPTY FILE LIST
            msgbox.showerror("NO FILE", "Please add file")
            return

        if len(txt_save_path.get()) == 0:  # IF EMPTY SAVE PATH
            msgbox.showerror("NO SAVE PATH", "Please specify path")
            return

        # IMAGE COMBINE
        img_combine()
        msgbox.showinfo("DONE")
    except Exception as err:
        msgbox.showerror("ERR", err)


def img_combine():
    images = [Image.open(x) for x in list_file.get(0, END)]  # FROM list_file SAVE images

    img_width = cbbox_width.get()
    image_sizes = []
    if img_width == "Keep size":
        img_width = -1
    else:
        img_width = int(img_width)

    if img_width > -1:
        image_sizes = [(int(img_width), int(img_width * x.size[1] / x.size[0])) for x in images]
    else:
        image_sizes = [(x.size[0], x.size[1]) for x in images]

    widths, heights = zip(*(image_sizes))

    total_distance = 0
    type_distance = 0

    if cbbox_distance.get() == "NONE":  # OPTION2 DISTANCE
        pass
    elif cbbox_distance.get() == "Narrow":
        for i in range(0, list_file.size()):
            total_distance += 20
            type_distance = 20
    elif cbbox_distance.get() == "Normal":
        for i in range(0, list_file.size()):
            total_distance += 40
            type_distance = 40
    elif cbbox_distance.get() == "Wide":
        for i in range(0, list_file.size()):
            total_distance += 80
            type_distance = 80

    print(list_file.size())
    print(type(list_file.size()))
    print("{} / {}".format(widths, heights))

    max_width, total_height = max(widths), sum(heights) + total_distance

    print("{} / {}".format(max_width, total_height))

    result_img = Image.new("RGB", (max_width, total_height), (255, 255, 255))
    y_offset = 0  # pos y location

    for idx, img in enumerate(images):
        if img_width > -1:
            img = img.resize(image_sizes[idx])

        result_img.paste(img, (0, y_offset))
        y_offset += img.size[1] + type_distance

        progress = (idx + 1) / len(images) * 100
        p_var.set(progress)
        progress_bar.update()

    save_combine_image_path = os.path.join(
        txt_save_path.get(), "combine_img.{}".format(cbbox_format.get().lower())
    )
    result_img.save(save_combine_image_path)


# FILE FRAME
file_frame = Frame(root)
file_frame.pack(fill=X, padx=5, pady=5)

btn_add_file = Button(file_frame, text="ADD FILE", padx=5, pady=5, width=12, command=add_file)
btn_add_file.pack(side="left")

btn_del_file = Button(file_frame, text="DELETE", padx=5, pady=5, width=12, command=del_file)
btn_del_file.pack(side="right")

# LIST FRAME
list_frame = Frame(root)
list_frame.pack(fill=BOTH, padx=5, pady=5)

scrollbar = Scrollbar(root)
scrollbar.pack(side=RIGHT, fill=Y)

list_file = Listbox(list_frame, selectmode=EXTENDED, height=15, yscrollcommand=scrollbar.set)
list_file.pack(side=LEFT, fill=BOTH, expand=True)
scrollbar.config(command=list_file.yview)

# SAVE PATH FRAME
path_frame = LabelFrame(root, text="SAVE PATH")
path_frame.pack(fill=X, padx=5, pady=5)

txt_save_path = Entry(path_frame)
txt_save_path.insert(END, FIRST_SAVE_PATH)

txt_save_path.pack(side=LEFT, fill=X, expand=True, padx=5, pady=5)

btn_save_path = Button(path_frame, text="Browse", width=10, command=save_path)
btn_save_path.pack(side=RIGHT, padx=5, pady=5)

# OPTION FRAME
option_frame = LabelFrame(root, text="OPTION")
option_frame.pack(fill=X, padx=5, pady=5)

lbl_width = Label(option_frame, text="WIDTH", width=8)
lbl_width.pack(side=LEFT, padx=5, pady=5)

cbbox_width_array = ["Keep size", "1024", "800", "640"]
cbbox_width = ttk.Combobox(option_frame, values=cbbox_width_array, state="readonly", width=10)
cbbox_width.current(0)
cbbox_width.pack(side=LEFT, padx=5, pady=5)

lbl_distance = Label(option_frame, text="DISTANCE", width=8)
lbl_distance.pack(side=LEFT, padx=5, pady=5)

cbbox_distance_array = ["NONE", "Narrow", "Normal", "Wide"]
cbbox_distance = ttk.Combobox(option_frame, values=cbbox_distance_array, state="readonly", width=10)
cbbox_distance.current(0)
cbbox_distance.pack(side=LEFT, padx=5, pady=5)

lbl_format = Label(option_frame, text="FORMAT", width=8)
lbl_format.pack(side=LEFT, padx=5, pady=5)

cbbox_format_array = ["PNG", "JPG", "BMP"]
cbbox_format = ttk.Combobox(option_frame, values=cbbox_format_array, state="readonly", width=10)
cbbox_format.current(0)
cbbox_format.pack(side=LEFT, padx=5, pady=5)

# PROGRESS BAR
progress_frame = LabelFrame(root, text="PROGRESS")
progress_frame.pack(fill=X, padx=5, pady=5)

p_var = DoubleVar()
progress_bar = ttk.Progressbar(progress_frame, maximum=100, variable=p_var)
progress_bar.pack(fill=X, padx=5, pady=5)

# RUN FRAME
run_frame = Frame(root)
run_frame.pack(fill=X, padx=5, pady=5)

btn_exit = Button(run_frame, text="EXIT", padx=5, pady=5, width=12, command=quit)
btn_exit.pack(side=RIGHT, padx=5, pady=5)

btn_start = Button(run_frame, text="START", padx=5, pady=5, width=12, command=start)
btn_start.pack(side=RIGHT, padx=5, pady=5)


root.resizable(False, False)
root.mainloop()


```

# 만들면서 나온 에러

1. 저장경로를 지정해주지 않았을 때

2. 저장경로의 permission denied
1, 2는 동시에 try ~ exception 구문을 추가해줘서 에러 메시지를 표시해주는걸로 해결했다.

3. range 안 씀
리스트파일을 for문에서 활용할 때 range()안에 넣지않고 쓰는 바람에 TypeError가 나왔다. range를 써서 해결함. 


# 정리

파이썬의 있던 모듈들을 활용해서 이렇게 간단한 프로그램들을 여럿 만들 수 있다. 난이도도 어렵지 않아서 쉽게 프로그램을 완성했다.