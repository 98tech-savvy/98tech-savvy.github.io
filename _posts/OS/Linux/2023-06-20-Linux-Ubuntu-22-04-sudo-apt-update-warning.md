---
title:  "[Linux] Ubuntu 22.04 Sudo apt -update W: 해결, 워닝 없애기"
excerpt: "Sudo apt -update 를 했을 때 나오는 W:apt-key를 없애보자."

categories:
  - Linux
tags:
  - [Linux, Ubuntu, 리눅스, 우분투, 우분투 22.04, 워닝, apt-key, sudo apt -update 워닝 해결]
자
toc: true
toc_sticky: true

date: 2023-06-20
last_modified_at: 2023-06-20
---

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/a6673219-546b-48d9-a8de-aabd3adb0f9d)

가끔 서버와 싱크를 맞추기 위해 sudo apt-get update 를 해주곤 한다. 하지만 가끔 마지막 줄에 여러 줄의 워닝: apt-key 가 나와 화면을 더럽히곤 한다. 가볍게 해결하는 방법

화면 왼쪽 상단의 **현재 활동** 혹은 어플리케이션 검색 창으로 진입한다.

검색 창에서 **Software & Update**를 검색해주고 들어간다. 거기서 **Other Software**에 진입, 중복된 키를 **1개를 제외하고** 전부 체크해제해준다.

해결.