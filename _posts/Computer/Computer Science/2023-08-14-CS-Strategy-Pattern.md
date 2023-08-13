---
title:  "디자인 패턴 - 전략 패턴(Strategy Pattern)"
excerpt: "디자인 패턴 중의 하나, 전략 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 전략 패턴, Strategy Pattern]

toc: true
toc_sticky: true

date: 2023-08-14
last_modified_at: 2023-08-14
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||**Strategy**|
|||Template Method|

# 전략 패턴
전략 패턴은 **실행 중에 알고리즘(전략)을 선택해 객체 동작을 실시간으로 바뀌도록 할 수 있게 하는 행위 디자인 패턴**을 말한다.

객체들이 할 수 있는 행위 각각에 대한 클래스(전략 클래스)를 생성하고, 유사한 행위들을 캡슐화하는 인터페이스를 정의해 객체의 행위를 동적으로 바꾸고 싶은 경우에 직접 행위를 수정하지 않고 전략을 바꿔주기만 함으로써 행위를 유연하게 확장하는 방법에 대해 말한다.

--------------------
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/01d35eea-d55f-4286-9b12-261ec36221d0)

1. Context
알고리즘을 실행해야 할 때마다 해당 알고리즘과 연결된 전략 객체의 메서드를 호출한다.
2. Strategy
모든 전략 구현체에 대한 공용 인터페이스를 뜻한다
3. ConcreteStrategy
알고리즘, 행위, 동작들을 객체로 정의한 구현체를 뜻한다
4. Client
특정 전략 객체를 Context에 전달함으로써 전략을 등록하거나 변경해 전략 알고리즘을 실행한 결과를 받는다.

> Context : 어떤 객체를 핸들링하기 위한 접근 수단

# 장단점

## 장점
1. Context의 코드 변경 없이 새로운 전략(Strategy)를 추가할 수 있다.

## 단점
1. Context에 적용되는 알고리즘이 적을 경우 분기를 타는 것이 편한 경우가 있다
2. 알고리즘이 많아질 수록 관리해야 할 객체의 수가 늘어난다
3. 적절한 전략을 선택하기 위해 전략 간의 차이점을 파악해야한다.
