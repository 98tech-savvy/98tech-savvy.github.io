---
title:  "Windows 무결성 검사하는 방법"
excerpt: "윈도우의 오류들을 해결해보자."

categories:
  - Windows
tags:
  - [윈도우, Windows, 무결성 검사, sfc /scannow]

toc: true
toc_sticky: true

date: 2023-07-15
last_modified_at: 2023-07-15
---

윈도우를 사용하며 여러가지 파일들을 설치하고 지워나가면서 잡다한 오류들이 생기기 마련이다. 그렇게 냅두다보면 어느새 컴퓨터는 느려지고 고장나기 시작하는데, 이 때 무결성검사와 그 외 여러가지 검사 방법들을 통해 예방하고 고쳐줄 수 있다.

Win 키를 눌러 검색화면에서 Powershell 을 검색해주고, 나오는 **Windows PowerShell**을 **[!]관리자 권한**으로 실행해주면 된다. 나오는 파란색 화면에 아래의 명령어들을 입력해주면 검사를 시작한다.

# 1. DISM
DISM<sup>Deployment Image Servicing and Management tool</sup>은 Windows 환경에서 운영체제의 이미지를 생성하고 적용하는 도구이다.

``DISM.exe /Online /Cleanup-image /Restorehealth`` 로 운영체제의 파일에 문제가 있는지 검사하고 문제가 있다면 그 파일을 복구한다.

# 2. SFC 검사 sfc /scannow
SFC<sup>System File Checker</sup>은 시스템 파일 손상을 검사하는 윈도우 자체 내장 유틸리티이다. 시스템 파일의 오류를 감지하고 감지했을 때 그 파일의 복구를 시도한다.

``sfc /scannow``
