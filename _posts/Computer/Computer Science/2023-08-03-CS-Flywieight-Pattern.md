---
title:  "디자인 패턴 - 플라이웨이트 패턴(Flyweight Pattern)"
excerpt: "디자인 패턴 중의 하나, 플라이웨이트 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, 플라이웨이트 패턴, Flyweight Pattern]

toc: true
toc_sticky: true

date: 2023-08-03
last_modified_at: 2023-08-03
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|**Flyweight**|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 플라이웨이트 패턴
플라이웨이트 패턴이란 **인스턴스를 가능한 한 공유해서 사용함으로써 메모리를 절약할 수 있는 패턴**을 말한다. 어떤 클래스의 인스턴스 한 개만을 가지고 여러 개의 '가상 인스턴스'를 제공하고 싶을 때 사용한다.

# 구성 요소

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/44b9fae6-9935-485c-a698-3fb3302a2fd7)

1. Flyweight
공유에 사용할 클래스들의 인터페이스를 선언한다.
2. ConcreteFlyweight
Flyweight의 내용을 정의한다(실제 공유될 객체임).
3. FlyweightFactory
Flyweight의 인스턴스를 생성 또는 공유해주는 역할을 한다
4. Client
해당 패턴의 사용자

# 장점과 단점

## 장점
1. 실행시에 객체 인스턴스의 개수를 줄여 메모리를 절약할 수 있다.
2. 여러 '가상 객체'의 상태를 한 곳에 집중시켜놓을 수 있다.

## 단점
1. 특정 인스턴스만 다른 인스턴스처럼 동작하는 것이 불가능하다.
2. 객체의 값을 변경하면 공유받은 '가상 객체'를 사용하는 곳에 영향을 줄 수 있다.

어떤 클래스의 인스턴스가 아주 많이 필요할 때 모두 똑같은 방식으로 제어할 수 있는 경우에 유용하게 사용할 수 있다.