---
title:  "API란?"
excerpt: "API에 대해 알아보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Computer
tags:
  - [Computer, 프로그래밍, API, 네트워크, 브라우저, URL]

toc: true
toc_sticky: true

date: 2023-07-01
last_modified_at: 2023-07-01
---

스크래핑 프로그램을 만들어보면 동적인 웹 페이지에서 속도가 매우 느려지고, 데이터가 많아지면 많아질수록 에러가 생기기 쉽고 좀 더 나은 대응방안이 없나 생각해본다. 사실 사이트에서 제공하는 API가 있다면, 굳이 스크래핑 프로그램을 만들지 않아도 API가 제공하는 여러가지 데이터를 가져올 수 있다.

# API

**API<sup>Apllication Programming Interface</sup>** 란 이종 시스템 간에 응용 프로그래밍이 가능하도록 정의된 명세를 말한다. 이전에는 Win32, OpenGL 처럼 전문적인 프로그래밍에서 사용했지만 최근에 HTTP를 만나 인터넷에서 브라우저를 통해 API를 사용할 수 있게 됐다. 현재는 웹 어플리케이션 개발에서 API를 사용한다(특정 정보를 제공할 목적으로)

# 데이터와 정보의 차이점

데이터란 날 것 그대로를 말한다. 고객이 구매한 내역, 환불한 내역, 결제한 금액 등을 말하고
정보란 가공되어서 나온 데이터, 6월 액세서리 구매자 등등

정보는 데이터보다 **추상화된 개념**이라고 할 수 있다.

# 네트워크
네트워크<sup>Network</sup>란 물리적으로 떨어져 있는 Peer(계층적 구조의 프로토콜을 사용하는 통신망의 동일 프로토콜 계층에서 대등한 지위로 동작하는 기능 단위 또는 장치, 쉽게 말해서 장치) 간의 연결 기술을 말한다.

1. Server-based
중앙 서버를 통해 Peer 간 연결

2. P2P-Network
Peer와 Peer끼리(Peer to Peer) 그물망식으로 연결

네트워크는 패킷을 통해 통신하는데, 패킷이란 데이터를 잘게 쪼개서 빨리 도착하도록 풀어주는 것을 의미한다. 송신지점에서 데이터를 분리해서 보내면(패킷) 수신지점에서 재조립이 이루어지는데, 이것이 **TCP/IP**의 기본 동작 원리이다.

# 인터넷 브라우저의 역할
인터넷 브라우저는 HTML/CSS 파일을 해석하고, Javascript파일을 해석하고, UI 렌더링 엔진을 실행하고, HTTP 클라이언트를 통해 여러가지 데이터를 수신한다.

# URL 해석
임의의 주소를 예로 들어보겠다.

```
http://thisishost.com:8080/kor/tutorial/profile?name=jen%40thistishost&t_type=native
```

1. 프로토콜 http://
어떻게 통신할 것인지를 이야기하는 곳이다. 예를 들어 http, https, ftp, smtp등이 있다.

2. 호스트 thisishost.com
접속해야 하는 대상, 현재는 도메인(thisishost.com)으로 되어있으며 도메인이 지정되어 있지 않다면 IP주소(192.168.0.1 같은)로 되어있을 것이다.

3. 포트 :8080
접속해야 하는 호스트의 포트, 프로토콜을 입력하면 자동으로 브라우저가 포트를 매핑해주기 때문에 프로토콜을 알면 자동으로 포트를 알 수 있다.

4. 경로 /kor/tutorial/profile
접속된 서버에 위치한 파일의 경로, 파일탐색기에서 Desktop/새폴더 와 같다.

5. 쿼리스트링(Query String) ?name=jen%40thistishost&t_type=native
이 부분이 중요한데, **API의 입력부분**이다. **key=value**의 형태로 이루어져있으며 위의 주소에 name=jen 이 위와 같다.

# Rest API 
Rest API<sup>Representational State Transfer API</sup> 란 HTTP프로토콜의 Method(POST, GET, PUT 등)를 활용해 웹서비스에 CRUD(Create, Read, Update, Delete) 서비스를 요청하는 것을 말한다.

## POST
해당 URL을 요청하면 리소스를 생성한다

## GET
해당 리소스를 조회한다. 해당 도큐먼트(문서)의 정보를 가져옴

## PUT
해당 리소스를 수정

## DELETE
해당 리소스를 삭제한다.