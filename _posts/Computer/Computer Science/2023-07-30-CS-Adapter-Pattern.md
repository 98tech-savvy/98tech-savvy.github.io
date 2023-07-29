---
title:  "디자인 패턴 - 어댑터 패턴(Adapter Pattern)"
excerpt: "디자인 패턴 중의 하나, 어댑터 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, Adapter, Adapter Pattern, 어댑터 패턴]

toc: true
toc_sticky: true

date: 2023-07-29
last_modified_at: 2023-07-29
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|**Adapter**|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 어댑터 패턴
한국에서 일본 여행을 갈 때, 자신에게 필요한 전자 제품(충전기, 드라이기)을 챙겨서 가져갈 때 필수로 챙겨가야하는 것이 있다. 바로 220>110 변환 **어댑터** 이다. 이처럼 **어댑터 패턴**은 **호환되지 않는 인터페이스를 가진 객체끼리 협업할 수 있게 해주는 구조적 디자인 패턴**을 말한다. 어댑터 패턴은 아래와 같은 경우에 사용해 줄 수 있다.

1. 외부 라이브러리 클래스를 사용하고싶을 때, 다른 코드와 클래스의 인터페이스가 호환되지 않을 때
2. 여러 자식 클래스에서 부모 클래스를 수정하기에 호환성이 문제가 될 것 같을 때

하지만 어댑터 패턴은 추가 코드를 작성해야하는 번거로움과, 오버헤드가 발생할 수 있어서 무분별한 사용은 권장하지 않는다. 호환되지 않는 클래스들이 함께 작동해야하거나, 이미 존재하는 클래스의 인터페이스가 요구 사항에 맞지 않을 때 어댑터 패턴을 고려해줄 수 있다.

## 어댑터 패턴의 구성요소
어댑터 패턴에서는 **타겟(Target), 어댑티(Adaptee), 어댑터(Adapter), 클라이언트(Client)** 4개의 구성요소로 이루어져있다.

1. 타겟(Target)
클라이언트가 직접적으로 호출하는 인터페이스
2. 어댑티(Adaptee)
아직 호환되지 않은 기존 클래스(혹은 인터페이스)
3. 어댑터(Adapter)
타겟 인터페이스를 구현해 클라이언트 요청을 어댑티로 전달하는 클래스
4. 클라이언트(Client)
특정 작업을 요청하는 클래스

## 장점
1. 기존 코드를 변경치 않고 원하는 인터페이스 구현체를 만들어서 재사용할 수 있다.
2. 기존 코드가 하던 일과 특정 인터페이스 구현체로 변환하는 작업 중에 각기 다른 클래스로 분리해 관리할 수 있다.

## 단점
1. 다수의 새로운 인터페이스와 클래스를 도입해야하므로 구조가 복잡해진다
2. 때로는 서비스 클래스를 변경하는 것이 간단할 수 있다

