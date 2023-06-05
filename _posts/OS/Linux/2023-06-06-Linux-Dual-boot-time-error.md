---
title:  "[Ubuntu] 듀얼 부팅 시 Windows 시간이 변경되는 문제 해결하기"
excerpt: "컴퓨터에 듀얼 부팅을 구성하던 중 Windows 시간이 바뀌는 문제를 찾았다."

//현재 카테고리: Comptuer, Blog, Python
categories:
  - Linux
tags:
  - [OS, Linux, 리눅스, 우분투, Ubuntu, Dual boot, 듀얼 부팅, 듀얼 부팅 날짜]

toc: true
toc_sticky: true

date: 2023-06-06
last_modified_at: 2023-06-06
---

> 듀얼부팅시 Windows 시간 변경되는 문제 해결하기
 

듀얼 부팅 체제를 구성하던 중에, Windows > Ubuntu 는 이상이 없는데
Ubuntu > Windows 로 바꿨을 시에 Windows 시간이 동기화가 되지 않는 문제를 찾았다.

Ubuntu는 UTC 시간을 기준으로 저장하는데, 로컬 타임으로 바꿔주면 된다.

Ubuntu에서 로컬 타임 저장하는 방법을 설명하겠습니다.

 
Ubuntu의 터미널에서:

$ timedatectl set-local-rtc 1 --adjust-system-clock
 
$ timedatectl
 
원래대로 UTC 타임을 저장하게 만들고 싶다면

$ timedatectl set-local-rtc 0 --adjust-system-clock