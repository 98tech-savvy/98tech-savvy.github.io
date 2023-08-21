---
title:  "디자인 패턴 - 인터프리터 패턴(Interpreter Pattern)"
excerpt: "디자인 패턴 중의 하나, 인터프리터 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 행동 패턴, 인터프리터 패턴, Interpreter Pattern]

toc: true
toc_sticky: true

date: 2023-08-08
last_modified_at: 2023-08-08
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|**Interpreter**|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 인터프리터 패턴
컴퓨터 과학에서 인터프리터(Interpreter)는 **소스 코드를 목적 코드로 변환하는 프로그램**을 의미한다.<br><br>디자인 패턴에서, 인터프리터 패턴은 **자주 등장하는 문제를 간단한 언어로 정의하고 재사용하는 패턴**을 의미한다.
# 구조
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/cee28150-bce9-4655-bdc5-742c1074bf8e)

1. Context
Expression에서 사용하는 모든 데이터들이 저장되어 있는 공간을 의미한다.
2. Expression
일련의 규칙을 계산하여 결과값을 반환한다
3. TerminalExpression
Expression을 포함시키지 않고, 계산된 결과만을 반환한다
4. NonTerminalExpression
Expression을 참조하며 종료를 하지 않고 다음 규칙으로 값을 넘기는 역할을 한다

# 장점, 단점
## 장점
1. 자주 등장하는 문제 문제 패턴을 언어와 문법으로 정의할 수 있음
2. 기존 코드를 변경시키지 않고 새로운 Expression을 만들 수 있음
## 단점
1. 복잡한 문법을 표현하려면 Expression과 Parser가 복잡해짐.

>*자바의 정규표현식, 스프링의 Expression Language등에서 사용된다*