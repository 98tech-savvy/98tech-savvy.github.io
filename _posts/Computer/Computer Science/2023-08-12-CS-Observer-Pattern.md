---
title:  "디자인 패턴 - 옵저버 패턴(Observer Pattern)"
excerpt: "디자인 패턴 중의 하나, 옵저버 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 옵저버 패턴, 관찰자 패턴, Observer Pattern]

toc: true
toc_sticky: true

date: 2023-08-12
last_modified_at: 2023-08-12
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
||Proxy|**Observer**|
|||State|
|||Strategy|
|||Template Method|

# 옵저버 패턴
옵저버 패턴은 **객체의 상태 변화를 관찰하는 관찰자들(옵저버들)의 목록을 객체에 등록해 상태 변화가 있을 시에 메서드등을 통해 객체가 각 목록의 옵저버에게 통지하는 디자인 패턴**을 말한다.

다시 말해 **객체가 변할 시 알림을 주는 디자인 패턴**이라고 보면 된다.

유튜브로 예를 들어보자면, 유튜버가 방송을 시작하거나 동영상을 업로드했을 때 구독자들에게 '알람'이 가는거라고 보면 된다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/bc209728-c81f-4541-a490-27483fedb494)

# 특징
옵저버 패턴에서는 객체 간 강한 결합(A가 변할 시 B의 상태가 변하는, 의존성의 문제가 있다)보다 **느슨한 결합으로 만들 수 있다**

## 느슨한 결합
느슨한 결합이란 그 둘이 상호작용을 하지만 서로에 대해 잘 모르는 것을 의미한다.

느슨한 결합을 사용하면
1. 옵저버를 언제든 추가, 제거할 수 있음
2. 새로운 형식의 옵저버에 주제를 변경할 필요가 없음
3. 주제-옵저버는 서로 독립적으로 재사용할 수 있음
4. 주제나 옵저버가 바뀌더라도 서로에게 영향을 끼치지 않음

> 서로 상호작용을 하는 객체 사이에서는 가능한 느슨한 결합을 사용한다

느슨한 결합은 시스템의 유지보수를 용이하게 하고, 전체 프레임워크를 안정적으로 만들어 시스템의 유연성을 증가시킬 수 있다.