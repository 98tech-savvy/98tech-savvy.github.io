---
title:  "[Linux] Ubuntu 22.04 Grub 부팅 순서 변경하기"
excerpt: "Grub의 부팅순서를 변경해보자"

categories:
  - Linux
tags:
  - [Linux, Ubuntu, 리눅스, 우분투, 우분투 22.04, Grub, 부팅 순서, Windows Boot loader]

toc: true
toc_sticky: true

date: 2023-06-12
last_modified_at: 2023-06-12
---

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/c7bf6aef-b507-44cd-ab46-595d440d5d11)

Windows와 Ubuntu의 듀얼 부팅 환경을 구성했다면, Grub이라는 부팅로더가 컴퓨터를 켰을 때 이렇게 반기는 모습을 볼 수 있다. 지금은 Ubuntu가 기본으로 되어있는데, Windows를 기본으로 바꾸고 싶다.

간단하게 grub의 파일을 수정해주면 끝난다.

```shell
$ sudo nano /etc/default/grub
```

연 grub의 파일에서
GRUB_DEFAULT = saved 로 수정

```shell
$ sudo update-grub
```

```shell
sudo grub-set-default 기본으로 설정할 첫번째사진에 있는 인덱스
```

확인

```shell
grub-editenv list
```