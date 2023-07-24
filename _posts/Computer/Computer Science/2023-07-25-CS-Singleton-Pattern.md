---
title:  "디자인 패턴 - 싱글톤 패턴(Singleton Pattern)"
excerpt: "디자인 패턴 중의 하나, 싱글톤 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 싱글톤 패턴, Singleton Pattern]

toc: true
toc_sticky: true

date: 2023-07-25
last_modified_at: 2023-07-25
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|**Singleton**|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 싱글톤 패턴
싱글톤 패턴이란 **객체의 인스턴스가 오직 한 개만 생성되는 패턴**을 의미한다. 

## 장점
객체의 인스턴스를 오직 한 개만 생성하게 된다면, **메모리적인 측면**에서 고정된 메모리 영역을 사용(최초 한번의 연산자를 통해)하기 때문에 추후 해당 객체에 접근할 때 메모리 낭비를 줄일 수 있다. 또한 이미 생성된 인스턴스를 활용하기 때문에 **속도적인 이점** 또한 있다고 볼 수 있다. 또 다른 클래스끼리의 **데이터 공유가 쉽다**. 싱글톤 인스턴스는 전역으로 사용되는 인스턴스이기 때문에 다른 클래스들이 접근하여 사용할 수 있다(하지만 동시성 문제가 발생할 수 있음)

## 단점
장점이 있다면 단점 또한 존재하는 법, 싱글톤 패턴에서는 뚜렷한 장점이 있는 만큼 많은 문제점을 수반한다.

먼저 **싱글톤 패턴을 구현하는 코드 자체가 많이 필요**하다. 또 위에서 언급했듯이 **동시성 문제**가 있기 때문에 Syncronized를 사용해주어야 한다. 그리고 싱글톤 인스턴스는 자원을 공유하기 때문에 테스트가 격리된 환경에서 수행하려면 매번 인스턴스의 상태를 초기화해주어야 한다. 이외에도 클라이언트가 구체 클래스에 의존하게 되는점, 자식 클래스를 만들 수 없는 점, 내부를 변경하기 어렵다는 여러가지 문제들 또한 존재한다.

# 유연성이 떨어지는 패턴
장점에 비해 단점들이 많은 것, 또 이러한 단점들을 봤을 때 유연성이 떨어지는 패턴이므로 이러한 디자인 패턴을 사용한다면 기초 설계를 잘 잡아주어야 할 것이다. 싱글톤 패턴을 사용한다면 프레임워크의 도움을 받으면 싱글톤의 문제점들을 보완할 수 있다.