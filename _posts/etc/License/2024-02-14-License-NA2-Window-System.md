---
title:  "[네트워크 관리사 2급] 8. 윈도우 시스템"
excerpt: "윈도우 시스템에 대해 알아보자"

categories:
  - License
tags:
  - [License, 네트워크 관리사 2급, 윈도우 시스템]

toc: true
toc_sticky: true

date: 2024-02-14
last_modified_at: 2024-02-14
---

# 윈도우 시스템
윈도우 시스템은 과거에는 단일 사용자 운영체제인 DOS였으며 이후에 GUI를 이용한 GUI 환경의 다중 사용자, 다중 프로세스 구조를 지원하는 운영체제가 되었다.

윈도우는 Plug & Play 기능을 지원하는데, 표준화된 인터페이스를 통해 하드웨어를 연결하였을 때 하드웨어를 자동으로 인식해 사용할 수 있게 하는 기능을 말한다. 이 Plug & Play 기능으로 개발하면 윈도우의 HAL(Hardware Abstraction Layer) 계층에서 하드웨어를 인식하고, 이 하드웨어를 Micro Kernel이 관리하게 된다.

> Plug&Play >> HAL >> Micro Kernel

## 윈도우 파일 시스템
윈도우는 FAT, FAT32, NTFS등을 지원한다. FAT(File Allocation Table)은 과거 DOS를 기반으로 하는 파일 시스템으로 작은 파일 시스템에 사용되며, NTFS(NT File System)은 대용량 파일, 긴 파일명, 압축, 오류처리 등에 사용된다. NTFS는 FAT으로 변환이 불가능하지만 FAT의 경우에는 NTFS로 변환이 가능하다.

### NTFS 파일 시스템
NTFS 파일 시스템은 기존 FAT의 파일 시스템을 개선하고 윈도우 서버용으로 사용하기 위해서 개발된 파일 시스템이다. EFS(대칭 키 기법), 다국어지원, 배드섹터 클러스터 재할당, 대용량(2TB 이상) 지원, MAC 호환 등의 기능이 있다.

## 윈도우 계정의 종류
1) 내장 사용자 계정
OS를 설치하면 자동으로 생성되는 계정으로, Administrator(관리자) 계정, Guest, IUSER_XXX, IWAM_XXX 등이 있다

2) 로컬 사용자 계정
OS로 로그인하는 계정으로, 해당 OS로만 로그인을 할 수 있다

3) 도메인 사용자 계정
윈도우 운영체제에 로그인 할 때 Active directory에서 관리하는 DC(Domain Controller)로 인증받은 후에 로그인을  할 수 있다.

> NETBIOS : LAN에서 서로 통신을 할 수 있게 해주는 프로그램, 라우팅 기능을 지원하지 않아 광역통신망 상에서 통신하는 어플리케이션 간에 TCP같은 Trasnport 메커니즘을 추가해 사용한다.