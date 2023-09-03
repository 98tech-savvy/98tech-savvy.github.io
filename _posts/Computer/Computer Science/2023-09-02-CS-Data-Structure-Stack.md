---
title:  "자료구조 - 스택"
excerpt: "자료구조의 기초, 스택에 대해 알아보자"

categories:
  - CS
tags:
  - [CS, 데이터 구조, Data Structure, 스택, Stack]

toc: true
toc_sticky: true

date: 2023-09-04
last_modified_at: 2023-09-04
---

# 스택이란?
스택(Stack)은 LIFO(Last In First Out) 구조로 데이터를 처리하는 자료구조로, 개념과 관련된 용어들은 다음과 같다.

bottom: 자료가 쌓이기 시작하는 가장 아래쪽
top: 연산이 일어나는 가장 윗부분
capacity: 스택의 최대 크기
최대 크기보다 더 많은 데이터를 스택에 저장하려고 해서 문제가 발생하는 것을 Stack Buffer Overflow라고 한다
stack pointer: 스택에 저장되어 있는 자료의 개수를 나타내는 정수값으로, 스택에서 각종 연산의 기준점이 된다
스택이 기본적으로 갖는 연산들은 아래와 같다.

push: 입력연산, 스택에 데이터를 추가
pop: 출력연산, 스택에서 데이터를 출력
peek: 조회연산, 스택의 top에 있는 데이터를 확인
