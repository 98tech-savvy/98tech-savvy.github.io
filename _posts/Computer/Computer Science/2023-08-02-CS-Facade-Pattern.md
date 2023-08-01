---
title:  "디자인 패턴 - 파사드 패턴(Facade Pattern)"
excerpt: "디자인 패턴 중의 하나, 파사드 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, 파사드 패턴, Facade Pattern]

toc: true
toc_sticky: true

date: 2023-08-02
last_modified_at: 2023-08-02
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|**Facade**|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 파사드 패턴
파사드 패턴은 **일련의 저수준 인터페이스들을 하나의 고수준 인터페이스로 묶어주는 패턴**을 말한다. 클라이언트 객체에서 여러 저수준의 인터페이스의 동작을 제어하려면 여러 저수준 인터페이스의 메서드들을 일일히 호출해야 하는데, 파사드 패턴을 이용하면 고수준 인터페이스의 메서드 호출 한 번만으로 동작시킬 수 있다.

*고수준 인터페이스를 '통합 인터페이스' 라고도 부름*

클라이언트 객체가 파사드 패턴을 사용하면 고수준 인터페이스만 건드리면 되므로 여러 저수준 인터페이스에 대한 의존성이 느슨해진다.

# 구성 요소

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/d9ca77f3-0e15-411f-9122-5cb9fa358ab6)
*[출처 위키백과](https://ko.wikipedia.org/wiki/%ED%8D%BC%EC%82%AC%EB%93%9C_%ED%8C%A8%ED%84%B4)*
# 장점과 단점

## 장점
1. 코드를 간단하게 만들 수 있다

## 단점
1. 고수준 객체가 복잡해진다.

파사드 패턴을 사용할 때 객체의 계층화를 잘 고려하여 최대한 연관성 있는 개체들끼리 모음으로써 고수준 객체를 잘 설계해야 한다.