---
title:  "[Python] 업무자동화(RPA) 3-1편 - 메일 보내기"
excerpt: "Python으로 회사의 반복적인 업무를 자동화 해보자. 파이썬으로 메일 보내보기"

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, 메일]

toc: true
toc_sticky: true

date: 2023-05-16
last_modified_at: 2023-05-16
---

SMTP 모듈을 사용해 메일을 보내고 IMAP_TOOLS 모듈을 사용해 메일을 받을 수 있다.

# 메일 보내기

SMTP 모듈을 임포트 해주고 자신의 이메일 계정과 비밀번호(앱 비밀번호)를 변수에 할당해주자. 만약 앱 비밀번호가 없다면 보안 탭에서 앱 비밀번호를 만들어서 설정해주자(구글 기준)

```python
import smtplib

EMAIL_ADDRESS = "이메일 주소"
EMAIL_PASSWORD = "앱 비밀번호"

with smtplib.SMTP("smtp.gmail.com", 587) as smtp:
    smtp.ehlo()  # SMTP 서버에 연결 제대로 됐는지 확인
    smtp.starttls()  # 모든 내용 암호화 전송
    smtp.login(EMAIL_ADDRESS, EMAIL_PASSWORD)  # 로그인

    subject = "TEST MAIL"
    body = "TEST BODY"

    msg = f"Subject: {subject}\n{body}"
    smtp.sendmail(EMAIL_ADDRESS, EMAIL_ADDRESS, msg)
```

ehlo() : SMTP 서버에 연결이 제대로 되었는지 확인한다.
starttls() : 모든 내용을 암호화해서 전송한다
login(EMAIL_ADDRESS, EMAIL_PASSWORD) : 해당 구글 계정에 로그인한다.

위의 3가지는 기본적으로 수행하는 것이라고 보면 된다.

subject 는 제목, body는 본문이다. 그리고 msg 변수에 위와 같이 만들어주고

``smtp.sendmail((EMAIL_FROM, EMAIL_TO), msg)``로 이메일을 보내주자.

**하지만 이 방법은 한글을 지원하지 않기 때문에 만약 Subject나 Body를 한글로 바꿔서 보낸다면 에러를 발생한다. 만약 한글로 보내고 싶다면**

# 한글 메시지 보내기

```python
import smtplib
from mail_address import *
from email.message import EmailMessage

msg = EmailMessage()

msg["Subject"] = "테스트 메일"  # 제목
msg["From"] = EMAIL_ADDRESS  # 보내는 사람
msg["To"] = EMAIL_ADDRESS  # 받는 사람

msg["To"] = "EMAIL_ADDRESS_1, EMAIL_ADDRESS_2, ..."

to_list = ["EMAIL_ADDRESS_1", "EMAIL_ADDRESS_2", ...]
msg["To"] = ", ".join(to_list) # .join 함수를 활용해서 to_list 배열의 사이 사이에 ", "를 넣어줘서 위의 것과 똑같이 만듬

msg["Cc"] = "EMAIL" # 참조
msg["Bcc"] = "EMAIL" # 비밀 참조

msg.set_content("테스트 메일입니다. \n 두 줄짜리 메일 테스트")  # 본문

with smtplib.SMTP("smtp.gmail.com", 587) as smtp:
    smtp.ehlo()
    smtp.starttls()
    smtp.login(EMAIL_ADDRESS, EMAIL_PASSWORD)

    smtp.send_message(msg)
```

``from email.message import EmailMessage``를 해줘서 email.message를 임포트해준다.

msg = EmailMessage() 로 이메일메세지 객체를 설정해주고

msg[""] = 로 원하는 곳(제목, 본문 등)에 데이터를 넣을 수 있다.
Subject = 제목
From = EMAIL_FROM # 보내는 사람
To = EMAIL_TO # 받는 사람

``msg.set_content("내용")`` 으로 본문을 설정해주고

``smtp.send_message(msg)``로 메시지를 송신해보자.

# 파일 송신하기

파일을 보내고 싶다면

```python
# msg.add_attachment()
with open("student.xlsx", "rb") as f:
    msg.add_attachment(
        f.read(), maintype="application", subtype="xls", filename=f.name
    )  # maintype subtype filename 보통 세 가지를 정해줌.

# MIME TYPE(미디어 타입) : 보내는 파일의 파일 형태를 알려줌 위의 경우에 image/png
# https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

with smtplib.SMTP("smtp.gmail.com", 587) as smtp:
    smtp.ehlo()
    smtp.starttls()
    smtp.login(EMAIL_ADDRESS, EMAIL_PASSWORD)

    smtp.send_message(msg)
```

만약 더 많은 MIME TYPE을 보고싶다면 [MIME TYPE](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types
) 을 참고하자.

보통 보내는 파일의 [메인 타입, 서브 타입, 파일 이름]을 지정해준다. 이 때 mime type을 사용하는데 보내는 파일의 종류에 따라 다르다.
