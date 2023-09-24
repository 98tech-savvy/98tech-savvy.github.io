---
title:  "자바스크립트(JavaScript) - 쿼리스트링(Query String) 가져오기"
excerpt: "자바스크립트에서 URL의 쿼리스트링을 쉽게 가져오는 방법에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, URL, getURLParams, Query String, 쿼리스트링]

toc: true
toc_sticky: true

date: 2023-09-24
last_modified_at: 2023-09-24
---

아래 함수를 이용하면 자바스크립터에서 주소상으로 넘어오는 인자 값을 쉽게 파싱해서 사용할 수 있다. 리턴된 값 또한 JSON 이기 때문에 사용하기 편하다

```js
function getUrlParams() {     
    var params = {};  
    
    window.location.search.replace(/[?&]+([^=&]+)=([^&]*)/gi, 
    	function(str, key, value) { 
        	params[key] = value; 
        }
    );     
    
    return params; 
}
```
