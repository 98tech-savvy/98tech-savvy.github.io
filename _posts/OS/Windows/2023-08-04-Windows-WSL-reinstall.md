---
title:  "WSL 재설치 하기"
excerpt: "WSL에 문제가 생겼을 때, WSL을 재설치 하는 방법"

categories:
  - Windows
tags:
  - [윈도우, Windows, WSL, Windows Subsystem for Linux]

toc: true
toc_sticky: true

date: 2023-08-04
last_modified_at: 2023-08-04
---

1. 기존에 설치된 Ubuntu 리눅스 (WSL)을 조회한다

```bash
wslconfig.exe /l
```

```
Linux용 Windows 하위 시스템 배포:
Ubuntu(기본값)
```

2. 설치된 WSL을 삭제한다.

```bash
wslconfig.exe /u Ubuntu
```

```bash
등록 취소 중...
```

3. 삭제 후 확인한다.

```bash
wslconfig.exe /l
```

```
Linux용 Windows 하위 시스템에 배포가 설치되어 있지 않습니다.
아래의 Microsoft Store에서 배포를 설치할 수 있습니다.
https://aka.ms/wslstore
```