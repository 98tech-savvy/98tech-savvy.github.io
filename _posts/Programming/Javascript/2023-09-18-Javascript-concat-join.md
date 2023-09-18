---
title:  "자바스크립트(JavaScript) - 문자열 합치기"
excerpt: "자바스크립트에서 문자열을 합치는 방법을 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 문자열 합치기, concat, join]

toc: true
toc_sticky: true

date: 2023-09-19
last_modified_at: 2023-09-19
---

# 문자열 합치기
자바스크립트에서 문자열을 연결할 때에는 '+' 연산자 혹은 ``concat()``함수를 사용하고 배열의 문자열을 합칠 때는 ``join()``함수를 사용한다.

# '+' 연산자
```js
var str = '98tech' + 'savvy';
```

str의 문자열은 '98techsavvy'로 저장된다.

피연산자는 여러개여도 상관없다. ``'98' + 'tech' + 'savvy'``

# concat()
```js
var str1 = '98tech';
var str2 = 'savvy';

var res = str1.concat(str2);
```

``res >> '98techsavvy'``

빈 문자열로도 합치기가 가능하다 ``var res == ''.concat('98tech', ' ', 'savvy');``

# join
```js
var langs = ['Python', 'Javascript', 'Java'];
var res = langs.join();
```

``res >> 'Python,Javascript,Java'``

``join()``함수는 배열의 문자열을 합치나 사이에 구분자를 넣어서 합친다. ``join()``함수의 인자에 아무것도 넣지 않으면 쉼표(,)를 넣어서 합친다
