---
title:  "[Python] Set, Dict의 자료구조의 검색이 빠른 이유"
excerpt: "Set, Dict의 자료구조는 왜 빠른 검색이 가능할까?"

categories:
  - Python
tags:
  - [Python, 파이썬, set, dict, 자료구조, set자료형 속도, set 속도, dict 속도]

toc: true
toc_sticky: true

date: 2024-02-29
last_modified_at: 2024-02-29
---

set, dict는 해쉬함수를 이용한 해쉬값을 저장하고 있는 해쉬테이블이란 자료구조를 이용하기 때문에 빠른 검색이 가능하다. 해쉬는 임의의 변수를 숫자로 변환해 매핑하는 것을 의미하고, 따라서 임의의 변수를 숫자로 매핑해 인덱스처럼 사용하므로 빠른 검색이 가능한 것이다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/37a37c59-eb5c-4c66-82ed-22364dbdc39c)
*https://modeling-languages.com/robust-hashing-models/*


