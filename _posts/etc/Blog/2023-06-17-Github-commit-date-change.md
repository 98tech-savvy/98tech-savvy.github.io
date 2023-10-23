---
title:  "Github 커밋 날짜 변경하기"
excerpt: "깃허브 블로그 커밋 날짜를 변경하는 방법에 대해 알아보자."

categories:
  - Blog
tags:
  - [Blog, Github, 커밋 날짜 변경]

toc: true
toc_sticky: true

date: 2023-06-17
last_modified_at: 2023-06-17
---

Github 블로그를 운영하던 사람들의 '잔디밭(커밋한 날짜의 커밋한 게시글 만큼 깃허브의 로그 색깔이 초록색으로 진해져서 잔디밭이라고 부름)'에 이메일을 잘못 입력해 커밋했다거나 하는 등의 실수등으로 잔디가 심어지지 않았을 때 해결방법에 대해 알아보자

** ※ 커밋 날짜를 변경하기 위해선 커밋이 최소 2개 이상 되어있어야한다. **

터미널에서 자신의 깃허브 레포지토리로 들어간다

```shell
cd 98tech-savvy.github.io
```

그 이후

```shell
git log
```

명령어를 이용해 커밋한 로그를 본다

```shell
savvy@DESKTOP-K4SH6P5:~/98tech-savvy.github.io$ git log
commit 555 (HEAD -> master)
Author: 98tech-savvy <98tech.savvy@gmail.com>
Date:   Fri Jun 16 08:01:03 2023 +0900

    5

commit 444
Author: 98tech-savvy <98tech.savvy@gmail.com>
Date:   Thu Jun 15 07:21:03 2023 +0900

    4

commit 333
Author: 98tech-savvy <98tech.savvy@gmail.com>
Date:   Wed Jun 14 00:09:25 2023 +0900

    3

commit 222
Author: 98tech-savvy <98tech.savvy@gmail.com>
Date:   Tue Jun 13 08:58:22 2023 +0900

    2

commit 111
Author: 98tech-savvy <98tech.savvy@gmail.com>
Date:   Mon Jun 12 06:40:04 2023 +0900

    1
```

여기서 4의 날짜를 변경하고싶다고 가정하자. 그렇다면 **4의 이전의 커밋 hash 값인 3의 commit 333을 이용한다**

```shell
git rebase -i 333(commit의 해쉬값을 써주면 된다)
```

그러면 아래와 같은 텍스트가 나온다

```shell
pick 444 2023-06-15
pick 333 2023-06-14

# Rebase 806b078..d9876c6 onto 806b078 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
```

이 때, 바꾸려고 하는 444의 pick을 edit으로 변경해주면 된다

``pick 444 2023-06-15`` >>> ``edit 444 2023-06-15``

윈도우에서 Ubuntu를 사용하는 경우 Ctrl+X > N
리눅스, 맥의 경우 INSERT로 텍스트 진입 > edit로 변경 > ESC > :wq 입력해서 저장후 닫기

여기까지 되었다면 이제 444의 커밋 값을 변경할 수 있는 상태다.

```shell
git commit --amend --no-edit --date "날짜(요일 월 일 시간:분:초 연도 +0900)"
```

```shell
git rebase --continue
```

```shell
git push origin master(혹은 main)
```

그러면 잔디밭에 올바르게 잔디가 심어져있는 모습을 볼 수 있다. 하지만 젤 좋은 방법은 까먹지않고 성실하게 올바른 이메일로 커밋하는 것.

### 이메일의 경우

이메일의 경우에는 바로 위의 단계(amend)에서

```shell
git commit --amend --author=이메일
```

로 수정해주고 그 다음 단계들을 진행해주면 된다.

