---
title:  "디자인 패턴 - 추상 팩토리 패턴(Abstract Factory Pattern)"
excerpt: "디자인 패턴 중의 하나, 추상 팩토리 패턴에 대하여"

categories:
  - Computer
tags:
  - [Computer, CS, 디자인 패턴, Design Pattern, 추상 팩토리 패턴, Abstract Factory Pattern]

toc: true
toc_sticky: true

date: 2023-07-26
last_modified_at: 2023-07-26
---

# 디자인 패턴이란?
[디자인 패턴이란?](https://98tech-savvy.github.io/computer/CS-Design-Pattern/) 게시글을 참고하자.

|생성(Creational) 패턴|구조(Structural) 패턴|행동(Behavioral) 패턴|
|--|--|--|
|Singleton|Adapter|Command|
|**Abstract Factory**|Composite|Interpreter|
|Factory Method|Decorator|Iterator|
|Builder|Facade|Mediator|
|Prototype|Flyweight|Memento|
||Proxy|Observer|
|||State|
|||Strategy|
|||Template Method|

# 추상 팩토리 패턴

[지식의 출처](https://victorydntmd.tistory.com/300)

추상 팩토리 패턴이란 **서로 관련이 있는 객체들을 통째로 묶어서 팩토리 클래스로 만들고 팩토리를 조건에 따라 생성하도록 다시 팩토리를 만들어서 객체를 생성하는 패턴**을 말한다.

생성 패턴의 팩토리 메서드(Factory Method) 패턴을 캡슐화한 방식이라고 볼 수 있다.

예를 들어, 삼성이 가전 제품 전시관을 열려고 하는데, 갑작스레 애플TV와 아이폰이 전시대에 전시되어있다고 생각해보자. 생각만해도 정신이 아득해진다. 삼성TV, 갤럭시, 갤럭시워치 등등 전부 '삼성' 제품이기 때문에 서로 관련이 있는 객체(삼성TV, 갤럭시, 갤럭시워치)를 통째로 묶어서(삼성) 팩토리 클래스로 만들고 그걸 다시 팩토리를 만들어 객체를 생성하는 패턴이라고 보면된다. 예를 들어보자

1. 삼성 가전제품을 만드는 클래스(SamsungBrandFactory)와 애플 가전제품을 만드는 클래스(AppleBrandFactory), 그리고 그것들을 캡슐화하는 BrandFactory 인터페이스를 정의한다.

```java
public interface BrandFactory{
  public TV createTV();
  public SmartPhone createSmartPhone();
}

public class SamsungBrandFactory implements BrandFactory{
  public SamsungTV createTV(){
    return new SamsungTV();
  }
  public SamsungSmartPhone createSmartPhone(){
    return new SamsungSmartPhone();
  }
}

public class AppleBrandFactory implements BrandFactory{
  public AppleTV createTV(){
    return new AppleTV();
  }
  public AppleSmartPhone createSmartPhone(){
    return new AppleSmartPhone();
  }
}
```

2. 그리고 입력값에 따라 다른 브랜드의 제품을 생성하는, 즉 객체 생성을 분기하는 FactoryOfBrandFactory 클래스를 정의한다.

```java
public class FactoryOfBrandFactory(){
  public void createTV(String type){
    BrandFactory brandFactory=null;
    switch(type){
      case "Samsung":
        brandFactory = new SamsungBrandFactory();
        break;
      case "Apple":
        brandFactory = new AppleBrandFactory();
        break; 
    }

    brandFactory.createTV();
    brandFactory.createSmartPhone();
  }
}
```

3. 마지막으로 이것들을 만들기 위한 Client 클래스를 정의한다.

```java
public class Client{
  public static void main(String args[]){
    FactoryOfBrandFactory factoryOfBrandFactory = new FactoryOfBrandFactory();
    factoryOfBrandFactory.createTV("Samsung");
  }
}
```

**추상 팩토리 패턴은 팩토리를 사용하는 방법에 초점을 둔다. 그리고 관련있는 여러 객체를 구체적인 클래스에 의존하지 않고 만들 수 있게 해주는 것이 목적이다.**