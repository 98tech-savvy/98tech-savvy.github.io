---
title:  "[네트워크 관리사 2급] 7. 응용 프로토콜"
excerpt: "응용 프로토콜에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, 응용 프로토콜]

toc: true
toc_sticky: true

date: 2024-02-13
last_modified_at: 2024-02-13
---

# 응용 프로토콜

## Telnet
Telnet의 기본 사용 포트 : **23번 포트**

원격으로 서버에 로그인 해 작업할 때 많이 사용하는 프로그램. SSH가 있기 때문에 자주 사용하는 프로그램은 아니며 **TCP 프로토콜**을 사용한다

## SSH
SSH의 기본 사용 포트 : **22번 포트**

Telnet은 암호화 되지 않는 평문으로 데이터를 전송하기 때문에 보안에 굉장히 취약하다. 그래서 Telnet을 사용하지 않고 데이터를 암호화해주는 SSH를 많이 사용한다.

## HTTP
HTTP의 기본 사용 포트 : **80번 포트**

우리가 기본적으로 사용하는 W3C 표준 프로토콜인 HTTP이다. 웹 브라우저와 웹 서버 사이에 메시지를 송수신 하는 프로토콜로 **TCP**를 사용하며 **State-less(요청이 있을 때 연결하고 처리한 후 연결을 종료함) 방식**을 사용한다.

|요청 방식|내용|
|-|-|
|GET|데이터의 양이 제한, URL 파라미터로 요청함 (ex. Get login.php?id=1234*pw=3414)|
|POST|데이터의 양이 제한되어 있지 않음, HTTP Body에 넣어서 전송함|

## FTP
FTP의 기본 사용 포트 : **21번 포트**

서버에 파일을 올리거나 다운로드할 때 쓰는 인터넷 표준 프로토콜이다. **TCP 프로토콜**을 사용한다. FTP는 **포트를 2개 사용**한다. 하나는 명령 포트(주로 21번), 나머지 하나는 업/다운로드를 위한 데이터 포트이다.

|종류|설명|
|-|-|
|FTP|TCP 프로토콜 송수신|
|TFTP|UDP 프로토콜 송수신, 인증x, 69번 포트|
|SFTP|암호화 사용, 기밀성|

## DNS(Domain Name Service)
DNS는 Domain Name Service로 컴퓨터의 이름을 IP 주소로 변환하거나 해석하는 분산 네이밍 시스템이다. 예를 들어 www.naver.com 이라는 URL 주소를 IP주소로 변환시켜준다.

#### DNS가 해석하는 과정
1) DNS Cache Table에 요청함
2) DNS Cache Table에 없으면 hosts 파일을 사용해 해석함
3) hosts 파일에도 없으면 DNS 서버에 이름 해석을 의뢰하고 이것을 **순환 쿼리(Recursive Query)**라고함.
4) 만약 DNS가 이름을 해석할 수 없다면 Top level 도메인(com, org, kr) 부터 Second level(naver, google, github)로 이름 해석을 의뢰함. 이것을 **반복 쿼리(Iterative Query)**라고 함

#### DNS 레코드 종류
|종류|설명|
|-|-|
|A|각각의 동일한 IP주소에 해당되는 여러 개의 호스트 이름을 IPv4 주소로 매핑함|
|AAAA|호스트 이름을 IPv6 주소로 매핑함|
|PTR(Pointer)|역방향 조회 때 사용|
|NS(Name Server)|DNS 서버를 가리킴|
|MX(Mail Exchanger)|도메인 이름으로 보낸 메일을 받도록 구성되는 호스트 목록을 지정함|
|CNAME(Canonical Name)|호스트의 다른 이름을 정의|
|SOA(Start of Authority)|도메인에 가장 큰 권한을 부여 받은 호스트 선언|
|Any(ALL)|위의 모든 레코드 표시|

## SMTP(Simple Mail Transfer Protocol)
SMTP의 기본 사용 포트 : **587번, 25번 포트**

RFC 821에 명시되어있음, **Store-and-Forward** 방식을 사용함 전자 우편을 보내는 프로토콜로 최단 경로를 찾아 수신자에게 근접한 메일 서버에 편지를 전달함

#### SMTP 구성요소

|구성 요소|내용|
|-|-|
|MTA(Mail Transfer Agent)|메일 전송 서버|
|MDA(Mail Delivery Agent)|우체부 역할, MTA에게 받은 메일을 사용자에게 전달|
|MUA(Mail User Agent)|사용자들이 사용하는 어플리케이션|

#### POP3, IMAP
POP3의 기본 사용 포트 : **110번 포트**
IMAP의 기본 사용 포트 : **143번 포트**

POP3 : 메시지를 읽으면 서버에서 메일을 삭제
IMAP : 메시지를 읽어도 서버에서 메일을 저장해둠

## SNMP(Simple Network Management Protocol)
SNMP의 기본 사용 포트 : **UDP 161번 포트**

네트워크를 수집 및 분석하는 네트워크 관리 시스템임. NMS라는 SNMP 프로토콜을 사용해 네트워크 정보를 수집한다.

## DHCP(Dynamic Host Configuration Protocol)
DHCP의 기본 사용 포트 : **서버 67번, 클라이언트 68번 포트**

**IP주소를 동적으로 할당하는 프로토콜**이다. DHCP 서버에서 관리하는 주소 목록에 접속한 컴퓨터 시스템에 IP 주소를 할당한다.