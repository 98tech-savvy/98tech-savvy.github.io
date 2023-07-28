---
title:  "디자인 패턴 - 프로토타입 패턴(Prototype Pattern)"
excerpt: "디자인 패턴 중의 하나, 프로토타입 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 프로토타입 패턴, Prototype Pattern]

toc: true
toc_sticky: true

date: 2023-07-29
last_modified_at: 2023-07-29
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|**Prototype**|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 프로토타입 패턴
실제 제품을 만들기에 앞서 테스트를 위한 샘플 제품을 **프로토타입**이라고 한다. 즉 프로토타입 패턴은 테스트를 위한 패턴, **원본 객체를 새로운 객체에 복사하여 필요에 따라 수정하는 패턴**을 의미한다.

프로토타입 패턴은 '자바'에서 ``clone`` 메서드를 활용해 사용할 수 있다.

프로토타입 패턴은 객체를 생성하는데 비용이 들고, 이미 유사한 객체가 존재하는 경우에 사용할 수 있다. 데이터베이스에 있는 데이터를 프로그램에서 수정해야 할 때, 매번 데이터베이스로부터 모든 데이터를 가져오는 대신에 한 번 데이터베이스에 접근해서 데이터를 가져온 객체를 필요에 따라 새로운 객체에 복사해 데이터 수정 작업을 거치면 되는 것이다.

