---
title:  "자바스크립트(JavaScript) - 특정 문자 모두 바꾸기, replaceAll 메서드 추가하기"
excerpt: "자바스크립트에서 replace 대신 replaceAll을 추가해보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, replaceAll, replace, 특정 문자 모두 바꾸기]

toc: true
toc_sticky: true

date: 2023-09-27
last_modified_at: 2023-09-27
---

자바스크립트에서는 기본 내장된 ``replace`` 메서드를 활용해 문자 하나를 바꿀 수 있다. 그러면 특정 문자를 모두 바꾸고 싶다면 어떻게 해야할까? 2가지 방법이 있다.

# String prototype 메서드 추가
```js
//replaceAll prototype 선언 
String.prototype.replaceAll = function(org, dest) {     
	return this.split(org).join(dest); 
}  

//replaceAll 사용 
var str = "Hello World"; 
str = str.replaceAll("o","*"); 

alert(str);
```

``split``으로 "o"를 기준으로 여러가지 배열(Hell, W, rld)을 만들고 ``join``을 활용해 그 배열을 다시 문자열로 만들어준다.


# 정규식 사용
```js
var str = "Hello World"; 
str = str.replace(/o/g,"*"); 

alert(str);
```