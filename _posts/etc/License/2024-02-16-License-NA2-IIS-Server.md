---
title:  "[네트워크 관리사 2급] 10. IIS 서버"
excerpt: "IIS 서버에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, IIS 서버]

toc: true
toc_sticky: true

date: 2024-02-16
last_modified_at: 2024-02-16
---

# IIS 서버
IIS(Internet Information Server)는 웬 서버의 역할을 수행하는 마이크로소프트 사의 프로그램으로 ASP를 지원하며 .Net framework를 기반으로 개발되어있다.

> 웹 서버 : 웹 브라우저와 송수신을 하며 HTML 형식 문서를 송 수신하는 프로그램

웹 브라우저의 세션을 관리하는걸 웹 서버라고 하며 윈도우에는 IIS, 리눅스에는 Apache가 대표적인 웹 서버이다.

## IIS의 기능
1. HTTP Request에 대해 HTTP Response로 HTML을 전송함
2. HTTP 리디렉션 기능으로 특정 주소로 바로 연결되게 함(예를 들어 www.google.com 으로 입력해서 들어가면 www.google.com/?gws_rd=ssl식으로 접속하게 해주는 것)
3. HTTP 상태 코드를 통해 오류를 관리함
4. HTTP 로깅 정보를 기록하고 관리함
5. ASP, .NET 언어를 지원함
6. SSL 인증서를 등록해 SSL 보안을 지원함

HTTP 리디렉션, HTTP 응답헤더, ISAPI 및 CGI 지원, ISAPI 필터, MIME 형식 등의 기능 또한 지원한다.

### 가상 디렉터리
실제 페이지 경로를 보이지 않게 해서 보안을 향상시키는 기술이다. 즉, 실제로 존재하지는 않는 가상의 디렉터리에 웹 페이지나 파일 등을 올려놓고 관리하는 것을 말한다.