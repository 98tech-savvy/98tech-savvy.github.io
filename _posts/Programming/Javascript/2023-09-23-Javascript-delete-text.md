---
title:  "자바스크립트(JavaScript) - 문자열 공백 제거"
excerpt: "자바스크립트에서 문자열의 공백을 제거해보자."

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 문자열, 문자열 공백, 공백 제거]

toc: true
toc_sticky: true

date: 2023-09-23
last_modified_at: 2023-09-23
---

자바스크립트에서 문자열의 양쪽 공백을 제거하기 위해서는 ``trim`` 함수를 사용하면 된다.
문자열에 포함된 모든 공백을 제거하기 위해서는 ``replace`` 함수를 사용하면 된다.

# trim
```js
var str = '  자바 스크립트  ';
var str = str.trim();
 ```

> 결과 :  '자바 스크립트'

``trim`` 함수를 사용하면 문자열의 왼쪽과 오른쪽의 공백을 제거할 수 있다. 문자열 내부의 공백은 제거되지 않는다.

# replace

```js
var str = '  자바 스크립트  ';
var str = str.replace(/^\s+|\s+$/gm, '');
```

> 결과 : '자바 스크립트'

``replace`` 함수를 사용하여 문자열의 양쪽 공백을 치환하여 제거할 수 있다


앞의 공백 : ``str.replace(/^\s+/gm, '')``

뒤의 공백 : ``str.replace(/\s+$/gm, '')``

※ (g : 문자열이 한 줄인 경우, gm : 문자열이 여러 줄인 경우)
 
## replace 함수를 사용하여 문자열의 모든 공백 제거

```js
var str = '  자바 스크립트  ';
var str = str.replace(/(\s*)/gm, '');
```

> 결과 : '자바 스크립트'


문자열의 모든 공백이 치환되어서 제거된 것을 확인할 수 있다.

 

