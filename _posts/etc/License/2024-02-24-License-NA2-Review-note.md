---
title:  "[네트워크 관리사 2급] 오답 노트"
excerpt: "문제를 풀며 헷갈리는 부분을 정리해보았다."

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급]

toc: true
toc_sticky: true

date: 2024-02-24
last_modified_at: 2024-02-24
---

# 시험보기 전 보면 좋은 것
1. OSI 7계층 물데네전세표에
물리, 데이터링크, 네트워크, 전송, 세션, 표현, 에플리케이션

2. OSI 7계층 단위 비프패세메메메
비트, 프레임, 패킷, 세그먼트, 메시지, 메시지, 메시지

3. 계층 별 프로토콜
- 응용 계층 : SMTP, SNMP, TFTP, FTP, SSH, TELNET, HTTP
- 네트워크 계층 : IP, ICMP, IGMP, ARP, RARP
- 전송 계층 : TCP, UDP

4. 서브넷 마스크 계산
ex) 4 ~ 5대 PC가 필요하다고 할 때 네트워크 1, 브로드 캐스트 1 해서 총 최대 5+1+1 = 7이 필요하다. 그러면 호스트의 갯수는 총 $2^3$, 8이 필요하며(더 커야하므로) 지수만큼 채워주면 C클래스라고 할 때 11111111.11111111.**111**00000.00000000 이다. 이걸 10진수로 바꿔주면 255.255.224.0 이 된다.

5. 사설 IP(내부 IP) 범위
- A 10.0.0.0 ~ 10.255.255.255
- B 172.16.0.0 ~ 172.31.255.255
- C 192.168.0.0 ~ 192.168.255.255

6. TCP/IP 계층 단위 응전인네
응용, 전송, 인터넷, 네트워크


# 오답노트
- DNS에서 TTL이 사용 될 때는 **데이터가 DNS 서버 캐시로부터 나오기 전 남은 시간**
- Ack는 TCP 헤더의 flag
- SNMP는 UDP 사용
- ICMP Type 0 : Echo Reply, Type 8 : Echo Request
- Data link 계층 : 2계층(오류, 흐름 제어)
- Linux /var에는 로그와 메일을 저장함
- Windows Server 2016에서 '컨테이너'라는 가상화 기술이 생김
- hosts 파일의 경로 : **'C:\Windows\System32\drivers\etc\hosts'**
- Windows Server 2016에서 [성능, 카운터, 로그]를 관리하는 그룹 : **Performance Log Users**
- 서버 에러 코드
500 : Internel Server Error
501 : Not Implemented
502 : Bad Gateway
503 : Service Unavailable
504 : Gateway Timeout
- Linux 파일 속성 명령어 lsattr은 i가 설정되어있으면 읽기 전용(root도 삭제 불가), chattr로 속성변경가능
- Fiber Optics : 광섬유
- 네트워크 계층 : IP, ICMP, ARP, RARP 전송 계층 : TCP, UDP
- TFTP는 UDP를 사용한다.
- 메트릭 : Hop Count 사용, RIP v1 : 브로드캐스트 RIP v2 : 멀티캐스트
- 이벤트 뷰어 Windows 로그에 속하는 것 : 보안, Setup, 시스템, Forwarded Events, 응용 프로그램
- vi 편집기에서 ex 10행~20행을 표현하고싶으면 :10,20s
- netstat -t는 TCP를 보여줌
- 라우팅은 링크 상태 라우팅과 거리 벡터 라우팅으로 나뉘고, 거리 벡터에서 '홉 수'를 사용한다.
- 라우터에서 show running-config 로 RAM의 값을 확인한다
- UDP 헤더에는 소스 포트, 목적지 포트, 길이(Length), 체크썸이 있다. (TCP에만 Ack가 있음)
- Unicast : 1대1, Multicast : 1대그룹, Broadcast : 1대다수
- TCP, UDP를 전부 사용하는 것 : DNS
- 서브넷 마스크 1이 네트워크, 0이 호스트 자리임.
- XON / XOFF는 흐름제어
- 성형 토폴로지는 고장나도 전체 영향 x
- 리눅스 바로 상위 디렉터리로 가는 명령어는 'cd ..'임
- SOA 레코드에서 책임자는 도메인 형태로 기입
- 내부 사설 IP, 외부 공인 IP => NAT
- Windows에서 명령어 route : 라우팅 테이블, tracert : 목적지 경로 추적
- 세션 : 대화 제어 / 전송, 데이터링크 : 에러 제어
- Windows Server에서 보안 로그에는 [파일, 시스템, 구성 변경]이 있음
- Linux에서 chown은 root만 사용가능 (소유 권한 변경)
- 도메인 쿼리 질의 파일은 resolv.conf
- Windows Server 2008에서 서버<=>서버는 Kerberos(대칭키와 티켓 사용)
- NAC(Network Access Control) 네트워크 비인가 단말 차단 (역할 기반 차단 x)
- IP 프로토콜은 '패킷 전송 역할'을 한다. 세그먼트 오류 감지나 정정 기능이 없음.
- 표현 계층에서 [암호, 압축, 인증] 기능을 수행한다.
- 로컬 보안 정책에는 [계정, 로컬, 이벤트, 시스템, 공개키]가 있다.
- 디스크 정보 명령어 : du
- 메모리 정보 명령어 : free
- SOA TTL이 길면 메모리 부하가 '줄어든다'
- CSMA/CD 표준은 802.11
- 게이트웨이 순서 정보 => tracert
- nice는 우선순위를 변경하는 명령어다. top은 실시간 cpu 사용률 명령어다
- init 6는 재부팅을 의미한다 (Run level 6)
- Hub, Repeater는 물리 계층, Bridge는 데이터 링크 계층, Router는 네트워크 계층이다.
- 루핑은 2개 이상의 경로가 있을 때 발생한다 (2개 '이상')
- ICMP v6에서 전달가능 여부는 **이웃 요청&광고 메시지**로 확인한다.
- CSMA/CD 기반 기술은 Ethernet이다.
- 시스템 임시파일은 /var에 저장한다.
- Windows Server 2008에서 가장 먼저 읽는건 index.htm 이다 (index.html 아님)
- OSPF는 Link State 기반이고, RIP를 지원하는데 홉의 총계는 사용하지않는다(Link state에서 사용을 안 함)
- 표본화 => **압축** => 양자화 => 부호화
- 데이터 링크 계층은 데이터 전송, 에러 제어, 통신 관리, 신뢰도가 낮은 전송로를 신뢰도가 높은 전송로로 바꿔준다
- VPN : 가상의 터널을 만들어 고비용 사설망을 대체함
- NAC(Network Access Control)은 End-Point 보안 솔루션, 보안 위협 정도에 따라 제어를 수행한다.
- Windows Server 2008에서 netstat 명령어를 사용하면 TCP,UDP,ICMP를 확인할 수 있다.
- Hyper-V에서는 외부, 내부, 개인 네트워크를 사용할 수 있다
- Active Directory에서 트러스트 내 도메인 통합 저장소는 **글로벌 카탈로그**이다.
