---
title:  "[Git] WSL git에서 username과 password 저장하기"
excerpt: "push나 pull을 할 때 username과 password를 입력하기 귀찮다면"

categories:
  - Git
tags:
  - [Git, Github, 깃, 깃허브, WSL, 비밀번호, username, passwd, password]

toc: true
toc_sticky: true

date: 2023-10-26
last_modified_at: 2023-10-26
---

git remote address가 ssh가 아니라 https로 되어 있는 경우, push나 pull을 해야 할 때 usename과 password를 입력하여 사용자 인증을 해야 한다.

그런데 최근 github에서는 이러한 사용자 인증 때 password 대신 PAC(Personal access code)를 쓰도록 정책을 변경하였다. 문제는 password와 달리 PAC는 암기할 수가 없고 메모장이나 다른 곳에 저장해놓고 계속해서 붙여넣기로 사용해주어야한다.

git에서는 내부적으로 username과 password를 암호화 해서 저장하는 keychain을 지원하고 있다(Mac이나 Windows에서 제공하는 기술을 지원함)

## 방법
OS에 따라 아래와 같이 git의 설정을 바꾸어 두면, 최초에 입력한 username과 password가 OS에 암호화되어 저장된 다음 이후로 별도의 입력 없이 사용되게 된다.

##### Mac
```shell
git config --global credential.helper osxkeychain
```

<br>

##### Windows
```shell
git config --global credential.helper wincred
```

<br>

##### Linux (Ubuntu)
1. libsecret를 설치한다.

```shell
sudo apt-get install libsecret-1-0 libsecret-1-dev
cd /usr/share/doc/git/contrib/credential/libsecret
sudo make
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

<br>

##### WSL

1. 1번 방법(내부 파일에 저장)
```shell
git config --global credential.helper store
```

2. 2번 방법(git-credential-manager 사용 ※WSL, Windows 양쪽에 git가 설치되있어야함)

```shell
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe"
```
