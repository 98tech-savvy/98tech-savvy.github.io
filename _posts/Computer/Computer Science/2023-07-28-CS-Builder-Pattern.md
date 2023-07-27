---
title:  "디자인 패턴 - 빌더 패턴(Builder Pattern)"
excerpt: "디자인 패턴 중의 하나, 빌더 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 빌더 패턴, Builder Pattern]

toc: true
toc_sticky: true

date: 2023-07-28
last_modified_at: 2023-07-28
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|**Builder**|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 빌더 패턴
**생성과 관련된 디자인 패턴으로, 동일한 프로세스를 거쳐 다양한 구성의 인스턴스를 만드는 패턴**이다. 복잡한 '객체를 생성하는 클래스'와 '표현하는 클래스'를 분리하여 동일한 절차에서도 서로 다른 표현을 할 수 있게끔 하는 방법을 제공한다. 특히 생성해야하는 객체가 Optional한 속성이 많을 수록 더 좋다.

빌더 패턴은 **생성자만 사용할 때 발생할 수 있는 문제**를 개선하기 위해 고안됐다. 팩토리 메서드 패턴이나 추상 팩토리 패턴에서는 생성해야하는 클래스에 대한 속성 값이 많아질 때 아래와 같은 문제들이 있었다.

> Client에서 팩토리 클래스를 호출할 때 Optional한 인자가 많아지면 **타입과 순서에 대한 관리가 어려워짐**
> 경우에 따라 필요 없는 파라미터들도 일일히 Null 값을 넘겨주어야함
> 생성해야 하는 Sub Class가 많아질 수록 팩토리 클래스가 복잡해짐

빌더 패턴은 이러한 문제를 보완하기 위해 별도의 Builder 클래스를 만들어 **필수 값은 생성자로, 선택적인 값들은 메소드를 통해** 값을 입력받고 build() 메서드를 통해 최종적으로 하나의 인스턴스를 return 한다.

> 불필요한 생성자를 만들지 않는다
> 데이터의 순서에 상관 없이 객체를 만들어낸다
> 사용자가 봤을 때 명시적이고 이해할 수 있어야 한다

# 장점
1. 빌더 패턴은 객체 생성 과정을 일관된 프로세스로 표현한다.
2. Default 매개 변수 생략을 간접적으로 지원한다
3. 필수 멤버와 선택적 멤버가 분리 가능하다
4. 객체 생성 단계를 지연할 수 있다
5. 멤버에 대한 변경 가능성 최소화를 추구할 수 있다
6. 초기화 검증을 멤버별로 분리할 수 있다

# 단점
1. 코드 복잡성이 증가한다
2. 생성자보다는 성능이 떨어진다
3. 지나친 빌더의 남용은 코드를 장황하게 만든다

