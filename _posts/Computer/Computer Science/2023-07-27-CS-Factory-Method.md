---
title:  "디자인 패턴 - 팩토리 패턴(Factory Pattern)"
excerpt: "디자인 패턴 중의 하나, 팩토리 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 팩토리 패턴, Factory Pattern]

toc: true
toc_sticky: true

date: 2023-07-27
last_modified_at: 2023-07-27
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|Abstract Factory|Composite|Interpreter|
|**Factory Method**|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 팩토리 패턴
팩토리 메서드 패턴은 객체지향 디자인 패턴이다. **부모 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴**이고 또 **자식 클래스가 어떤 객체를 생성할지 결정하도록 하는 패턴**이기도 하다. 혹은 부모 클래스에 구체 클래스 이름을 감추기 위한 방법으로도 사용되기도 한다.

*Template Method의 생성 패턴 버전으로도 볼 수 있다*

팩토리 메서드가 중첩되기 시작하면 프로그램은 굉장히 복잡해진다. 또 상속을 사용하지만 부모 클래스는 전혀 확장하기 않기 때문에 이 패턴은 extends 관계를 잘못 이용한 것으로도 볼 수 있다. extends 관계를 남발하면 프로그램의 복잡도가 증가하므로 팩토리 메서드 패턴의 사용에 주의해야 한다.

```python
class Chicken:
  FRIED_TYPE = 0
  SEASONED_TYPE = 1
  SOY_TYPE = 2

  def __init__(self):
    self.__price = None

  def getPrice(self):
    return self.__price

class FriedChicken(Chicken):
  def __init__(self):
    self.__price = 1.5

class SeasonedChicken(Chicken):
  def __init__(self):
    self.__price = 1.8

class SoyChicken(Chicken):
  def __init__(self):
    self.__price = 2

class ChickenFactory:
  def createChicken(self, chickenType):
    if chickenType == Chicken.FRIED_TYPE:
      return FriedChicken()
    elif chickenType == Chicken.SEASONED_TYPE:
      return SeasonedChicken()
    elif chickenType == Chicken.SOY_TYPE:
      return SoyChicken()

chickenPrice = ChickenFactory().createChicken(Chicken.FRIED_TYPE).getPrice()
print "$%.02f" % chickenPrice
```