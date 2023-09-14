---
title:  "자바스크립트(JavaScript) - 타입스크립트(TypeScript)처럼 코딩하기"
excerpt: "자바스크립트를 타입스크립트처럼 코딩하는 방법에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 타입스크립트, Typescript, 자바스크립트 타입스크립트처럼 코딩하기]

toc: true
toc_sticky: true

date: 2023-09-15
last_modified_at: 2023-09-15
---

# 타입스크립트처럼 코딩하는 방법
자바스크립트를 타입스크립트처럼 코딩하고싶다면, /** 를 사용해서 ``@param {type} 변수``의 형태로 작성해주면 된다.

```js
/**
 * 
 * @param {number} a
 * @param {number} b
 */

const add = (a, b) => {
  return a + b;
};
add(a, b)
```

# 타입스크립트처럼 검증하는 방법
처음에 ``// @ts-check``를 작성해주면 타입스크립트와 비슷한 검증을 진행한다.