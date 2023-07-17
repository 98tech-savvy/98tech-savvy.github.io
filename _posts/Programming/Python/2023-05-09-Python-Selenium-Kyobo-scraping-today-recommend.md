---
title:  "셀레니움 교보문고 오늘의 추천 스크래핑하기"
excerpt: "교보문고 사이트의 '오늘의 추천'의 책 리스트를 스크래핑해서 엑셀 파일로 저장해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, 스크래핑, Scraper, Kyobo, today_recommend_scraper, Selenium]

toc: true
toc_sticky: true

date: 2023-05-09
last_modified_at: 2023-05-09
---

# 기능
교보문고 사이트의 '오늘의 추천'탭에 있는 책들을 자동으로 가져와 엑셀파일로 정리하는 프로그램을 만들자

# 완성된 코드
```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.edge.options import Options

import openpyxl as pyxl
import time

# 웹 드라이버 생성
edge_option = Options()
edge_option.add_experimental_option("excludeSwitches", ["enable-logging"])


driver = webdriver.ChromiumEdge(options=edge_option)

url = "https://product.kyobobook.co.kr/today-book#?page=1&per=20&sort=rec&year=2023&month=00"
driver.get(url)

time.sleep(4)

# 저장할 엑셀 파일 만들기
xlsx = pyxl.Workbook()

xlsx1 = xlsx.create_sheet("오늘의 선택 도서")

xlsx1["a1"] = "제목"
xlsx1["b1"] = "정가"
xlsx1["c1"] = "판매가"
xlsx1["d1"] = "할인율"
xlsx1["e1"] = "작가"
xlsx1["f1"] = "출판사"
xlsx1["g1"] = "출판일"
xlsx1["h1"] = "한줄평"

page_last_num = driver.find_element(By.CSS_SELECTOR, "[data-role='last']").text
print(f"[MAX_COUNT_PAGE : {page_last_num}]")
print("[PAGE_IS_NOW : 1]")

total_book_count = 0
for i in range(0, int(page_last_num)):
    # 책 정보 리스트로 가져오기
    books = driver.find_elements(By.CSS_SELECTOR, ".prod_item")
    book_count = len(books)
    print("[BOOK_COUNT : {}]".format(book_count))
    # 책 정보 프린트하기

    for idx, book in enumerate(books):
        book_name = book.find_element(
            By.CSS_SELECTOR,
            ".prod_name",
        ).text

        book_price = book.find_element(By.CSS_SELECTOR, ".prod_price > .price > .val").text + "원"
        book_price_normal = book.find_element(
            By.CSS_SELECTOR, ".prod_price > .price_normal > .val"
        ).text
        book_price_percent = book.find_element(By.CSS_SELECTOR, ".prod_price > .percent").text
        book_author = book.find_elements(By.CSS_SELECTOR, ".prod_author")[0].text.split(" · ")

        book_one_comment = book.find_element(By.CSS_SELECTOR, ".prod_introduction").text

        cal_xlsx_number = total_book_count + (idx + 2)
        print(cal_xlsx_number)
        xlsx1[f"a{cal_xlsx_number}"] = book_name
        xlsx1[f"b{cal_xlsx_number}"] = book_price
        xlsx1[f"c{cal_xlsx_number}"] = book_price_normal
        xlsx1[f"d{cal_xlsx_number}"] = book_price_percent
        xlsx1[f"e{cal_xlsx_number}"] = book_author[0]
        xlsx1[f"f{cal_xlsx_number}"] = book_author[1]
        xlsx1[f"g{cal_xlsx_number}"] = book_author[2]
        xlsx1[f"h{cal_xlsx_number}"] = book_one_comment
        xlsx1[f"i{cal_xlsx_number}"] = f"PAGE {i+1}"

    total_book_count += book_count
    print(total_book_count)
    if i + 1 < int(page_last_num):
        next_page = driver.find_element(By.CSS_SELECTOR, "#top_pagi > button.btn_page.next").click()
        print(f"[PAGE_IS_NOW :{i+2}]")

    time.sleep(2)


xlsx.save("kyobo_today_recommend.xlsx")
print("SAVE DONE")

driver.quit()
```

# 제작 도중 나온 에러
- 클릭하지 못하는 버튼을 클릭했을 때 프로그램이 종료됨
교보문고의 '다음 페이지 버튼'은 마지막 페이지에 도달했을 때 버튼의 클릭 기능이 사라지는데, 이 때 프로그램은 버튼이 눌리지 않는걸 에러로 종료시켜버린다.
<br>**page_last_num을 계산해주어서 해결**<br><br>

- 계산 오류<br>``car_xlsx_number = total_book_count + (idx + 2)``의 원래 코드는 ``car_xlsx_number = (i * int(book_count) + (idx + 2))`` 였는데 이 때 마지막페이지의 개수가 11개여서 엑셀 파일에 삽입할 때 중간에 삽입되버리는 버그가 생겼다.
<br>**total_book_count 변수를 따로 선언해주어서 해결**