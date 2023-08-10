---
title:  "디자인 패턴 - 미디에이터 패턴(Mediator Pattern)"
excerpt: "디자인 패턴 중의 하나, 미디에이터 패턴(중재자 패턴)에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 중재자 패턴, 미디에이터 패턴, Mediator Pattern]

toc: true
toc_sticky: true

date: 2023-08-10
last_modified_at: 2023-08-10
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|**Mediator**|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 미디에이터 패턴
미디에이터 패턴은 중재자 패턴이라고도 불린다. 이 패턴은 **모든 클래스간의 상호작용(로직)을 캡슐화시켜서 하나의 클래스에 위임하여 처리하는 패턴**이다.

> M:N → M:1 의 관계로 만들어주는 패턴

유지 보수 및 재사용 확장성에 유리한 패턴이다. 객체들 간에 소통이 잘 되어있으나 복잡할 때 사용한다

> 비행기끼리 소통하는게 아닌, 관제탑을 중계로 소통하는 것과 같음

# 구조
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/4edc602f-5c76-453f-9f26-053f8f90054c)
[출처, 위키피디아](https://en.wikipedia.org/wiki/Mediator_pattern)

1. Mediator
Colleague 객체간의 소통을 위한 인터페이스
2. Colleague
Mediator를 통해 다른 Colleague와 소통을 위한 인터페이스
3. ConcreteMediator
Mediator 구현체로 Colleague간의 상호 소통을 위해 Colleague들을 가지고 있으며 소통들을 조정함
4. ConcreteColleague
Colleague 인터페이스의 구현체

# 장점, 단점
## 장점
1. 효율적인 자원 관리가 가능하다
2. 객체간의 통신을 위해 서로 간에 참조할 필요가 없어진다
3. 객체들 간 수정할 필요 없이 관계를 수정할 수 있다

## 단점
1. 특정 어플리케이션 로직에 맞춰져있어서 다른 어플리케이션에 재사용하기가 힘들다
2. 미디에이터 패턴 사용 시 미디에이터 객체에 권한이 집중화되어서 미디에이터 객체가 굉장히 크고 복잡해진다.