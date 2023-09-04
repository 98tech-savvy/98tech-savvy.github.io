---
title:  "자료구조 - 큐"
excerpt: "자료구조의 기초, 큐(Queue)에 대해 알아보자"

categories:
  - CS
tags:
  - [CS, 데이터 구조, Data Structure, 큐, Queue]

toc: true
toc_sticky: true

date: 2023-09-05
last_modified_at: 2023-09-05
---

# 큐(Queue)란?
큐(Queue)는 FIFO(First In First Out) 메커니즘에 따라 데이터를 처리하는 자료구조로, 개념과 관련된 용어들은 다음과 같다.

front: 데이터를 꺼내는 쪽
rear: 데이터를 넣는 쪽
큐가 기본적으로 갖는 연산들은 아래와 같다.

enqueue: 큐에 데이터를 넣는다.
dequeue: 큐에서 데이터를 꺼낸다.
Python으로 큐를 구현할 때, list.pop(0)을 사용하면 FIFO 방식의 dequeue처럼 작동하기는 하는데, 이러면 매 연산마다 모든 객체에 index를 새로 부여하느라 O(n)의 시간 복잡도가 생긴다.

원형 버퍼(Ring Buffer)는 고정 크기의 큐를 마치 양 끝이 연결된 것처럼 사용할 수 있는 자료구조를 말하는데, index로 인한 시간 복잡도를 해결하기 위해서는 원형 버퍼를 사용하면 된다.