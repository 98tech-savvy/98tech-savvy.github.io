---
title:  "[네트워크 관리사 2급] 15. 네트워크 서버 운영"
excerpt: "네트워크 서버 운영에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, 네트워크 서버 운영]

toc: true
toc_sticky: true

date: 2024-02-22
last_modified_at: 2024-02-22
---

# 네트워크 서버 운영

## NIC(Network Interface Card)
NIC는 OSI 7계층에서 **물리 계층**에 속해있는 장치이다. LAN 케이블(UTP)와 연결되어서 네트워크와 컴퓨터 간에 통신을 수행해준다.

### NIC 특징
1. 데이터 링크 계층과 물리 계층 사이에서 통신을 수행함
2. **베이스밴드**를 사용해 **디지털 신호를 변환**함
3. LAN, 토큰 링등의 네트워크에서 사용됨
4. 인터페이스 역할을 수행함
5. MAC주소가 할당되어 있음(할당은 데이터 링크 계층에서 수행)
6. 고성능의 데이터 처리를 위해 송수신되는 데이터를 압축함

### NIC 카드 종류
NIC는 이더넷, 고속 이더넷, 기가비트 이더넷, Token Ring, ATM LAN등으로 나뉠 수 있는데 다음의 특징을 가지고 있다.

1. 이더넷 : 10Mbps
2. 고속 이더넷 : 100Mbps
3. 기가비트 이더넷 : 1Gbps
4. Token Ring : 16Mbps, 메인 프레임 시스템에 설치
5. ATM LAN : 고속의 ATM 네트워크에 접속하기 위해서 사용됨

### ISA, PCI
요새는 전부 PCI Express 방식을 사용하지만, NIC ⇔ 메인보드 간에 사용되는 방식은 두 가지가 있다.

1. ISA(Industry Standard Architecture bus) 방식
16bit, 3Mbps의 성능을 가지고 있으며 IBM의 PC/XT나 PC/AT를 위해서 지원된 방식이다.

2. PCI(Peripheral Component Interconnect bus) 방식
32bit 및 64bit를 지원하며 버스 마스터링 기능을 처리한다.

>> 버스 마스터링(Bus Mastering) : 인터럽트를 사용하지 않고 해당 단말기에 직접 정보를 전송해 DMA 방식을 개선한 방식

## VLAN(Virtual Local Area Network)
VLAN은 **하나의 물리적 스위치로 여러 논리 환경을 구성해 각각 다른 설정과 관리를 할 수 있는 네트워크 가상화 기술**을 말한다. IEEE 802.10에 표준으로 지정했으며 **불필요한 브로드캐스트를 방지할 수 있는 기술**이다. 또 데이터 처리 흐름을 관리해 **네트워크 보안성을 향상**시켰다.

VLAN 특징 : 브로드캐스트 제어, 보안성 향상, 트렁크

VLAN은 정적(Static) 방식과 동적(Dynamic) 방식이 있는데, 정적 방식은 가장 일반적으로 사용되는 방식으로 포트 별로 VLAN을 관리하고 모니터링을 한다. 동적 방식은 MAC 주소를 기반으로 VLAN을 구성하는 방식으로 대형의 스위치에서 사용한다.

### VTP(VLAN Trucking Protocol)
VLAN의 특징 중 '트렁크'라는 특징이 있었는데, 이 VTP는 복수 개의 스위치 간에 VLAN 설정 정보를 교환할 수 있는 프로토콜로 VLAN 설정의 편의성을 향상시킬 수 있다. ISL, IEEE 802.1q, LANE, 802.10(FDDI)등의 방법이 있다.

## RAID(Redundant Array of Independent Disks)
저용량, 저성능, 저가용성인 **디스크를 배열(Array)구조로 중복 구성함으로써** 고용량, 고성능, 고가용성 디스크를 **대체**할 수 있는 기법이다. **데이터 분산 저장에 의한 액세스**가 가능하며, **병렬 데이터 채널에 의한 데이터 전송 시간을 단축할 수 있는 장점**이 있다.

1. 디스크 배열 기술로 여러 개의 하드 디스크를 하나의 배열로 관리함
2. 논리적으로 하나의 디스크로 보임
3. 고장이 발생해도 즉시 백업 하드 디스크가 복구해 가용성을 향상시킴
4. 많은 디스크가 필요함, 하지만 복구 용이

RAID에는 여러 종류가 있는데 각각 RAID 0(Stripe), RAID 1(Mirroring), RAID 2(Hamming Code ECC), RAID 3(Parity ECC), RAID 4(Parity ECC Block), RAID 5(Parity ECC 분산 저장), RAID 6(Parity ECC 분산 복수 저장)이 있다.

### RAID 0(Stripe, Concatenate)
최소 2개의 디스크로 구성되며 작은 디스크를 모아 하나의 큰 디스크를 만드는 기술이다. Disk Striping으로 데이터를 나누어 저장하지만 중복되어 저장되지 않기 때문에 에러가 발생해도 복구할 수는 없다.

### RAID 1(Mirroring)
**Disk Mirroring**은 여러 디스크에 데이터를 이중화해 저장하는 방식이라 RAID에서는 **가장 좋은 방식**이지만 **비용이 많이 발생한다는 단점**이 있다. Disk Mirroring 방식은 복구가 가능하고 Read와 Write가 병렬실행되어 속도가 빠르다는 장점이 있다.

### RAID 2(Hamming Code ECC)
ECC(Error Correction Code)가 없는 기능이 없는 디스크의 복구를 위해 개발되었고, **Hamming Code를 이용해 오류 복구를 한다**

### RAID 3(Parity ECC)
**Parity 정보를 별도 Disk에 저장한다**. 1개의 디스크 장애 시 패리티를 통해 복구가 가능하며 RAID 0 방식으로 구성된 디스크의 I/O 성능은 향상되나 Parity 계산 때문에 Write 성능이 저하된다는 단점이 있다.

### RAID 4(Parity ECC, Block 단위 I/O)
RAID 3와 다른점은 **데이터를 Block 단위로 저장**한다는 점이다. 그 외에는 RAID 3와차이가 없다.

### RAID 5(Parity ECC, 분산 저장)
**분산 Parity**를 구현해 안정성이 향상되었고, **최소 3개의 디스크가 필요**하다.

### RAID 6(Parity ECC, 분산 복수 저장)
**분산 Parity인 RAID 5의 안정성 향상을 위해 Parity를 다중화해서 저장**한다. 장애 상황에서도 정상적으로 동작한다.
