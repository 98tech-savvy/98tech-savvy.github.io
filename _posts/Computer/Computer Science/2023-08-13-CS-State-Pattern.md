---
title:  "디자인 패턴 - 스테이트 패턴(State Pattern)"
excerpt: "디자인 패턴 중의 하나, 스테이트 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 상태 패턴, 스테이트 패턴, State Pattern]

toc: true
toc_sticky: true

date: 2023-08-13
last_modified_at: 2023-08-13
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
|||**State**|
|||Strategy|
|||Template Method|

# 스테이트 패턴
스테이트 패턴은 **객체가 상태에 따라 행위를 다르게 할 때, 직접 상태를 체크해 상태에 따른 행위를 호출하는 게 아니라 상태를 객체화해 필요에 따라 다르게 행동하도록 위임하는 디자인 패턴**을 말한다.

객체의 특정 상태를 클래스로, 클래스에서 해당 상태에서 할 수 있는 행위들을 메서드로 정의하고 이러한 각 상태 클래스들을 인터페이스로 캡슐화시켜서 클라이언트에 인터페이스를 호출하는 방식을 말한다.

예를 들어 데스크탑에서 원래 코드인 전원을 키는 powerOn, 전원을 끄는 powerOff에서 절전모드인 powerSaving을 추가한다고 할 때의 코드 수정은 크게 어렵지 않다. 하지만 분기점(On, Off, Saving)이외에 더 많은 분기점이 추가된다면 코드가 굉장히 길어져 상태에 따라 하고자 하는 행위를 파악하기 쉽지 않을 것이다. 또 TV, SmartPhone 등에서 같은 분기점을 사용한다면 기능이 변경될 때 마다 일일이 다 찾아가서 수정을 해야 할 것이다.

이 때 **스테이트 패턴**을 적용하면, 'On, Off, Saving' 상태를 클래스로 묶고 하나의 인터페이스로 정의한다음, 데스크탑, TV, 스마트폰등에서 인터페이스 메서드를 호출하기만 하면, 각 상태 클래스에서 정의된 행위가 수행되는 방식으로 바꿔줄 수 있다.

> 전략 패턴과 비슷하지만, 전략 패턴은 상속을 대체하려는 목적, 스테이트 패턴은 코드 내의 조건문들을 대체하려는 목적으로 사용된다는 점이 다르다.

# 장단점

## 장점
1. 상태에 따른 동작을 개별 클래스로 옮겨서 관리할 수 있음
2. 상태와 관련된 모든 동작을 각각의 상태 클래스에 분산시켜 '코드 복잡도'를 줄일 수 있다
3. 단일 책임 원칙을 준수할 수 있음
4. 개방 폐쇄 원칙을 준수할 수 있음
5. 하나의 상태 객체만 사용해 상태 변경을 하므로 일관성 없는 상태 주입을 방지하는데 도움이 된다.

## 단점
1. 관리해야할 클래스의 수가 늘어난다.
2. 상태 클래스의 갯수가 많고 상태 규칙이 자주 변경된다면 Context의 상태 변경 코드가 복잡해지게 될 수 있다.
3. 객체에 적용될 상태가 몇 가지 밖에 없거나 상태 변경이 이루어지지않는 경우 사용하지 않는 것이 좋다.
