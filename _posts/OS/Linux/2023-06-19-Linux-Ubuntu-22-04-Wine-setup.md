---
title:  "[Linux] Ubuntu 22.04 Wine 와인 설치하기"
excerpt: "와인을 설치해보자"

categories:
  - Linux
tags:
  - [Linux, Ubuntu, 리눅스, 우분투, 우분투 22.04, 와인, Wine, 윈도우 호환]

toc: true
toc_sticky: true

date: 2023-06-19
last_modified_at: 2023-06-19
---

Wine을 설치하면 윈도우즈 응용프로그램을 리눅스에서 사용할 수 있다.

일단 32비트 아키텍처를 활성화시켜준다(대부분의 윈도우즈 응용프로그램이 32비트 아키텍처 기반으로 만듦)

```linux
sudo dpkg --add-architecture i386
```

활성화되었는지 확인해본다.

```linux
dpkg --print-architecture
dpkg --print-foreign-architectures
```

대답은

```linux
amd64
i386
```

이 나오면 정상이다.

이제 와인을 설치한다.

```linux
wget -O - https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add
sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ impish main`
sudo apt update
sudo apt install --install-recommends winehq-stable
```

이러면 와인 설치가 완료됐다. 마지막으로 모노 패키지를 설치해주면 되는데 단순히 와인을 실행하면 설치 관리자가 뜬다.

```linux
wine PROGRAM
```

깔려진 와인 버전을 확인하려면

```linux
wine --version
```