---
title:  "자바스크립트(JavaScript) - 문자열에서 특정 문자의 개수 구하기"
excerpt: "자바스크립트에서 문자열의 특정 문자의 개수를 구하는 2가지 방법에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 문자열, 특정 문자, 특정 문자 갯수 구하기, split, match]

toc: true
toc_sticky: true

date: 2023-09-21
last_modified_at: 2023-09-21
---

자바스크립트를 활용해 문자열에 있는 특정 문자의 개수를 구하려면 어떻게 해야할까?
정답은 **split**과 **match**함수를 사용하는 것이다.
예제는 전부 쉼표(,)를 구하는 방법으로 진행하겠다

# split
```js
var str = '98,tech,savvy';
var cnt = str.split(',').length -1; // 구한 배열의 길이에서 -1을 해줘야 특정 문자의 개수가 나옴
```

> result ▷ 2

# match
```js
var str = '98,tech,savvy';
var cnt = str.match(/,/g).filter(function(item) { return item !== ''; }).length;
```

> result ▷ 2

``split`` 함수는 **특정 문자를 기준으로 문자열을 배열로 변환**하고
``match`` 함수는 **특정 문자를 추출하여 배열로 반환**한다.

``match`` 함수는 특정 문자가 없을 경우에 빈 배열을 반환하는데 이 때 ``filter``함수를 사용해 빈 배열을 제거해주면 원하는 값을 얻을 수 있다.