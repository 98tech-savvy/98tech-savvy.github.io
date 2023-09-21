---
title:  "자바스크립트(JavaScript) - 날짜형식의 문자열에 날짜 더하기 빼기"
excerpt: "자바스크립트에서 dateadd 함수를 활용해 날짜를 더하거나 빼보자."

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 문자열, 날짜 형식, 날짜 문자열, 날짜 더하기, 날짜 빼기]

toc: true
toc_sticky: true

date: 2023-09-22
last_modified_at: 2023-09-22
---

문자열이 날짜 형식(ex. '2023-09-21')으로 되어다면 문자열에 날짜를 더하거나 빼줄 수 있다.

```js
function date_add(sDate, nDays) {
    var yy = parseInt(sDate.substr(0, 4), 10);
    var mm = parseInt(sDate.substr(5, 2), 10);
    var dd = parseInt(sDate.substr(8), 10);
 
    d = new Date(yy, mm - 1, dd + nDays);
 
    yy = d.getFullYear();
    mm = d.getMonth() + 1; mm = (mm < 10) ? '0' + mm : mm;
    dd = d.getDate(); dd = (dd < 10) ? '0' + dd : dd;
 
    return '' + yy + '-' +  mm  + '-' + dd;
}
```