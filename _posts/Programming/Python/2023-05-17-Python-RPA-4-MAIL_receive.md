---
title:  "[Python] 업무자동화(RPA) 3-2편 - 메일 받기, 검색하기"
excerpt: "Python으로 회사의 반복적인 업무를 자동화 해보자. 파이썬으로 메일 받아보기, 파이썬으로 메일 검색해보기"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, 메일]

toc: true
toc_sticky: true

date: 2023-05-17
last_modified_at: 2023-05-17
---

이번에는 파이썬을 활용해 메일을 받아보고 활용해보자.

# 메일 받기
메일을 받기 위해서는 imap_tools 를 사용해주면 된다. imap_tools>MailBox를 임포트해준다.

```python
from imap_tools import MailBox
from mail_address import *

mailbox = MailBox("imap.gmail.com", 993)
mailbox.login(EMAIL_ADDRESS, EMAIL_PASSWORD, initial_folder="INBOX")  # INBOX : 받은편지함

for msg in mailbox.fetch(limit=10, reverse=True):  # limit = 제한숫자, reverse = 뒤집어서 가져옴(최신 순)
    print("제목 : ", msg.subject)
    print("발신자 : ", msg.from_)
    print("수신자 : ", msg.to)
    # 참조자 msg.cc 비밀참조자 msg.bcc
    print("날짜 : ", msg.date)
    print("본문 : ", msg.text)
    # print("HTML 메시지 : ", msg.html)
    print("=" * 55)

    # 첨부 파일 가져오기
    for att in msg.attachments:
        print("첨부파일 : ", att.filename)
        print("파일 타입 : ", att.content_type)
        print("파일 사이즈 : ", att.size)

        # 파일 다운로드
        with open("download_" + att.filename, "wb") as f:
            f.write(att.payload)
            print("첨부 파일 다운로드 완료 : ", att.filename)

mailbox.logout()

# https://pypi.org/project/imap-tools/

```

``mailbox.login(EMAIL_ADDRESS, EMAIL_PASSWORD, initial_folder="INBOX")  # INBOX : 받은편지함`` 이 부분의 INBOX는 메일의 '받은편지함'을 받아오겠다는 뜻이다.

``for msg in mailbox.fetch(limit=10, reverse=True):  # limit = 제한숫자, reverse = 뒤집어서 가져옴(최신 순)``  for문을 활용해 메일박스 모듈로 받은 메일들을 변수 msg에 배열로 저장하고, limit와 reverse 옵션을 추가해주었다.

만약 더 많은 imap-tools 기능을 보고 싶다면 [imap-tools](https://pypi.org/project/imap-tools/)를 참고하자.

# 메일 검색하기
메일을 받아올 때 특정 검색 조건을 만들어 줄 수 있다. 그러면 메일박스는 특정 검색 조건을 만족한 메일만을 가지고 와서 변수에 저장해준다.

```python
mailbox.fetch('UNSEEN') # 읽지 않은 메일 가져오기
mailbox.fetch('FROM 98tech.savvy@gmail.com') # 특정인이 보낸 메일 가져오기
mailbox.fetch('(TEXT "내용")') # 어떤 글자를 포함하는 메일(제목과 본문) 내용안에는 띄어쓰기로 구분하고 각각의 단어를 포함하는 메일을 찾음.
mailbox.fetch('(SUBJECT "내용")') # 어떤 글자를 포함하는 메일(제목)
한글의 경우는 아직 지원을 하지 않기 때문에 for 문 안에 특정 문자의 if문을 넣어줘서 찾아주면 된다.
mailbox.fetch('(SENTSINCE 날짜(00-MONTH-0000))') # 특정 날짜 이후에 온 메일
mailbox.fetch('(ON 날짜)') # 특정 날짜에 온 메일
```

``mailbox.fetch`` 부분에 위의 코드들을 넣어주면 된다. 만약 위의 코드들 외에 일정의 조건을 원한다면 fetch 아래에 if문을 넣어서 활용해주면 된다.