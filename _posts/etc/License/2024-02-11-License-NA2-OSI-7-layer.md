---
title:  "[네트워크 관리사 2급] 5. OSI 7 계층"
excerpt: "OSI 7 계층에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, OSI 7 계층, 프로토콜, HDLC]

toc: true
toc_sticky: true

date: 2024-02-11
last_modified_at: 2024-02-11
---

# OSI 7 계층

## 프로토콜(Protocol)
프로토콜은 통신망에서 통신을 원하는 양측 시스템에서 데이터를 주고받기 위해 **미리 약속된 운영상의 통신 규약**을 말한다. 즉, 데이터 통신 수행 규칙들의 집합을 말한다고 생각하면 된다.

프로토콜은 **구문(Syntax), 의미(Semantics), 순서(Timing)**으로 구성되며 각각 부호화, 개체 조정, 순서 제어 등을 담당한다.

송/수신간에 데이터를 전송하는 것에는 **비트 단위, 바이트 단위, 문자 단위** 전송 방법이 존재하며 각각 프로토콜은 다음과 같다.

|데이터 전송 방법|프로토콜|
|-|-|
|비트 단위|SDLC, HDLC|
|바이트 단위|DDCM|
|문자 단위|BSC|

## OSI 7 계층(Open System Interconnection)
ISO에서 제정한 표준안으로, 모든 데이터 통신 기준을 계층으로 분할하고 각 계층 간 필요한 프로토콜을 규정했다. 정보가 전달되는 프레임워크를 제공해 네트워크 형태 간 차이가 발생해도 데이터 통신을 지원하고, 계층 별로 정보 흐름을 최소화 해 각 계층의 독립성을 향상시켰다.

OSI 7 계층은 다음과 같다.

|계층|설명|PDU|
|-|-|-|
|7. 애플리케이션(Application) 계층|사용자들이 있는 계층, 하위 계층을 몰라도 네트워크를 사용할 수 있고 인터넷-HTTP, 파일 업/다운로드-FTP, 네트워크 모니터링-SNMP, 전자우편-SMTP등의 프로토콜이 존재함|메시지|
|6. 표현(Presentation) 계층|애플리케이션 계층에서 전송한 메시지에 대해 코드화를 수행하는 계층, 사전에 정해진 코드로 변환하고 메시지를 압축해 데이터량을 줄임. 암호화도 수행한다|메시지|
|5. 세션(Session) 계층|송수신 간 통신을 위해 동기화 신호를 주고받는 계층, 세션 연결을 하고 가상 연결을 제공함. 이 때 통신 방식인 단순, 반이중, 전이중 방식도 결정함|메시지|
|4. 전송(Transport) 계층|송수신 간 논리적 연결을 수행하는 계층, 종단 간 End to End 연결 관리, TCP, UDP프로토콜이 존재함|세그먼트|
|3. 네트워크(Network) 계층|수신자의 IP주소를 읽어 라우터가 경로를 설정하는 계층, 포워딩을 수행하며 IPv4, IPv6가 있음. 네트워크 에러 확인을 위한 ICMP 프로토콜을 사용함|패킷|
|2. 데이터 링크(Data Link) 계층|네트워크 계층에서 붙인 IP헤더의 주소를 읽어 MAC 주소를 구하는 계층, 흐름제어를 하며 에러를 탐지하고 교정(ARQ)하는 계층, 프레임 릴레이, HDLC등의 프로토콜이 있음|프레임|
|1. 물리(Physical) 계층|구한 MAC주소로 전기적 신호인 비트(Bit)로 데이터를 전송하는 계층, 전송 거리가 멀면 리피터라는 증폭기를 이용해 신호를 증폭시킴|비트|

*애플리케이션-게이트웨이, 네트워크-라우터, 데이터 링크-브릿지, 스위치, 물리-케이블, 리피터*

## 에러 제어
네트워크에 에러를 제어하기 위해 송수신 간 일정한 약속으로 확인해야함. 이 때 에러가 없는지 확인하는 것을 FEC(Forward Error Correction), 데이터를 수신 받지 못하면 재전송하는 것을 BEC(Backward Error Correction)이라고 함

1) 패리티 체크
하나의 비트로 코드의 에러를 검출, 데이터 내의 Set(1) 비트 수를 체크해 짝수, 홀수에 따라 코드를 그대로 두거나 1비트를 추가해 에러를 검출한다

2) 해밍코드
오류 발견 및 교정이 가능한 코드로 1비트의 에러 검출 및 교정을 한다

3) 체크섬(CRC)
Check Sum 이라는 비트를 전송해 Check Sum 비트로 수신자가 연산해 에러 여부를 확인한다. 주로 무선 LAN과 이더넷 프레임에서 사용함

### FEC
송신 측이 특정한 정보 비트와 함께 전송해 수신 측에서 이 정보 비트로 에러 발생 시 수정하는 방식을 말하며 재전송 요구가 없어 역 채널이 필요 없고 연속적인 데이터 전송이 가능하다는 장점이 있다. 하지만 잉여 비트들이 전송되므로 전송 효율은 감소되는편이다.

### BEC
수신 측이 에러 검출 후 송신 측에게 에러가 발생한 데이터 블록을 다시 요청하는 방식으로, ARQ(Auto Repeat reQuest)가 있으며 ARQ에도 Stop-and-Wait, Go-Back-N, Selective-repeat, Adaptive ARQ 등이 있다.

1) Stop-and-Wait
송신자가 데이터를 전송하고 수신응답이 오면 다음 데이터를 전송한다

2) Go-Back-N
수신자가 데이터를 수신 받지 못할 경우 마지막으로 수신 받은 데이터 이후의 모든 데이터를 재전송하는 방법으로 **TCP 프로토콜에서 사용**한다.

3) Selective repeat
수신자가 수신 받은 데이터 중 중간에 빠져 있는 것만 재전송하는 방식이다.