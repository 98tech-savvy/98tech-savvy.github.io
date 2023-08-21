---
title:  "디자인 패턴 - 템플릿 메서드 패턴(Template Method Pattern)"
excerpt: "디자인 패턴 중의 하나, 템플릿 메서드 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴,템플릿 메서드 패턴, Template Method Pattern]

toc: true
toc_sticky: true

date: 2023-08-15
last_modified_at: 2023-08-15
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
|||State|
|||Strategy|
|||**Template Method**|

# 템플릿 메서드 패턴
템플릿 메서드 패턴이란 특정 작업을 처리하는 일부분을 서브 클래스로 캡슐화해 전체적인 구조는 바꾸지 않으면서 특정 단계에서 수행하는 내용을 바꾸는 패턴을 말한다. 객체지향 언어로 개발하다보면 무의식적으로 사용을 많이 하는 패턴이다.

**전체적으로 동일하면서 부분적으로는 다른 구문으로 구성된 메서드의 코드 중복을 최소화**할 때 유용하다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/47395a92-f9af-40bd-b0e3-987a6a4d8747)

상속을 통해 슈퍼 클래스의 기능을 확장할 때 사용하는 가장 대표적인 방법으로 변하지 않는 기능을 슈퍼 클래스에 만들어두고 자주 변경되며 확장할 기능은 서브 클래스에서 만들도록 한다.

# 장단점

## 장점
1. 중복 코드를 줄일 수 있다.
2. 자식 클래스의 역할을 줄여 핵심 로직의 관리에 용이하다
3. 코드를 객체지향적으로 구성할 수 있다.

## 단점
1. 추상 메서드가 많아지면서 클래스 관리가 복잡해진다.
2. 클래스간의 관계와 코드가 꼬여버릴 수 있다.

알고리즘의 뼈대를 맞추는 것이 목적인 템플릿 메서드 패턴은 전체적인 레이아웃을 통일하며 상속받은 클래스를 훅 메서드를 이용해 확장할 수 있도록 유연성을 주는 디자인 패턴이다.