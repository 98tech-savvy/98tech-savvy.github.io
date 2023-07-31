---
title:  "디자인 패턴 - 데코레이터 패턴(Decorator Pattern)"
excerpt: "디자인 패턴 중의 하나, 데코레이터 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, 데코레이터 패턴, Decorator Pattern]

toc: true
toc_sticky: true

date: 2023-08-01
last_modified_at: 2023-08-01
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|**Decorator**|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 데코레이터 패턴
데코레이터 패턴이란 **객체의 결합을 통해 기능을 동적으로 유연하게 확장할 수 있게 해주는 패턴**을 말한다. 즉, 기본 기능에 추가해야하는 기능의 종류가 많을 경우에 각 추가 기능을 Decorator 클래스로 정의 한 후에 필요한 Decorator 객체를 조합함으로써 추가 기능의 조합을 설계하는 방식이다.

# 구성 요소

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/858bf3e6-0eaf-4d16-833b-5510b9edd049)

데코레이터 패턴은 **Component, ConcreteComponent, Decorator, ConcreteDecoratorA ...**
으로 구성되어 있으며, 각 역할이 수행하는 작업은

1. Component
기본 기능을 뜻하는 ConcreteComponent와 추가 기능ㅇ르 뜻하는 Decorator의 공통 기능을 정의한다.
2. ConcreteComponent
기본 기능을 구현한다.
3. Decorator
많은 수가 존재하는 구체적인 Decorator의 공통 기능을 제공한다.
4. ConcreteDecoratorA ~ ...
Decorator의 하위 클래스로 기본 기능에 추가되는 개별적인 기능들을 뜻한다.

# 장점과 단점

## 장점
1. 기존 코드를 수정하지 않고 Decorator 패턴을 통해 확장시킬 수 있다.
2. 구성과 위임을 통해서 실행 중 새로운 행동을 추가할 수 있다.

## 단점
1. 의미없는 객체들이 너무 많이 추가될 수 있다.
2. Decorator를 많이 사용하면 코드가 복잡해진다.

Decorator 패턴은 **클래스의 요소들을 계속해서 수정하며 사용하는 경우, 여러 요소들을 조합해서 사용하는 클래스인 경우**에 사용하면 효과적으로 써줄 수 있다.