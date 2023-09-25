---
title:  "자바스크립트(JavaScript) - 쿠키(Cookie) Expires 쉽게 설정하기"
excerpt: "자바스크립트에서 쿠키셋팅 시에 expires를 일 수로 설정해보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, expires, 쿠키 셋팅, 쿠키 세팅, 쿠키 expires 설정]

toc: true
toc_sticky: true

date: 2023-09-26
last_modified_at: 2023-09-26
---

```js
function setCookie(name, value, days) {
        if (days) {
                var date = new Date();
                date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
                var expires = "; expires=" + date.toGMTString();
        } else {
               var expires = "";
        }
        
        document.cookie = name + "=" + value + expires + "; path=/";
}

 

function getCookie(name) {
        var i, x, y, ARRcookies = document.cookie.split(";");
        
        for (i = 0; i < ARRcookies.length; i++) {     
                x = ARRcookies[i].substr(0, ARRcookies[i].indexOf("="));
                y = ARRcookies[i].substr(ARRcookies[i].indexOf("=") + 1);
                
                x = x.replace(/^\s+|\s+$/g, "");

                if (x == name) {
                        return unescape(y);
                }
        }
}


```