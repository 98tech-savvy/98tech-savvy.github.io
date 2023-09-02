---
title:  "자료구조의 기초"
excerpt: "자료구조의 기초에 대해 알아보자"

categories:
  - CS
tags:
  - [CS, 데이터 구조, Data Structure]

toc: true
toc_sticky: true

date: 2023-09-02
last_modified_at: 2023-09-02
---

# 자료구조란?
**자료구조(Data Structure)**란 효율적인 검색, 검색을 위해 데이터가 저장되는 방식을 말한다.

자료 자체의 형태와 그 자료들에 대한 연산을 **추상적 자료형(Abstract Data Type)**이라고 하는데, 이 추상적 자료형을 실질적으로 구현한 것을 자료구조라고 한다.

# 기본적인 자료구조

## 배열(Array)
가장 기본적인 자료형으로, 자료를 원소로 취급해 나열한 자료구조이다. 생성 시 원소들에게 고유한 인덱스(Index)를 부여해 이 인덱스를 통해 원소들에게 접근할 수 있다.

## 스택(Stack)
순서가 보존되는 **선형 데이터 구조**의 자료구조이다. LIFO(Last In First Out)구조의 메커니즘으로 데이터를 처리한다.

## 큐(Queue)
순서가 보존되는 **선형 데이터 구조**의 자료구조이다. 스택과 달리 FIFO(First In First Out)구조의 메커니즘으로 데이터를 처리한다

## 연결 리스트(Linked List)
노드(Node)라는 데이터묶음을 저장할 때 그 다음 순서의 자료가 있는 위치까지 데이터에 포함시키는 방식으로 자료를 저장하는 자료구조를 말한다.

## 그래프(Graph)
정점(Vertex)사이에 변(Edge)이 있는 자료구조를 말한다. 일방통행의 Directed Graph와 쌍방통행의 Undirected Graph가 있다.

## 트리(Tree)
그래프가 **계층적 구조**를 가진 자료구조를 말한다. 부모 노드(parentNode)와 자식 노드(childNode)의 연결 구조로 구현되어있다.