---
title:  "디자인 패턴 - 프록시 패턴(Proxy Pattern)"
excerpt: "디자인 패턴 중의 하나, 프록시 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 구조 패턴, 프록시 패턴, Proxy Pattern]

toc: true
toc_sticky: true

date: 2023-08-06
last_modified_at: 2023-08-06
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
||**Proxy**|Observer|
|||State|
|||Strategy|
|||Template Method|

# 프록시 패턴
프록시 패턴은 **대상 원본 객체를 대리해 대신 처리하게 함으로써 로직의 흐름을 제어하는 행동 패턴**을 말한다. 프록시(Proxy)는 사전적으로 '대리인'이라는 뜻이며, 프록시 패턴또한 사전적인 의미와 맞물려 객체지향에서 '클라이언트 측에서 대상 객체를 직접 쓰는게 아닌 프록시(대리인)를 거쳐서 쓰는 패턴'이라고 볼 수 있다.

즉, 대상 객체(Subject)의 메서드를 **직접 실행하는 것이 아닌** 대상 객체에 접근하기 전에 **프록시 객체 메서드에 접근**한 후 로직을 처리하고 접근하게 된다.

# 구성 요소

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/a959369e-d34b-4d01-91c8-abc234e69d12)
[출처, 위키백과](https://upload.wikimedia.org/wikipedia/commons/thumb/7/75/Proxy_pattern_diagram.svg/1200px-Proxy_pattern_diagram.svg.png)

1. Subject: Proxy와 RealSubject를 하나로 묶는 인터페이스
추상 메서드를 정의하며, 인터페이스가 있음으로 Proxy와 RealSubject 역할 차이를 의식할 필요가 없음
2. Client: Subject 인터페이스를 이용해 프록시 객체를 생성하는 사용자
3. RealSubject: 원본의 대상 객체
4. Proxy: 대상 객체(RealSubject)를 중계할 대리자
대상 객체를 합성하며, 대상 객체와 같은 이름의 메서드를 호출해 별도의 로직을 수행할 수 있지만 흐름제어만 할 뿐 프록시 내에서 결과값을 조작하거나 변경하면 안됨

# 종류
## 기본형 프록시

## 가상 프록시
지연 초기화 방식이며, 실제 객체의 생성에 많은 자원이 소모되나 실 사용이 잦지 않을 때 사용한다.

## 보호 프록시
프록시가 대상 객체에 대한 자원으로의 액세스를 제어할 수 있다

## 로깅 프록시
대상 객체에 대한 로깅을 추가하고 싶을 때 사용한다

## 원격 프록시
프록시 클래스는 로컬, 대상 객체는 원격 서버에 존재할 경우 사용할 수 있다.

## 캐싱 프록시
데이터가 클 경우 캐싱해 재사용을 유도한다.

# 장점과 단점

## 장점
1. 원래 하려던 기능을 수행하며 그 외 부가적인 작업을 수행할 수 있음
2. 클라이언트가 객체를 신경쓰지않음
3. 클라이언트 입장에서 프록시 객체와 실제 객체와 차이점이 없어 사용성에 문제되지 않음
4. OCP, SRP 준수

## 단점
1. 코드의 복잡도가 증가함(대상 객체의 흐름 제어를 할 프록시 객체의 증가)
2. 서비스로부터 응답이 늦어질 수 있음