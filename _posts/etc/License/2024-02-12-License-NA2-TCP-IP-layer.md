---
title:  "[네트워크 관리사 2급] 6. TCP/IP 계층"
excerpt: "TCP/IP 계층에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, TCP/IP, 프로토콜]

toc: true
toc_sticky: true

date: 2024-02-12
last_modified_at: 2024-02-12
---

# TCP/IP 계층
미국 ARPANET에서 개발한 프로토콜로 OSI보다 먼저 만들어지고 가장 많이 사용되고 있는 프로토콜 계층이다. OSI 7 Layer와 매우 흡사한 모양을 가지고 있다.

## TCP/IP 4계층

1) 애플리케이션(Application) 계층
FTP, Telnet, SSH, HTTP, SMTP, SNMP등의 프로토콜이 있는 계층으로 사용자들이 사용하는 프로그램이 있는 계층이다.

2) 전송(Transport) 계층
메시지를 전송하는 TCP, UDP 프로토콜이 있는 계층이다.

3) 인터넷(Internet) 계층
라우팅을 실행하고 최단 경로를 설정한다. 논리적 주소인 IP 주소를 부여하고, IP 주소를 MAC주소로 변환하는 ARP 프로토콜을 지원하는 계층이다. 네트워크 에러 검사의 ICMP 프로토콜 또한 지원한다.

4) 네트워크 접근(Network Access) 계층
물리적 케이블, 무선 통신으로 연결하고 메시지를 전송하는 계층이다.

TCP/IP 계층은 OSI 7 계층을 그대로 준수하고 있는 모습을 볼 수 있다.

|OSI 7 Layer|TCP/IP 4 Layer|
|-|-|
|Application|Application|
|Presentation|Application|
|Session|Application|
|Transport|Transport|
|Network|Internet|
|Data Link|Network Access|
|Physical|Network Access|

> TCP/IP 프로토콜은 TCP, UDP, ARP, RARP, ICMP, IP 로 구성된다.

### 전송(Transport) 계층

#### 세그먼트(Segment)
세그먼트는 전송 계층에서 TCP/UDP를 사용할 때 해당 헤더(Header)에 메시지를 붙이는 것을 의미한다.

#### 세그먼트의 TCP와 UDP
TCP Header는 UDP에 비해 크기가 크다(TCP는 여러 보안 잡다구리한게 담겨있음) TCP는 전송한 메시지를 수신측에서 ACK를 되돌려서 수신 여부를 확인시키는데, 동일한 ACK 번호를 반복적으로 수신측에서 전송한다면 어떤 이유로든 데이터를 받지 못하는 것이고 이 때 에러 제어 기법을 통해 재전송을 수행한다. 이 때 GO-Back-N 방법을 사용한다(되돌아온 ACK 이후의 모든 것을 전부 재전송) 또 동일 ACK 번호가 계속 되돌아오면 송신자는 전송 속도를 낮추는데 이걸 **혼잡 제어**라고 한다.

> TCP는 Sequence 번호를 통해 순서를 파악한다

> Check Sum은 TCP/UDP 둘 다 존재하는데 송신 중 메시지 변조를 파악하기 위해 송수신 간 에러를 체크하기 위한 방법이다

> TCP의 주요기능 : 신뢰성 있는 전송, 순서 제어, 전이중, 흐름 제어, 혼잡 제어

그에 반해 UDP는 데이터를 빠르게 전송하는 용도로 사용하며 TCP에 비해 기능은 없으나 데이터를 빠르게 송수신 할 수 있는 장점이 있다. 재전송 기능이 없어 패킷 손실 위험이 있다.
**비연결성, 비신뢰성**의 특성을 가지는 프로토콜로 송수신의 여부에 대한 책임을 Application이 가진다.

### 인터넷(Internet) 계층
인터넷 계층은 송수신의 IP 주소를 읽어 경로를 결정하고 전송하는 역할을 수행한다. 다중 네트워크 링크를 통해 패킷의 발신지-대-목적지 전달에 대한 책임을 가진다(데이터 링크 계층은 노드 간 책임, Point to Point)

인터넷 계층은 IP, ICMP의 TCP/IP 프로토콜 군이 존재하며 멀티캐스팅의 IGMP, 라우팅의 BGP, OSPF, RIP등이 존재한다.

라우터 라는 장비를 통해 최적의 경로를 설정한다.

#### 데이터그램(Datagram)
데이터그램은 기존 패킷에 IP Header를 붙이는 것을 의미한다.

##### IP Header 구조
IP Header에는 Flag와 Fragment Offset이라는게 있는데, 패킷의 크기가 너무 크면 패킷이 분할전송된다. 이 때 수신자의 재 조립을 위해 패킷의 순서에 관한 정보를 담아놓은 것이다.

TTL(Time to Live)은 라우터를 통과할 때마다 -카운트를 하며 0이 되면 패킷은 자동으로 폐기 된다. 무한정으로 인터넷에서 떠도는 패킷을 막기 위해 만들어졌다.

Protocol 은 IP Header 위의 상위 프로토콜의 종류를 의미한다(TCP인지 UDP인지)

Header Checksum은 헤더의 무결성을 검사하기 위한 것이다.

### 네트워크 접근 계층(Network Access) 계층
LAN 카드의 물리적인 주소인 MAC 주소를 가지고 전기적인 비트 신호로 메시지를 전송하는 계층이다. **프레임 단위, MAC 주소, 레이어**를 사용하는 계층이다.