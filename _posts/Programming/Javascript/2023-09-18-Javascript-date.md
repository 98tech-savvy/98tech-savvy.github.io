---
title:  "자바스크립트(JavaScript) - 현재 날짜, 시간 구하기"
excerpt: "자바스크립트에서 현재 날짜와 시간을 구하는 방법을 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 현재 날짜, 시간 구하기, date, format]

toc: true
toc_sticky: true

date: 2023-09-18
last_modified_at: 2023-09-18
---

# 현재 날짜, 시간 구하기

```js
var today = new Date();

console.log(today);
```

``결과 : Mon Sep 18 2023 00:57:40 GMT+0900 (한국 표준시)``

Date 객체를 활용하면 현재 시스템의 날짜를 가져와서 출력할 수 있지만, 평상시의 날짜 포맷으로 나오지 않기 때문에 year, month, day를 구해 날짜 포맷을 만들어주면 된다.

```js
var today = new Date();

var year = today.getFullYear();
var month = ('0' + (today.getMonth() + 1)).slice(-2);
var day = ('0' + today.getDate()).slice(-2);

var dateString = year + '-' + month  + '-' + day;

console.log(dateString);
```

``결과 : 2023-09-18``

시간 포맷 또한 다르지 않다

```js
var today = new Date();   

var hours = ('0' + today.getHours()).slice(-2); 
var minutes = ('0' + today.getMinutes()).slice(-2);
var seconds = ('0' + today.getSeconds()).slice(-2); 

var timeString = hours + ':' + minutes  + ':' + seconds;

console.log(timeString);
```