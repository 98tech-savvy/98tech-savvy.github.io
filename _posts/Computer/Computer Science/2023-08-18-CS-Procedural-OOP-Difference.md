---
title:  "절차지향과 객체지향의 차이"
excerpt: "절차지향과 객체지향의 차이점에 대해 알아보자"

categories:
  - CS
tags:
  - [CS, Procedural Programming, Object Oriented Programming, OOP, 객체지향, 절차지향, 차이점]

toc: true
toc_sticky: true

date: 2023-08-18
last_modified_at: 2023-08-18
---

절차지향과 객체지향 프로그래밍의 차이점을 알아보기 전에, 절차지향과 객체지향이 무엇인가에 대해 알아보자.

# 절차지향이란?
**절차지향 프로그래밍(Procedural Programming)**이란 위에서 아래로 흐르는 것처럼 순차적인 처리가 중요시 되며 프로그램 전체가 유기적으로 연결되도록 만드는 프로그래밍 기법이다. 대표적으로 **C언어**가 있으며 컴퓨터의 작업처리 방식과 유사하기 때문에 작업 처리 속도가 객체지향에 비해 빠르다. 하지만 이러한 장점은 하드웨어의 빠른 발전을 통해 컴퓨팅 환경이 증가함에 따라 중요치않아지게되었고 그에 따라 **모듈화, 캡슐화같은 개념적으로 접근하는 형태를 통해 만드는 객체지향 프로그래밍**이 만들어졌다.

## 장점
컴퓨터의 처리구조와 유사해 실행속도가 빠르다

## 단점
유지보수가 어렵고, 실행 순서가 정해져있어서 코드 순서를 바꾸면 동일한 결과를 보장하기 어렵다. 그리고 디버깅이 어렵다는 단점이 있다

# 객체지향이란?
**객체지향 프로그래밍(Object Oriented Programming)**이란 **실제 세계를 모델링하여 소프트웨어를 개발하는 방법**이다. 데이터와 절차를 하나의 덩어리로 묶어서 개발하게 되는데, 이는 컴퓨터 부품을 하나 하나 사서 컴퓨터를 조립하는 조립컴퓨터와 유사한 방식을 가지고 있다.

객체지향 프로그래밍은 3가지의 대표 특성을 가지고 있다.

1. 캡슐화
관련된 데이터와 알고리즘을 하나의 묶음으로 정리된 것으로 개발자가 만들었으며 관련된 코드와 데이터가 묶여있고 오류가 없어서 사용이 편리하다. 데이터를 감출 수도 있으며 외부 세계와의 상호작용은 메서드를 통해 할 수 있다.

2. 상속
이미 작성된 클래스를 이어받아서 새로운 클래스를 생성하는 기법으로 위의 클래스는 부모 클래스, 아래의 클래스는 자식 클래스라고 칭한다. 기존 코드를 재활용해 사용하는 것을 의미하며 객체지향 방법의 장점 중에 하나이다

3. 다형성
하나의 이름으로 많은 상황에 대처하는 기법이다. 개념적으로 동일한 작업을 하는 함수들에 똑같은 이름을 부여해 코드가 간단해지는 효과가 있다.

그리고 위의 세 가지 특성으로 아래의 장점들을 가지게 된다.

1. 신뢰성 있는 소프트웨어를 작성할 수 있다
2. 코드재사용이 용이하다
3. 디버깅이 쉽다
4. 업그레이드가 쉽다

## 장점
1. 코드의 재활용성이 높다
2. 코딩이 절차지향보다 간편하다
3. 디버깅이 쉽다

## 단점
1. 처리속도가 절차지향보다 느리다
2. 설계에 많은 시간 소요가 들어간다

이제 객체지향과 절차지향에 대한 기본적인 개념을 공부해봤으니, 이 둘에 대한 차이점에 대해 자세히 알아보자

# 객체지향과 절차지향의 차이점
중요한게 있다. **객체지향의 반대는 절차지향이 아니며, 절차지향의 반대는 객체지향이 아니다.** 절차지향은 순차적으로 실행되는데 초점이, 객체지향은 객체간의 관계에 초점을 두고 있을 뿐 서로 반대되는 개념은 아니다. 

김치볶음밥 만드는 과정에 대해 절차지향과 객체지향으로 설명해보자.

- 절차지향

```
마트에간다
▽
김치를 산다
▽
대파를 산다
▽
식용유를 산다
▽
베이컨을 산다
▽
달걀을 산다
▽
간장을 산다
▽
대파와 식용유를 넣고 볶아준다
▽
베이컨, 간장을 넣고 볶아준다
▽
설탕, 김치를 넣고 볶아준다
▽
밥을 넣고 볶아준다
▽
완성
```

- 객체지향

```
┌(장보기 팀)
│마트에 가서 김치,대파,식용유,│베이컨,달걀, 간장을 산다
│
├(요리 팀)
│장 본 음식들로 대파,식용유를 │넣고 볶아준 후 베이컨, 간장을 │넣고 볶고 마지막으로 설탕, 김치, │밥을 넣고 볶아준다
│
완성
```

절차지향은 데이터를 중심으로, 객체지향은 기능을 중심으로 메서드를 구현하게 된다.

<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td>&nbsp;</td>
<td style="text-align: center;"><b>절차지향(POP)</b></td>
<td style="text-align: center;"><b>객체지향(OOP)</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>접근 방식</b></td>
<td style="text-align: center;"><b><span><span>Top-Down</span></span></b><br><span><span>(시스템 동작 방식을 먼저 생각,</span></span><br><span><span>그 다음 세부 모델 디자인)</span></span></td>
<td style="text-align: center;"><b><span><span>Bottom-Up</span></span></b><br><span><span>(세부 모델 디자인 후 조립)</span></span></td>
</tr>
<tr>
<td style="text-align: center;"><b>구현 관점</b></td>
<td style="text-align: center;"><span><span>전체적인 기능 동작을 고려</span></span><br><span><span>↓</span></span><br><span><span>각 단계별로 기능을 구현</span></span></td>
<td style="text-align: center;"><span><span>필요한 속성의 객체를 설계</span></span><br><span><span>(보안성, 데이터, 함수 등)</span></span><br><span><span>↓</span></span><br><span><span>각 객체의 상호작용(절차)을 설계</span></span></td>
</tr>
<tr>
<td style="text-align: center;"><b>구성 요소</b></td>
<td style="text-align: center;"><b>함수</b></td>
<td style="text-align: center;"><b>객체</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>접근 제어</b></td>
<td style="text-align: center;">Public</td>
<td style="text-align: center;"><b>Public, Protected, Private</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>오버로딩, 다형성</b></td>
<td style="text-align: center;"><b>불가능</b></td>
<td style="text-align: center;">함수, 생성자, 연산자 등을 <b>오버로딩 가능</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>상속</b></td>
<td style="text-align: center;"><b>불가능</b></td>
<td style="text-align: center;"><b>가능</b>(Public, Protected, Private)</td>
</tr>
<tr>
<td style="text-align: center;"><b>보안성</b></td>
<td style="text-align: center;"><b>낮음</b></td>
<td style="text-align: center;"><b>높음</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>데이터 공유</b></td>
<td style="text-align: center;">모든 함수가 공유 가능</td>
<td style="text-align: center;"><b>객체 간 멤버함수로만 공유</b>&nbsp;</td>
</tr>
<tr>
<td style="text-align: center;"><b>Friend 함수</b></td>
<td style="text-align: center;">없음</td>
<td style="text-align: center;">C++에 있음</td>
</tr>
<tr>
<td style="text-align: center;"><b>가상 클래스, 가상 함수</b></td>
<td style="text-align: center;">없음</td>
<td style="text-align: center;">상속 개념 아래 존재함</td>
</tr>
<tr>
<td style="text-align: center;"><b>예시 언어</b></td>
<td style="text-align: center;"><b>C</b>, Visual Basic, Fortran, Pascal</td>
<td style="text-align: center;"><b>C++, Java</b>, VB.NET, C#, <b>Python</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>장점</b></td>
<td style="text-align: center;"><b>설계하기 좋음</b></td>
<td style="text-align: center;"><b>구조를 파악하기가 좋음</b><br><b>코드를 절약</b>할 수 있음</td>
</tr>
<tr>
<td style="text-align: center;"><b>단점</b></td>
<td style="text-align: center;"><b>구조가 복잡</b>해지고 <b>중복 코드를 작성</b>할 수 있음</td>
<td style="text-align: center;">오버헤드를 최적화 하지 않으면 <b>상대적으로 느려짐</b></td>
</tr>
<tr>
<td style="text-align: center;"><b>용도</b></td>
<td style="text-align: center;"><b>한정된 자원</b><br><b>초기부터 설계</b></td>
<td style="text-align: center;"><b>큰 규모</b><br><b>잦은 협업</b><br><b>생산성 중시</b></td>
</tr>
</tbody>
</table>

*[테이블 출처](https://blackvill.tistory.com/221)*