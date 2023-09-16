---
title:  "자바스크립트(JavaScript) - 문자열 자르기 (substr, substring, slice)"
excerpt: "자바스크립트에서 문자열을 나누는 가장 기본적인 함수 3가지"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 문자열 자르기, substr, substring, slice]

toc: true
toc_sticky: true

date: 2023-09-17
last_modified_at: 2023-09-17
---

# 자바스크립트에서 문자열을 자르는 세 가지 방법
자바스크립트에서 문자열을 자르기 위해서는 ``substr(), substring(), slice()``함수를 사용하면 된다.

```js
str.substr(start[, length])
str.substring(indexStart[index, indexEnd])
str.slice(beginIndex[Index, endIndex])
```

## substr(Start, Length)
substr()함수는 시작 위치부터 해당 길이만큼 문자열을 자르는 아주 기본적인 함수이다.

## substring(Start, End)
substring()함수는 시작 위치부터 종료 위치까지 문자열을 자른다. 종료 위치를 지정하지 않을 경우에는 문자열의 끝까지 자른다.

1. ※ 주의 : substring()함수는 **종료 위치의 -1번째 인덱스까지 자른다**
2. ※ 주의 : substring()함수는 **음수를 대입하면 해당 값이 '0'으로 치환된다**

## slice(Start, End)
slice()함수는 기본적으로 substring()과 사용법이 동일하나, 음수를 자유롭게 사용할 수 있어서 뒤에서부터 문자열을 자를 수 있다.