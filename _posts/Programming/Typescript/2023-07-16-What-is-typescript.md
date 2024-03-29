---
title:  "타입스크립트란?"
excerpt: "자바스크립트에 타입을 부여한 언어, 타입스크립트에 대하여"

categories:
  - Typescript
tags:
  - [Javascript, Typescript, 자바스크립트, 타입스크립트, 웹 개발]

toc: true
toc_sticky: true

date: 2023-07-16
last_modified_at: 2023-07-16
---

# 타입스크립트란?
타입스크립트<sup>Typescript</sup>란 자바스크립트에 **타입**을 부여한 언어이다. 자바스크립트를 공부하다보면 알텐데, 자바스크립트는 유명한 언어들과는 달리 신기한 오류들이 많다.

```js
> typeof NaN
< "number"
```

```js
> 0.5 + 0.1 == 0.6
< true

> 0.1 + 0.2 == 0.3
< false
```

문법이 널널한 대신에, 널널한 만큼 오류가 많다

그래서 만들어진게 타입스크립트고, 자바스크립트의 **확장된 언어**라고 보면 된다.

타입스크립트는 자바스크립트와 달리 브라우저에서 파일을 한번 컴파일해주어야한다.

# 자바스크립트 대신 타입스크립트를 쓰는 이유

## 에러의 사전 방지
타입스크립트는 자바스크립트와는 다르게 에러를 사전에 방지할 수 있다.

``a+b``라는 코드가 있을 때, 자바스크립트라면 a=10, b=10 일 때 20을, a='10', b='10'일 때 1010을 반환한다.

사용자에게 입력을 받아 코드를 숫자로 변환하는 과정을 거치지 않는다면 데이터베이스가 혼란해지고 말 것이다.

그렇기에

```ts
function sum(a: number, b: number){
    return a+b;
}
```

라고 타입스크립트에서 정의해주면 a='10', b='10'일 때 컴파일 과정에서 오류를 확인하고 수정할 수 있다.

## VSCODE
타입스크립트는 개발 툴의 기능을 최대로 활용할 수 있다. 변수에 대한 타입이 지정되어 있다면 VSCode에서는 해당 타입에 대한 API를 미리 보기로 띄워줄 수 있어 API를 일일이 치지 않고 자동완성기능을 활용할 수 있고 오탈자를 예방할 수 있다.