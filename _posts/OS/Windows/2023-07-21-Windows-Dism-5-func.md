---
title:  "Windows DISM 필수 활용법 4가지"
excerpt: "윈도우 유지보수 도구인 DISM의 활용법을 알아보자."

categories:
  - Windows
tags:
  - [윈도우, Windows, DISM, 유지보수, 윈도우 유지보수 도구]

toc: true
toc_sticky: true

date: 2023-07-21
last_modified_at: 2023-07-21
---

DISM<sup>Deployment Image Servicing and Management</sup> 은 **배포 이미지 서비스 및 관리 도구**이다. 윈도우에 내장된 기본 툴로써 .wim(윈도우 이미지 파일 형식)을 기반으로 윈도우 이미지를 만들고 관리하는 용도로 비스타에 처음 도입되었다.

DISM을 통해 여러가지 기능을 수행할 수 있는데, 4가지 정도의 작업을 살펴보겠다

1. 윈도우 이미지 복구하기(10, 11)
2. 저장소 정리해 디스크 공간 확보하기
3. 국제 설정 변경하기
4. 윈도우 업데이트 설치하기

# DISM 4가지 기능

## 윈도우 이미지 복구하기
``/cleanup-image`` 옵션에

1. ``/checkhealth``
2. ``/scanhealth``
3. ``/restorehealth``

스위치로 오작동하는 윈도우 시스템을 정상 상태로 복원할 수 있다.

## 저장소 정리해 디스크 공간 확보하기

```bat
dism /online /cleanup-image /analyzecomponentstore 
dism /online /cleanup-image /startcomponentcleanup
```

로 윈도우 구성요소 저장소(WinSxS 폴더에 위치함)에 있는 이전 버전의 업데이트 구성 요소를 찾아 삭제할 수 있다. 

## 국제 설정 변경하기

``dism /online /Get-Intl`` 를 사용해 언어 설정을 확인할 수 있다.

여기서 언어 설정을 확인한 후 자신의 원하는 옵션을

```
/Set-UILang, /Set-UILangFallback, /Set-UserLocale, /SetInputLocale
```

등으로 변경할 수 있다.

## 윈도우 업데이트 설치하기
``dism /Add-Package`` 옵션을 사용해 윈도우 업데이트가 제대로 작동하지 않을 때, 원격 배포를 관리할 때 사용할 수 있다.