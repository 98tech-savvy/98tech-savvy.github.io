---
title:  "윈도우 환경에서 WSL을 사용해 Github 블로그를 만들기"
excerpt: "WSL을 사용해서 윈도우 환경에서 Github 블로그를 만들어보자"

categories:
  - Blog
tags:
  - [Blog, Github, Windows, WSL, Git, Commit, push, github blog, 블로그 구축]

toc: true
toc_sticky: true

date: 2023-08-05
last_modified_at: 2023-08-05
---

Windows에서 WSL을 활용해 Github 블로그를 설치하는 방법에 대해서 알아보는 시간을 가지겠다.

# Windows에서 WSL 설치하는 방법

1. Windows 기능에서 'Linux용 Windows 하위 시스템' 을 체크해서 설치해준다.

2. Windows Store에서 'Linux용 Windows 하위 시스템'을 설치해준다.

3. [x64용 WSL2 Linux 커널 업데이트 패키지](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)를 설치해준다.

4. 설치한 WSL을 실행해서 잠시 기다려준 후, 사용할 아이디와 패스워드를 정해준다.

# Github repository 생성하기

1. Github에 가입한다.
<br>
2. 자신의 Github 주소에서 Repository를 생성해준다.
<br>
    1. 접속한다
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/a3d5bacf-66fe-488e-98f6-ce5cf41f09aa)
https://github.com/자신의깃허브아이디?tab=repositories 에서 초록색의 **NEW**버튼을 눌러 레포지토리를 만들 수 있다.
<br>
    2. 그러면 아래의 화면이 나온다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/b14e89a3-74b8-4fb6-970e-088daa0fc79c)
        1. Repository name *
        └ **자신의ID.github.io**
        2. Initialize this repository with:
        └ **Add a README file 체크**
        3. 맨 하단의 Create repository 클릭
    <br>
3. Git Clone 하기
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/2a0e5f95-057d-413b-acaa-08321d1f13f1)

자신의 레포지토리에서 초록색의 **'<> Code'**를 눌러서 **HTTPS**의 주소를 복사하자. 오른쪽의 두개의 네모 겹친걸 누르면 복사가 된다.

**아까 깔았던 'Windows용 Linux 하위 시스템'에서 ``git clone 복사한 주소``**
를 입력해주자.
<br>
>*터미널이란 리눅스의 커맨드 창, 윈도우의 cmd, powershell 같이 CLI, "명령 줄 장치""를 말한다*

그러면 이제 WSL도 설치했고, 레포지토리를 자신의 컴퓨터에 클론까지 해주었다. 이제 jekyll과 ruby를 설치해서 블로그를 꾸며보자.

# Ruby와 Jekyll 설치하기
WSL의 터미널에서 다음과 같은 명령어를 입력해 패키지를 업데이트 해준다.

```linux
sudo apt-get update -y && sudo apt-get upgrade -y
```

이후 루비를 설치한다.
```linux
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby2.5 ruby2.5-dev build-essential dh-autoreconf
```

그리고 Ruby gems를 업데이트 해준다

```linux
gem update
```

그리고 Jekyll을 설치해준다.

```linux
gem install jekyll bundler
```

Jekyll의 버전을 확인한다.

```linux
jekyll -v
```

Ruby와 Jekyll 설치가 완료되었다.

----------------------

이제 Jekyll을 Clone한 블로그 레포지토리에 설치해보자.

WSL 터미널에서 아까 자신이 클론한 레포지토리로 이동해준다.

```
cd 자신의이름.github.io
```

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/50a80f76-32b0-421a-8020-377f9e0bb2b7)

위 사진과 같이 뜬 상태에서

```
jekyll new./
bundle install
```

그리고 로컬 서버를 열어서 jekyll의 설치가 되었는지 확인한다.

```li
bundle exec jekyll serve
```

*위 명령어는 후에 블로그 포스팅할 때 테스팅 목적으로 많이 사용하므로 알아두자*

로컬 서버의 주소는 다음과 같다.

http://127.0.0.1:4000/

Jekyll이 설치되었다면 **Welcome to Jekyll!**이라며 반기는 문구를 확인할 수 있다. Github에 커밋해서 결과를 반영해보자.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/50a80f76-32b0-421a-8020-377f9e0bb2b7)

위 사진과 같은 상태에서

```
git add .
git commit -m "커밋 메시지"
git push origin master
```