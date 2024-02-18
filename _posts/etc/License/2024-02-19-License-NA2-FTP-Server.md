---
title:  "[네트워크 관리사 2급] 13. FTP Server"
excerpt: "FTP Server 에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, FTP Server]

toc: true
toc_sticky: true

date: 2024-02-19
last_modified_at: 2024-02-19
---

# FTP Server
윈도우 서버는 FTP서버를 구축해서 윈도우 서버로 파일을 올리거나 내려받을 수 있다. FTP서버는 IIS 관리자 프로그램에서 FTP 추가 메뉴를 사용해 구축해서 사용할 수 있다.

FTP 사이트 추가 >> FTP 사이트 이름, FTP 서버 디렉터리를 지정하고 특정 IP에 대해서만 접근이 가능하도록 하려면 IP 주소 바인딩 탭을 사용한다. FTP 서버는 21번 포트 번호를 사용하며 SSL을 사용해 암호화를 수행할 수 있다(인증기관으로부터 SSL 인증서를 받아야 가능함)

윈도우에서 FTP를 사용하려면 알FTP 같은 FTP 클라이언트 프로그램을 설치해서 FTP 서버에 접속할 수 있다.

리눅스에서는 FTP 프로그램을 실행해 사용자 ID와 패스워드를 입력하면 바로 로그인해 FTP서버를 사용할 수 있다(ftp IP).