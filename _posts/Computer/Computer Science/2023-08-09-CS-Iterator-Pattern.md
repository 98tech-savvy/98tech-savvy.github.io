---
title:  "디자인 패턴 - 이터레이터 패턴(Iterator Pattern)"
excerpt: "디자인 패턴 중의 하나, 이터레이터 패턴(반복자 패턴)에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 이터레이터 패턴, 반복자 패턴, Iterator Pattern]

toc: true
toc_sticky: true

date: 2023-08-09
last_modified_at: 2023-08-09
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|**Iterator**|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 이터레이터 패턴
이터레이터 패턴은 반복자 패턴이라고도 불린다. **컬렉션 구현 방법을 노출시키지 않으면서 그 집합체 안의 모든 항목에 접근할 수 있는 방법을 제공하는 패턴**이다.

이터레이터 패턴을 사용하면 모든 항목에 접근하는 작업을 **컬렉션 객체가 아닌 이터레이터 객체**에서 맡게되기 때문에 집합체의 인터페이스 및 구현이 간단해지고, 집합체에서는 반복작업에서 손을 떼고 원래 자신이 할 일에 전념할 수 있다는 장점이 있다.

> 접근기능과 자료구조를 분리화시켜 객체화, Interface를 통일시키고싶을 때

# 구조
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/6af5ba88-f66e-40e4-a464-1dcfc86480e4)
[출처, 위키백과](https://en.wikipedia.org/wiki/Iterator_pattern)

1. Iterator
집합체의 요소들을 순서대로 검색하기 위한 인터페이스
2. ConcreteAggregate
Aggregate 인터페이스를 구현하는 클래스
3. Aggregate
여러 요소들로 이루어져 있는 집합체
4. ConcreteIterator
Iterator 인터페이스를 구현하는 클래스

# 장점, 단점
## 장점
1. 집합체 클래스의 응집도를 높여줌
2. 집합체 안의 모든 항목에 접근할 수 있게 해줌
3. 항목에 접근하는 작업을 컬렉션 객체가 아닌 이터레이터 객체에 맡김으로써 집합체의 구현이 간단해지고, 집합체에서 반복 작업에 손을 대지 않아도 됨

## 단점
단순한 순회를 구현할 경우 코드의 복잡도가 증가할 수 있음