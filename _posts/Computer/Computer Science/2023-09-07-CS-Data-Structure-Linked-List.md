---
title:  "자료구조 - 연결 리스트"
excerpt: "자료구조의 기초, 덱에 대해 알아보자"

categories:
  - CS
tags:
  - [CS, 데이터 구조, Data Structure, 링크드리스트, Linked List, 연결 리스트]

toc: true
toc_sticky: true

date: 2023-09-07
last_modified_at: 2023-09-07
---

# 연결 리스트(Linked List)란?

연결 리스트(Linked List)란 노드(Node)라는 데이터 묶음을 저장할 때 그 다음 순서의 자료가 있는 위치를 데이터에 포함시키는 방식으로 자료를 저장하는 자료구조이다.

**최대 크기가 정해진 배열에 비해 최대 크기를 변화시키기 쉽고 데이터가 삭제되면 해당 데이터에 대한 메모리 예약도 없어지기 때문에 메모리 낭비가 적다**는 장점이 있지만
**index가 없이 반드시 순차 접근을 해야하기 때문에 처리속도가 비교적 느리다**는 단점또한 있다.