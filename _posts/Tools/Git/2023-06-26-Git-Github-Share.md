---
title:  "[Git] Github에 공유하기"
excerpt: "Github에 자신의 코드를 공유해보자"

categories:
  - Git
tags:
  - [Git, Github, 깃, 깃허브, 깃허브 공유, 코드 공유, 오픈 소스]

toc: true
toc_sticky: true

date: 2023-06-26
last_modified_at: 2023-06-26
---

Github에 공유를 하기 위해서는 일단 회원가입을 진행해야한다.

회원가입을 진행 후 자신의 레포지토리(저장소)를 생성해준다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/acc033f2-8d81-449d-b6ee-7ba120223ec1)

그럼 이러한 페이지가 나온다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/5187e4b9-4b86-4517-92cd-5e389a718d42)

1. 레포지토리의 이름을 적어준다
2. 공개할건지 비공개할건지 선택해준다
3. 레포지토리를 만든다

# git push
로컬 저장소(나의 컴퓨터)에서 원격 저장소(Github)로 푸시해보자(파일을 올려보자).

```git
git remote add name url

git push [-u | --set-upstream] [repository]
```

메인 브랜치가 main이고, 원격 저장소를 origin으로 설정했다면

``git push origin master`` 식으로 푸시해주면 된다.

새 커밋을 푸시하고싶다면

```git
git add .
git commit -m "커밋 내용"
git push origin master
```

식으로 해주면 된다.

# git clone

git clone은 레포지토리를 복제해주는 명령어이다.

```git
git clone [repository] [directory]
```

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/ca1939bd-b64c-4fdd-be21-471ccc4dc7f0)

터미널에서 복제하고 싶은 폴더의 위치로 이동한 후에

``git clone 레포지토리 주소`` 를 해주면 복제가 된다.

# git pull

원격 저장소에 변경된 내용을 로컬 저장소로 가져올 수 있다.
