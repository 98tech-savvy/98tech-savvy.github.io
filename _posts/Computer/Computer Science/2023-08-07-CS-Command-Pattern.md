---
title:  "디자인 패턴 - 커맨드 패턴(Command Pattern)"
excerpt: "디자인 패턴 중의 하나, 커맨드 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 커맨드 패턴, Command Pattern]

toc: true
toc_sticky: true

date: 2023-08-07
last_modified_at: 2023-08-07
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|**Command**|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 커맨드 패턴
커맨드 패턴이란 **요청을 객체의 형태로 캡슐화하여 사용자가 보낸 요청을 나중에 이용할 수 있게 요청에 필요한 정보를 저장, 로깅, 취소할 수 있게 해주는 패턴**이다. 커맨드 패턴에는 명령(Command), 수신자(Receiver), 발동자(Invoker), 클라이언트(Client)가 있으며, 수신자 객체를 가지고 있어 수신자 객체의 메서드를 호출해 그 메서드를 수행시킬 수 있다.

# 구조
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/5cbd16f5-08eb-496a-9d65-5f4068370505)

1. Command
실행될 기능에 대한 인터페이스이며, 실행될 기능을 execute 메서드로 선언한다.
2. ConcreteCommand
실제로 실행되는 기능을 구현한다(즉, Command라는 인터페이스를 구현함)
3. Invoker
기능의 실행을 요청하는 호출자
4. Receiver
ConcreteCommand에서 execute메서드를 구현할 때 필요한 클래스(즉, 수신자 클래스)

Command 패턴을 사용하면 여러 객체에 명령하기 위해 모든 객체들에 대해 의존성을 가질 필요가 없어지기 때문에 이러한 경우에 유용하게 사용할 수 있다(execute 메서드로 모든 객체들의 제어가 가능하기 때문).