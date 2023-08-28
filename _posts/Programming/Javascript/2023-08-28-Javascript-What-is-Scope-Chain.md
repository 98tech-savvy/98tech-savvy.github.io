---
title:  "자바스크립트(JavaScript) - 스코프 체인(Scope Chain)"
excerpt: "자바스크립트의 스코프 체인(Scope Chain)에 관해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, Scope, 스코프]

toc: true
toc_sticky: true

date: 2023-08-28
last_modified_at: 2023-08-28
---

# 스코프(Scope)란?
[자바스크립트 - 스코프(Scope)](https://98tech-savvy.github.io/javascript/Javascript-What-is-Scope/) 게시글을 참고하자.

# 스코프 체인(Scope Chain)이란?
**스코프 체인(Scope Chain)**이란 일종의 리스트로서 전역 객체와 중첩된 함수의 스코프의 레퍼런스를 차례로 저장하고 **각각의 스코프가 어떻게 연결되고 있는지 보여주고 있는 것**을 말한다.

스코프 체인 이전에 자바스크립트의 **실행 컨텍스트(Execution Context)의 선행학습을 해보자**

## 실행 컨텍스트(Execution Context)
실행 컨텍스트는 **우리가 작성한 코드가 실행되는 환경**을 의미하고 총 두 가지 실행 컨텍스트가 존재한다

### 전역 실행 컨텍스트(Global Execution Context)
코드가 실행되기 이전에 생성이 되며, 함수 내에 없는 코드는 모두 이 **전역 실행 컨텍스트 안에 존재**한다. 무조건 **하나의 전역 실행 컨텍스트만이 존재**하며 어플리케이션이 종료될 때 까지 이 전역 실행 컨텍스트가 유지된다.

### 함수 실행 컨텍스트(Functional Execution Context)
전역 실행 컨텍스트가 생성된 이후에, 함수가 실행될 때 마다 새로운 실행 컨텍스트가 작성된다.

--------------------------

이 실행 컨텍스트는 **LIFO**, 즉 **Last In First Out**의 구조를 가진 스택의 형태이다.

엔진이 실행 컨텍스트가 실행되면 스코프 체인을 통해 **렉시컬 스코프(중첩된 함수 그룹에서 내부 함수가 상위 범위의 변수 및 기타 리소스에 액세스 할 수 있음, 함수를 어디서 선언했느냐에 따라 상위 스코프를 결정한다는 뜻)**를 먼저 파악한다.
