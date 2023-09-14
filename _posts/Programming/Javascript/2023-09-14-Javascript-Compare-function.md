---
title:  "자바스크립트(JavaScript) - Compare 함수"
excerpt: "Compare 함수에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, sort, compare function]

toc: true
toc_sticky: true

date: 2023-09-14
last_modified_at: 2023-09-14
---

# JS의 sort 함수
자바스크립트의 sort함수는 ``array.sort([Compare Function])``의 형태로 사용된다.
자신이 원하는 조건으로 정렬하기 위해 직접 Compare Functing을 구현해주어야한다.

이 때 Compare Function의 반환값에 따라 정렬은 다르게 동작한다

1. 반환값 == 0 → 변경없음
2. 반환값 >  0 → 오름차순
3. 반환값 <  0 → 내림차순 (음수일 때 위치가 바뀐다고 생각)