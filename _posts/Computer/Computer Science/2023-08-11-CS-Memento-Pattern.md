---
title:  "디자인 패턴 - 메멘토 패턴(Memento Pattern)"
excerpt: "디자인 패턴 중의 하나, 메멘토 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 메멘토 패턴, Memento Pattern]

toc: true
toc_sticky: true

date: 2023-08-11
last_modified_at: 2023-08-11
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|**Memento**|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 메멘토 패턴
메멘토 패턴은 **객체 상태 정보를 가지는 클래스를 따로 만들어서 객체의 상태를 저장하거나 이전 상태로 복원할 수 있게 해주는 패턴**을 말한다. 즉, 원하는 시점의 상태 복원이 가능한 패턴이다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/261a14e5-1c71-4ee9-968b-9c593583e0a1)

1. Originator
저장할 객체의 클래스이다. Originator의 State(상태)를 저장한다
2. Memento
내부 정보를 추상화한 클래스이다. Caretaker는 Originator의 내부정보를 추상화한 Memento 타입의 정보를 가져간다.
3. Caretaker
Originator의 내부 정보를 가져와 저장한다


# 장단점
## 장점
1. 캡슐화를 지키면서 상태 객체의 상태 스냅샷(State snapshot)을 만들 수 있다.
2. 객체 상태가 바뀌어도 코드가 바뀌지 않는다
3. 객체 상태를 저장하고 복원하는 역할을 Caretaker에 위임할 수 있다

## 단점
1. 많은 정보를 저장하는 Memento가 자주 생성될 경우 메모리 사용량에 영향을 줄 수 있다.

*자바의 직렬화등에 사용된다*