---
title:  "자바스크립트(JavaScript) - 해당 날짜의 요일 구하기"
excerpt: "자바스크립트에서 날짜의 요일을 구하는 방법에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, getWeekday, 요일 구하기]

toc: true
toc_sticky: true

date: 2023-09-25
last_modified_at: 2023-09-25
---

```js
function getWeekday(sDate) {

    var yy = parseInt(sDate.substr(0, 4), 10);
    var mm = parseInt(sDate.substr(5, 2), 10);
    var dd = parseInt(sDate.substr(8), 10);

    var d = new Date(yy,mm - 1, dd);
    var weekday=new Array(7);
    weekday[0]="일";
    weekday[1]="월";
    weekday[2]="화";
    weekday[3]="수";
    weekday[4]="목";
    weekday[5]="금";
    weekday[6]="토";

    return weekday[d.getDay()];
}
```