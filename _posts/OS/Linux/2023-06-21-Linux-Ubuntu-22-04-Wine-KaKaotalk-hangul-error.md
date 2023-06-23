---
title:  "[Linux] Ubuntu 22.04 카카오톡 한글 두번 입력되는 현상 해결"
excerpt: "와인을 사용해 카카오톡을 설치했더니 한글을 두 번씩 입력하는 괴현상이 일어났다"

categories:
  - Linux
tags:
  - [Linux, Ubuntu, 리눅스, 우분투, 우분투 22.04, Wine, 카카오톡]

toc: true
toc_sticky: true

date: 2023-06-21
last_modified_at: 2023-06-21
---

리눅스에서 카카오톡을 사용하기 위해 와인을 설치하고 카카오톡을 실행했더니 카카오톡에서 한글이 두 번씩 입력되는 (ex : 안안녕녕하하세세요요) 현상이 일어났다.

해결 방법

터미널에서 와인 컨픽을 열고, 윈도우 버전을 **Windows 10** 으로 교체해준다

```linux
winecfg
```

이후 레지스트리 파일을 수정해주어야한다.

```linux
wine regedit
```

**내 컴퓨터 > HKEY_CURRENT_USER > Software > Wine 에서 X11 Driver 라는 키를 만들어주고, 그 키(폴더)안에 inputStyle 이라는 문자열을 만들어주고 데이터는 root로 해준다.

그 이후 카카오톡을 재실행해주면 문제 해결.

