---
title:  "자바스크립트(JavaScript) - 2차원 배열 만들기"
excerpt: "자바스크립트에서 트릭을 사용해 없는 2차원 배열을 만들어보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 2차원 배열, two dimensional array]

toc: true
toc_sticky: true

date: 2023-09-20
last_modified_at: 2023-09-20
---

자바스크립트는 **제대로 된 2차원 배열**은 없다(``var arr = [][];``같은 코드는 없다). 하지만 약간의 트릭을 통해 2차원 배열과 **비슷한 배열**을 만들어낼 수 는 있다.

# 2차원 배열 만들기

## 초기값 할당 방법
```js
var arr = [[1, 2], [3, 4], [5, 6]];
// arr[3][2]와 같다
```

## 반복문 사용 방법
```js
var arr = new Array(5);

for (var i = 0;i < arr.length; i++) {
  arr[i] = new Array(2);
}
```

## ES6 지원할 때
```js
// arr[5][2]
const arr1 = Array.from(Array(5), () => new Array(2)

// arr[5][2] (null)
const arr2 = Array.from(Array(5), () => Array(2).fill(null))
```