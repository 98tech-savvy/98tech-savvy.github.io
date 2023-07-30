---
title:  "디자인 패턴 - 컴포지트 패턴(Composite Pattern)"
excerpt: "디자인 패턴 중의 하나, 컴포지트 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, 컴포지트 패턴, Composite Pattern]

toc: true
toc_sticky: true

date: 2023-07-31
last_modified_at: 2023-07-31
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|**Composite**|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 컴포지트 패턴
컴포지트 패턴은 객체들의 관계를 트리 구조로 구성하여 부분과 전체 계층을 표현하는 패턴이다. 클라이언트는 컴포지트 패턴을 통해 단일, 복합 객체를 모두 동일하게 다룰 수 있다.

컴포지트 패턴은 **전체-부분의 관계를 갖는 객체들 사이의 관계를 정의할 때** 유용하게 쓰일 수 있다.

## 구조
구조는 Component, Leaf, Composite로 이루어진다.

1. 컴포넌트(Component)
인터페이스, 혹은 추상 클래스로 정의되며 모든 오브젝트들에게 공통되는 메소드를 정의해야 한다. 그리고 클라이언트가 컴포지션내에 오브젝트들을 다루기 위해 제공되는 인터페이스를 말한다.
2. 리프(Leaf)
컴포지션내에 오브젝트들의 행동을 정의한다. 이는 복합체를 구성하는데 중요한 요소이며, 베이스 컴포넌트를 구현한다. 그리고 리프는 다른 컴포넌트에 대해 참조를 가지면 안된다.
3. 컴포지트(Composite)
리프(Leaf) 객체들로 이루어져 있으며 컴포넌트 내 명령들을 구현한다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/be0a1c61-036a-49ac-9875-cbd45ab5241b)

# 
부모 데이터의 리스트를 가질 수 있음과 동시에, 부모의 특징을 가져서 내 리스트도 내가 가질 수 있는 걸 구현해야 할 때 컴포지트 패턴을 활용하면 된다. (인벤토리안의 아이템 중의 '가방' 안의 아이템)