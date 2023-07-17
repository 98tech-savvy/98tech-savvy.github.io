---
title:  "tkinter로 윈도우 메모장 만들어보기"
excerpt: "tkinter의 기본은 전부 배웠으니 이제 tkinter를 활용해서 메모장을 만들어보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, tkinter, 윈도우 메모장]

toc: true
toc_sticky: true

date: 2023-04-27
last_modified_at: 2023-04-27
---

# 설계, 윈도우 메모장의 생김새
![image](https://user-images.githubusercontent.com/128434645/234473658-139683af-3d3f-479c-a22d-d73b833572a4.png)

나는 Notepad++를 사용하면서 기존의 윈도우 메모장이 필요없다고 생각해서 메모장을 파워쉘을 사용해서 지웠다. 그래서 구글링해서 위 사진을 보고 어느 블로그의 '윈도우10 기능 파헤치기'같은 포스팅을 보면서 프로그램을 만들기로했는데 크게 이 정도의 기능만 있으면 될 것 같다고 설계했다.

- 5개의 메뉴(파일, 편집, 서식, 보기, 도움말)
- 단축키로 메뉴 띄우기
- 파일의 이름과 프로그램 이름 타이틀에 띄우기
- 텍스트 박스와 스크롤 바

정도로 생각하고 코딩을 진행했다.

# 완성된 코드

```python
from tkinter import *
import tkinter.messagebox as msgbox
import tkinter.ttk as ttk
import tkinter.filedialog as fd
import tkinter.font as ttkft
import os
import pyperclip as cb
import pyautogui as pg
import webbrowser
from datetime import datetime

root = Tk()

WIDTH = 640
HEIGHT = 480

# - 파일의 이름과 프로그램 이름 타이틀에 띄우기
file_name = "제목없음"
note_name = "98tech-savvy"

NORMALPATH = "C:\\Users\\Seounb\\Desktop\\Workspace\\PythonWorkspace\\notepad\\"
ICOPATH = "C:\\Users\\Seounb\\Desktop\\Workspace\\PythonWorkspace\\notepad\\ico.ico"

root.geometry("{}x{}".format(WIDTH, HEIGHT))
root.title("{} - {}".format(file_name, note_name))
root.iconbitmap(ICOPATH)
font = ttkft.Font(
    root,
    family="맑은 고딕",
    size=10,
)
# - 5개의 메뉴(파일, 편집, 서식, 보기, 도움말)
menu = Menu(root)

file_menu = Menu(menu, tearoff=0)
edit_menu = Menu(menu, tearoff=0)
format_menu = Menu(menu, tearoff=0)
view_menu = Menu(menu, tearoff=0)
help_menu = Menu(menu, tearoff=0)

menu.add_cascade(label="파일(F)", menu=file_menu)
menu.add_cascade(label="편집(E)", menu=edit_menu)
menu.add_cascade(label="서식(O)", menu=format_menu)
menu.add_cascade(label="보기(V)", menu=view_menu)
menu.add_cascade(label="도움말", menu=help_menu)


###################################################################
open_file_wizard_idx = 0


def file_new(event=None):  # 새 파일 만들기
    # 새 파일 만들때 저장안한 내용 물어보는 코드 구현하기

    file_name = "제목없음"
    root.title("{} - 98tech Notepad".format(file_name))
    textbox.delete("1.0", END)


def file_open(event=None):  # 파일 열기
    textbox.delete("1.0", END)

    global file_name
    global open_file_wizard
    global open_file_wizard_idx

    open_file_wizard = fd.askopenfilename(
        initialdir=NORMALPATH,
        title="파일 열기",
        filetypes=(("텍스트 파일", "*.txt"), ("모든 파일", "*.*")),
    )

    open_file = open(open_file_wizard, "r", encoding="UTF-8")

    of = open_file.read()
    path_list = list(open_file_wizard)
    path_name = []
    for i in range(1, len(path_list)):  # 타이틀에 쓰기 위해 파일 이름을 구하는 코드
        if path_list[-i] == "/":
            break
        else:
            path_name.append(path_list[-i])
    path_name.reverse()

    file_name = "".join(path_name)

    root.title("{} - {}".format("".join(file_name), note_name))
    textbox.insert(END, of)
    open_file_wizard_idx = 1


def file_save(event=None):  # 파일 저장하기
    if open_file_wizard_idx == 1:
        save_file = open(file_name + ".txt", "w", encoding="UTF-8")
        save_file.write(textbox.get("1.0", END))
    else:
        file_another_name_save()


def file_another_name_save(event=None):  # 파일 다른이름으로 저장하기
    global open_file_wizard_idx

    save_file_wizard = fd.asksaveasfilename(
        initialdir=NORMALPATH,
        title="다른 이름으로 저장",
        initialfile=file_name,
        filetypes=(("텍스트 파일", ".txt"), ("모든 파일", "*")),
    )

    save_file = open(save_file_wizard + ".txt", "w", encoding="UTF-8")
    save_file.write(textbox.get("1.0", END))
    open_file_wizard_idx = 1


def file_page_set(event=None):  # 페이지 설정
    pass


def file_print(event=None):  # 프린트
    # win32api.ShellExecute(0, "프린트", open_file_wizard, None, ".", 0)
    pass


def file_exit(event=None):  # 끝내기
    root.quit()
    exit()


file_menu.add_command(label="새로 만들기(N)", command=file_new, accelerator="Alt+N")
file_menu.add_command(label="열기(O)...", command=file_open, accelerator="Alt+O")
file_menu.add_command(label="저장(S)", command=file_save, accelerator="Alt+S")
file_menu.add_command(label="다른 이름으로 저장(A)...", command=file_another_name_save, accelerator="Alt+A")
file_menu.add_separator()
file_menu.add_command(
    label="페이지 설정(U)...", command=file_page_set, state=DISABLED, accelerator="Alt+U"
)
file_menu.add_command(label="인쇄(P)", command=file_print, state=DISABLED, accelerator="Shift+P")
file_menu.add_separator()
file_menu.add_command(label="끝내기(X)", command=file_exit, accelerator="Alt+X")
###################################################################


def edit_undo(event=None):  # 되돌리기 기능
    textbox.edit_undo()


def edit_cut(event=None):  # 잘라내기 기능
    cb.copy(textbox.selection_get())
    textbox.delete(textbox.index(SEL_FIRST), textbox.index(SEL_LAST))


def edit_copy(event=None):  # 복사하기 기능
    cb.copy(textbox.selection_get())


def edit_paste(event=None):  # 붙여넣기 기능
    textbox.insert(textbox.index(INSERT), cb.paste())  # index로 INSERT(커서 위치값)을 받아내고 paste함


def edit_delete(event=None):  # 삭제하기 기능
    textbox.delete(textbox.index(SEL_FIRST), textbox.index(SEL_LAST))


def edit_find(event=None):  # 찾기 기능, 바꾸기 기능
    def cmd_find_text():  # 찾기 창 열기
        s = find_text.get()
        if s:
            idx = "1.0"
            while 1:
                idx = textbox.search(
                    find_text.get(), idx, nocase=1, stopindex=END
                )  # 대소문자 무시 nocase=1
                if not idx:
                    break

                lastidx = "%s+%dc" % (idx, len(s))
                textbox.tag_add("found", idx, lastidx)
                idx = lastidx

            textbox.tag_config("found", foreground="red")
        find_text.focus_set()

    def cmd_change_text():  # 바꾸기 창 열기
        s = find_text.get()
        if s:
            idx = "1.0"
            while 1:
                idx = textbox.search(
                    find_text.get(), idx, nocase=1, stopindex=END
                )  # 대소문자 무시 nocase=1
                if not idx:
                    break

                lastidx = "%s+%dc" % (idx, len(s))
                textbox.delete(idx, lastidx)
                textbox.insert(idx, change_text.get())
                idx = lastidx

        find_text.focus_set()

    find_windows = Toplevel(root)
    find_windows.title("찾기/바꾸기")
    find_windows.iconbitmap(ICOPATH)

    find_text = Entry(find_windows, width=45)
    find_label = Label(find_windows, text="찾을 값")
    find_button = Button(find_windows, height=1, text="찾기", command=cmd_find_text)
    find_label.grid(row=0, column=0, sticky=N + E + W + S)
    find_text.grid(row=0, column=1)
    find_button.grid(row=0, column=2, sticky=N + E + W + S)

    change_text = Entry(find_windows, width=45)
    change_label = Label(find_windows, text="바꿀 값")
    change_button = Button(find_windows, height=1, text="바꾸기", command=cmd_change_text)
    change_label.grid(row=1, column=0, sticky=N + E + W + S)
    change_text.grid(row=1, column=1)
    change_button.grid(row=1, column=2, sticky=N + E + W + S)


def edit_move(event=None):
    newWindow = Toplevel(root)
    newWindow.title("줄 번호 이동")
    newWindow.iconbitmap(ICOPATH)

    def move_text():
        textbox.yview_pickplace(int(text.get()) - 1)

    label = Label(newWindow, text="줄 번호 입력 : ")
    text = Entry(newWindow)
    button = Button(
        newWindow,
        text="이동",
        command=move_text,
    )

    label.grid(row=0, column=0)
    text.grid(row=0, column=1)
    button.grid(row=0, column=2)


def edit_all_select(event=None):
    textbox.tag_add(SEL, "1.0", END)


def edit_time_date(event=None):
    textbox.insert(INSERT, datetime.today().strftime("%Y/%m/%d-%H:%M:%S"))


edit_menu.add_command(label="실행 취소(U)", command=edit_undo, accelerator="Alt+U")
edit_menu.add_separator()
edit_menu.add_command(label="잘라내기(T)", command=edit_cut, accelerator="Alt+T")
edit_menu.add_command(label="복사(C)", command=edit_copy, accelerator="Alt+C")
edit_menu.add_command(label="붙여넣기(P)", command=edit_paste, accelerator="Alt+P")
edit_menu.add_command(label="삭제(L)", command=edit_delete, accelerator="Alt+L")
edit_menu.add_separator()
edit_menu.add_command(label="찾기/바꾸기(F)...", command=edit_find, accelerator="Alt+F")
edit_menu.add_command(label="이동(G)...", command=edit_move, accelerator="Alt+G")
edit_menu.add_separator()
edit_menu.add_command(label="모두 선택(A)", command=edit_all_select, accelerator="Ctrl+A")
edit_menu.add_command(label="시간/날짜(D)", command=edit_time_date, accelerator="Alt+D")
###################################################################


def format_auto_line_change(event=None):
    if auto_line_check_var.get() == 1:
        textbox.config(wrap="char")
    elif auto_line_check_var.get() == 0:
        textbox.config(wrap="none")


def format_font(event=None):
    font_window = Toplevel(root)
    font_window.title("글꼴 설정")
    font_window.iconbitmap(ICOPATH)

    lstfont1_label = Label(font_window, text="굵기 설정")
    lstfont1 = Listbox(font_window, selectmode=SINGLE, exportselection=False)
    lstfont1.insert(0, "보통")
    lstfont1.insert(1, "굵게")
    lstfont1.select_set(0)

    lstfont2_label = Label(font_window, text="기울임 설정")
    lstfont2 = Listbox(font_window, selectmode=SINGLE, exportselection=False)
    lstfont2.insert(0, "보통")
    lstfont2.insert(1, "기울임")
    lstfont2.select_set(0)

    lstfont3_label = Label(font_window, text="밑줄/취소선")
    lstfont3 = Listbox(font_window, selectmode=MULTIPLE, exportselection=False)
    lstfont3.insert(0, "밑줄")
    lstfont3.insert(1, "취소선")

    def apply_font(event=None):
        if int(lstfont1.curselection()[0]) == 1:
            font.config(weight="bold")
        else:
            font.config(weight="normal")

        if int(lstfont2.curselection()[0]) == 1:
            font.config(slant="italic")
        else:
            font.config(slant="roman")

        if int(lstfont3.curselection()[0]) == 0:
            font.config(underline=1)

        if int(lstfont3.curselection()[0]) == 1:
            font.config(overstrike=1)

        textbox.config(font=font)
        textbox.update()

    def cancel_font():
        font_window.destroy()

    apply_button = Button(font_window, text="적용", command=apply_font)
    cancel_button = Button(font_window, text="취소", command=cancel_font)
    lstfont1.grid(row=1, column=0)
    lstfont1_label.grid(row=0, column=0)
    lstfont2.grid(row=1, column=1)
    lstfont2_label.grid(row=0, column=1)
    lstfont3.grid(row=1, column=2)
    lstfont3_label.grid(row=0, column=2)
    apply_button.grid(row=2, column=0, sticky=N + E + W + S)
    cancel_button.grid(row=2, column=2, sticky=N + E + W + S)


auto_line_check_var = IntVar()
format_menu.add_checkbutton(
    label="자동 줄 바꿈(W)",
    command=format_auto_line_change,
    variable=auto_line_check_var,
    accelerator="Shift+N",
)
format_menu.add_command(label="글꼴(F)...", command=format_font, accelerator="Shift-W")


###################################################################


def view_status_display_line(event=None):
    if status_display_var.get() == 1:
        row, col = textbox.index(INSERT).split(".")
        status_display_label.config(text="row:{}, col:{}".format(row, col))
        root.after(100, view_status_display_line)
    else:
        status_display_label.config(text="")


status_display_var = IntVar()
view_menu.add_checkbutton(
    label="상태 표시줄(S)",
    command=view_status_display_line,
    variable=status_display_var,
    accelerator="Shift-F",
)
###################################################################


def help_link(event=None):
    webbrowser.open("https://98tech-savvy.github.io/python/Python-Tkinter-make-notepad/")


help_menu.add_command(label="도움말 보기", command=help_link, accelerator="Shift-S")
###################################################################

# - 단축키로 메뉴 띄우기
root.bind_all("<Alt-n>", file_new)
root.bind_all("<Alt-o>", file_open)
root.bind_all("<Alt-s>", file_save)
root.bind_all("<Alt-a>", file_another_name_save)
root.bind_all("<Alt-u>", file_page_set)
root.bind_all("<Shift-p>", file_print)
root.bind_all("<Alt-x>", file_exit)

root.bind_all("<Alt-u>", edit_undo)
root.bind_all("<Alt-t>", edit_cut)
root.bind_all("<Alt-c>", edit_copy)
root.bind_all("<Alt-p>", edit_paste)
root.bind_all("<Alt-l>", edit_delete)
root.bind_all("<Alt-f>", edit_find)
root.bind_all("<Alt-g>", edit_move)
root.bind_all("<Control-a>", edit_all_select)
root.bind_all("<Alt-d>", edit_time_date)

root.bind_all("<Shift-n>", format_auto_line_change)
root.bind_all("<Shift-w>", format_font)

root.bind_all("<Shift-f>", view_status_display_line)

root.bind_all("<Shift-s>", help_link)


# - 텍스트 박스와 스크롤 바
mainframe = Frame(root)
mainframe.pack()

yscrollbar = Scrollbar(mainframe)
xscrollbar = Scrollbar(mainframe, orient=HORIZONTAL)
textbox = Text(
    mainframe,
    wrap="none",
    width=WIDTH,
    height=HEIGHT,
    yscrollcommand=yscrollbar.set,
    xscrollcommand=xscrollbar.set,
    undo=True,
    font=font,
)
status_display_label = Label(mainframe, text="")
status_display_label.pack(side=BOTTOM, anchor="s")
yscrollbar.pack(side=RIGHT, fill=Y)
xscrollbar.pack(side=BOTTOM, fill=X)
textbox.pack()

# status_display_label.pack(anchor="se", padx=1, pady=1)

yscrollbar.config(command=textbox.yview)
xscrollbar.config(command=textbox.xview)

root.config(menu=menu)
root.mainloop()


```

# 만들면서 나온 에러

1. IntVar 변수의 반환값으로 PY_VAR0이 나옴.
해결 - .get() 으로 반환해줘야 불리언대수가 나옴.

2. tkinter의 bind 기능이 반응하지 않음.
bind의 커맨드를 입력할 때 '대문자'를 입력할 시 SHIFT를 동시에 입력해줘야함.

3. bind기능으로 단축키를 만들고 반응하지 않음.
인자를 너무 많이 주었다는 에러메시지를 출력했음. event=none인자를 주어서 해결.


# 정리

모듈의 기본 기능만을 공부한 채로 구글링과 함께 메모장 프로그램을 만들었다.
버그도 잡지 않은 채라 '완성된' 프로그램이라 하기는 뭐하지만, 만들어보니 뿌듯함이 일어오른다.

pyinstaller로 빌드해서 프로그램을 실행해보았다.

![image](https://user-images.githubusercontent.com/128434645/234729443-b715bc57-053a-4366-b7d3-4fbdaf5888a2.png)

꽤 윈도우 메모장처럼 보이는게 만족스럽지만 파일의 저장형식을 txt로 고정했고, 글꼴 자체를 바꾸는 코드를 넣어주지 않아서 기능은 떨어지는 편이다.