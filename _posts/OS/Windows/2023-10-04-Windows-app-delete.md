---
title:  "[Windows] 기본 앱 삭제 방법"
excerpt: "윈도우의 필요없는 기본 앱들을 삭제해보자"

categories:
  - Windows
tags:
  - [Windows, 기본 앱 삭제, 앱, Powershell]
toc: true
toc_sticky: true

date: 2023-10-04
last_modified_at: 2023-10-04
---

[토마스 벤후트, 기본 앱 삭제 명령어](https://thomas.vanhoutte.be/miniblog/delete-windows-10-apps/) 를 참고해서 지우고 싶은 앱을 골라준다.

Camera 앱을 지워보도록하겠다.

1. Win + R 키로 [실행]창을 열어준다.

2. 빈 칸에 ``powershell`` 입력

3. 열린 파란색 창에 ``Get-AppxPackage *camera* | Remove-AppxPackage`` 입력

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/a1eb577b-e81e-4950-83d2-29c79c91f7dd)