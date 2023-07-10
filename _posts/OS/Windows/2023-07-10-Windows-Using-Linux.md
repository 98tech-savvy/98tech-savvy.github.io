---
title:  "윈도우10에서 리눅스를 사용해보자, WLS 설치하기"
excerpt: "윈도우10에서 사용할 수 있는 서브 시스템 리눅스(WLS2)를 사용해보자."

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Windows
tags:
  - [윈도우, Windows, 리눅스, Linux, WLS2]

toc: true
toc_sticky: true

date: 2023-07-10
last_modified_at: 2023-07-10
---

윈도우10에서는 리눅스를 서브 시스템으로 사용할 수 있다. 그것도 어플리케이션 설치만 해주면 간편하게 사용해줄 수 있다.

**WLS : 리눅스용 윈도우즈 하위 시스템**

1. Microsoft Store를 연다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/81061191-a17e-467c-abc5-822547299d2c)

2. Ubuntu 22.04 를 찾는다
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/e42b5ca0-930f-44ed-9d11-2edace5b6585)

3. Ubuntu 22.04 LTS를 설치해준다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/6737ee70-8e7a-483d-b003-e62fb6e405db)

4. Win 키를 눌러 검색창을 활성화 한 후 "기능" 을 검색해준다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/82aabf2f-c2e2-4a62-a021-1b96ef89cd47)
사진의 **[Windows 기능 켜기/끄기]**를 켜준다. 

5. Linux용 Windows 하위 시스템 (이하 WLS)를 체크해서 켜준다
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/d96067e5-835a-4707-8d68-f7f79050f51d)

6. 재부팅 후 Ubuntu 22.04 LTS 어플리케이션을 실행해준다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/69bebbc8-84ed-47df-b8b7-76ead3bbb0a8)

성공적으로 실행됨을 볼 수 있다. 이후 계정과 비밀번호를 입력해주면 설치 완료.