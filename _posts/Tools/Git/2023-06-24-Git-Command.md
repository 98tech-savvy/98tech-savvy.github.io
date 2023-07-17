---
title:  "Git의 기본 명령어"
excerpt: "깃의 기본 명령어에 대해 알아보자"

categories:
  - Git
tags:
  - [Git, Github, 깃, 깃허브, 깃허브 명령어]

toc: true
toc_sticky: true

date: 2023-06-24
last_modified_at: 2023-06-24
---

# git init

저장소(레포지토리)를 만드는 명령어. 로컬 Git 저장소를 설정한다

# git status

현재 상태 확인, 현재 작업 중인 파일의 상태를 확인한다

# git add

현재 상태를 추적한다. 파일의 변경사항을 인덱스에 추가함(커밋하기 전, 먼저 추가하기 위한 선행작업)

# git commit

현재 상태를 저장한다. 인덱스에 추가된 변경 사항을 추가한다.

# git log

```git
git log [options] [revision range] [path]
```

다양한 옵션을 조합해 원하는 형태의 로그를 출력한다.

# git reset

특정 커밋까지 이력을 초기화시킨다.

# git revert

특정 커밋을 취소하는 Ctrl + Z와 같은 명령어라고 보면 된다. 이 때 커밋이 되돌아가는게 아닌 1 2 3 에서 3에 git revert를 수행했다면 3에 새로운 2를 만들어내서 1 2 2의 기존 이력을 유지한다.

