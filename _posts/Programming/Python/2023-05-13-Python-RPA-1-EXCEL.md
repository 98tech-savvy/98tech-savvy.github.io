---
title:  "업무자동화(RPA) 1편 - 엑셀"
excerpt: "Python으로 회사의 반복적인 업무를 자동화 해보자. 엑셀 자동화하기"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, 엑셀]

toc: true
toc_sticky: true

date: 2023-05-13
last_modified_at: 2023-05-13
---

# openpyxl
openpyxl은 파이썬에서 엑셀의 데이터를 변경할 수 있게 해주는 모듈이다.

터미널에 ``pip install openpyxl``로 설치가 가능하며 [OpenPyXL readthedocs](https://openpyxl.readthedocs.io/en/stable/) 사이트에서 모듈의 설명을 볼 수 있다.

# 학생들의 데이터 받아서 엑셀로 저장하기

대학의 교수가 필요할법한 프로그램으로, 학생들의 성적 데이터를 받아서 총합을 내고 성적을 나눠주는 프로그램을 만들어보자.

학생들의 데이터:

```
학번, 출석, 퀴즈1, 퀴즈2, 중간고사, 기말고사, 프로젝트
1,10,8,5,14,26,12
2,7,3,7,15,24,18
3,9,5,8,8,12,4
4,7,8,7,17,21,18
5,7,8,7,16,25,15
6,3,5,8,8,17,0
7,4,9,10,16,27,18
8,6,6,6,15,19,17
9,10,10,9,19,30,19
10,9,8,8,20,25,20
```

해야하는 일:
- 학생들의 데이터를 받아 엑셀에 삽입하기
- 학생들의 데이터에 총점을 계산하기
- 계산한 총점으로 성적을 나누기
- 출결점수가 좋지 않은 학생은 F학점

# 완성된 코드

```python
from openpyxl import Workbook
from openpyxl import load_workbook

wb = Workbook()  # 엑셀 워크북 생성
ws = wb.active
ws.title = "Student_"  # 현재 활성화 된 시트(sheet)를 가져옴

# 데이터 (학번/출석/퀴즈1/퀴즈2/중간고사/기말고사/프로젝트)
student_data = [
    (1, 10, 8, 5, 14, 26, 12),
    (2, 7, 3, 7, 15, 24, 18),
    (3, 9, 5, 8, 8, 12, 4),
    (4, 7, 8, 7, 17, 21, 18),
    (5, 7, 8, 7, 16, 25, 15),
    (6, 3, 5, 8, 8, 17, 0),
    (7, 4, 9, 10, 16, 27, 18),
    (8, 6, 6, 6, 15, 19, 17),
    (9, 10, 10, 9, 19, 30, 19),
    (10, 9, 8, 8, 20, 25, 20),
]

ws.append(("학번", "출석", "퀴즈1", "퀴즈2", "중간고사", "기말고사", "프로젝트", "총점", "성적"))

for idx, i in enumerate(student_data):
    ws.append(i)  # 데이터 엑셀에 집어넣기
    ws.cell(row=idx + 2, column=4).value = 10  # 퀴즈2 10점으로 수정
    ws.cell(row=idx + 2, column=8).value = f"=SUM(B{idx+2}:G{idx+2})"  # 총점 계산

    sum_val = sum(i[1:]) - i[3] + 10  # 성적계산용 총점
    print("총점 : {}".format(sum(i[2:])))
    print("퀴즈2 : {}".format(i[3]))
    print("성적용 총점 : {}".format(sum_val))
    print()
    if sum_val >= 90:  # 성적 나누기
        ws.cell(row=idx + 2, column=9).value = "A"
    elif sum_val >= 80:
        ws.cell(row=idx + 2, column=9).value = "B"
    elif sum_val >= 70:
        ws.cell(row=idx + 2, column=9).value = "C"
    else:
        ws.cell(row=idx + 2, column=9).value = "D"

    if int(i[1]) < 5:
        ws.cell(row=idx + 2, column=9).value = "F"

wb.save("student.xlsx")
wb.close()
```

이렇게 엑셀파일에 성공적으로 학생들의 데이터를 저장했다. 다음 포스팅에서 엑셀과 ppt를 사용해 카드에 저장하는 식으로 구현해보겠다.