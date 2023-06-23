---
title:  "[Linux] Ubuntu 22.04 기본 입/출력 장치 변경하기"
excerpt: "리눅스를 켰을 때 기본 마이크/스피커를 변경해보자."

categories:
  - Linux
tags:
  - [Linux, Ubuntu, 리눅스, 우분투, 우분투 22.04, 기본 오디오 변경, 마이크, 스피커, 기본 스피커 변경]

toc: true
toc_sticky: true

date: 2023-06-23
last_modified_at: 2023-06-23
---

내가 찾은 2가지 방법이 있다.

# 구글에 퍼져있는 방법

sources = 마이크(입력장치)
sinks = 스피커(출력장치)

```li
pactl list short sources
pactl list short sinks
```
를 해주면 입/출력장치에 대한 정보와 넘버가 나온다.

```li
sudo vi /etc/pulse/default.pa
```

를 해주면 여러 코드가 주루루룩 나오는데, 내리다보면

```li
set-default-sink ~
set-default-source ~
```

부분이 있다. 여기서 ~ 부분을 위에서 찾은 sources와 sinks에서 찾은 넘버를 입력해주면 된다.

이후

```li
rm -rf ~/.config/pulse
```

명령어를 통해 pulse 폴더를 제거해준다.

# 이걸로 해결 못한 사람들을 위한 방법

나 같은 경우는 이걸 아무리 해도 어떤 입/출력장치로 변경해도 내가 원하는 입/출력장치로 변하지 않았다.

그래서 좀 더 쉽게 해결하는 방법을 알려준다.

리눅스의 앱 검색을 통해 **Startup Applications Preferences** 를 들어가준다.

그리고 시작 프로그램을 추가(A) 해준다.

위에서 찾은 source와 sink의 번호를 기억하자.

```
Name: mike (원하는 이름)
Command: pactl set-default-source 2(찾은 번호)
Comment:
```

```
Name: speaker (원하는 이름)
Command: pactl set-default-sink 4(찾은 번호)
Comment:
```

그리고 재부팅하면 원하는 입/출력 장치로 변경됨을 알 수 있다.