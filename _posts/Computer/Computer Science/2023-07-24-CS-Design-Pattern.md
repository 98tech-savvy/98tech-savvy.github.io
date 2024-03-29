---
title:  "디자인 패턴이란?"
excerpt: "개발자가 배워야 할 세 가지 디자인 패턴에 대해 알아보자"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern]

toc: true
toc_sticky: true

date: 2023-07-24
last_modified_at: 2023-07-24
---

# 디자인 패턴이란?
디자인 패턴<sup>Design Pattern</sup>은 작업을 더 쉽게 하기 위해 사용된다. 디자인 패턴을 활용하면 코드를 좀 더 보기 쉽게 되고 유지보수가 쉬워지게 만들 수 있다.

디자인 패턴을 알기 쉽게 설명해보자면 아래와 같다.

## 프로그래밍 언어는 언어, 프로그래밍 코드는 어휘

**프로그래밍 언어는 영어, 일본어, 한국어 등 언어와 같다**. 같은 언어를 사용하는 사람들끼리 만나면 아무리 어눌하게 말해도 결국에는 무슨 뜻을 말하는지 알 수 있다. **프로그래밍 코드는 표준어, 사투리같은 어휘와 같다**. 같은 언어를 사용한다 해도 같은 사투리를 쓰는 사람이면 알아듣기 쉽고, 사투리를 많이 접해보지 못한 사람이라면 이해하는데 어려움이 있을 것이다. 그러다 서울 사람이 제주도 사투리를 보면 못 알아들을 가능성도 높다.

디자인 패턴은 자신과 동료가 보다 효과적으로 의사소통하는데 사용할 수 있는 공유 어휘를 설정한 것이라고 볼 수 있다.

## 쓰레기통과 필요없어진 물건들을 담는 통
쓰레기통이란 무엇인가? 쓰레기통을 설명하자면 ``쓰레기를 일시적으로 보관하는 통을 말하며, 금속이나 플라스틱으로 이루어져 있다`` 이다. 만약에 쓰레기통이라는 단어를 쓰지 못한다면 누군가에게 쓰레기통을 말하고 싶을 때 저렇게 길게 풀어서 말해야만 할 것이다. **쓰레기통**이란 **쓰레기를 일시적으로 보관하는 통을 말하며, 금속이나 플라스틱으로 이루어져 있다**를 **압축**시켜논 것과 같다. 쉽게 말해 **덩어리화**시켜놨다고 보면 된다. 프로그래밍도 디자인 패턴을 장황하게 설명하지 않고 디자인 패턴 그 자체의 이름만을 말해서 프로그래밍 설계의 복잡도를 줄인다면 자신과 동료들간에 소통이 좀 더 쉬워질 것이다.

# 디자인 패턴의 카테고리
디자인 패턴은 **생성 패턴, 구조 패턴, 행동 패턴**으로 크게 세 가지 카테고리로 나눌 수 있다.

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
|||Template Method|

## 생성 디자인 패턴
생성 디자인 패턴<sup>Creational Design Patterns</sup>은 여러 상황에 맞는 객체 생성 메커니즘을 제공하여 코드를 유연하고 재사용 가능하게 유지한다. 객체가 생성되는 방식에 독립적인 시스템을 만드는 방법이다.

## 구조적 디자인 패턴
구조적 디자인 패턴<sup>Structural Design Patterns</sup>은 유연성과 확장성을 유지하면서 더 큰 시스템을 구축할 때 여러 클래스를 구성하고 결합하는 방법에 중점을 두고 있다. 이를 통해 시스템의 각 부분은 서로 독립적으로 변경할 수 있다.

## 행동적 디자인 패턴
행동적 디자인 패턴<sup>Behavioral Design Patterns</sup>은 서로 다른 객체가 서로 통신하는 방식에 관한 것이다. 객체와 클래스가 서로 어떻게 통신하고 동작해야 하는지에 대한 방식을 제공한다.
