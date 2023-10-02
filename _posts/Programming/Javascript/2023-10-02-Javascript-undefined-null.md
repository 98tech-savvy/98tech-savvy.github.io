---
title:  "자바스크립트(JavaScript) - undefined, null"
excerpt: "자바스크립트의 undefined와 null에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, undefined, \null]

toc: true
toc_sticky: true

date: 2023-10-02
last_modified_at: 2023-10-02
---

자바스크립트에는 '없음'을 나타내는 값이 두 가지가 존재한다. 바로 **undefined**와 **null** 인데 두 값의 의미는 같은 것 같지만 미세하게 다르고 사용하는 목적 또한 다르다.

1. undefined
우선 undefined의 경우 사용자가 명시적으로 지정할 수도 있지만 값이 존재하지 않을 때 자바스크립트 엔진이 자동으로 부여하는 경우가 있다. 사용자가 명시적으로 ``undefined``를 지정하는 경우는 달리 덧붙일 내용이 없어 넘어가고, **자바스크립트 엔진이 자동으로 부여하는 경우**에 대해 살펴봅시다.

자바스크립트 엔진은 사용자가 응당 어떤 값을 지정할 것이라고 예상되는 상황임에도 실제로는 그렇게 하지 않았을 때 undefined를 반환한다다. 다음 세 경우가 이에 해당한다

1. 값을 대입하지 않은 변수, 즉 데이터 영역의 메모리 주소를 지정하지 않은 식별자에 접근할 때
2. 객체 내부의 존재하지 않는 프로퍼티에 접근하려고 할 때
3. return 문이 없거나 호출되지 않은 함수의 실행 결과

```js
1 var a;
2 console.log(a) // undefined
3
4 var obj = { a: 1};
5 console.log(obj.b) // undefined
6
7 var func = function() {};
8 var c = func();
9 conosle.log(c) // undefined
 ```

위의 1번째 경우처럼 값을 대입하지 않은 경우에 대해 배열의 경우에는 조금 특이한 동작을 확인할 수 있다.

```js
1 var arr1 = [];
2 arr1.length = 3;
3 console.log(arr1); // [empty x 3]
4
5 var arr2 = new Array(3);
6 console.log(arr2); // [empty x 3]
7
8 var arr3 = [undefined, undefined, undefined];
9 console.log(arr3); // [undefined, undefined, undefined]
```

arr1, arr2의 경우 [empty x 3]이 출력되지만 undefined로 초기화한 arr3의 경우 출력값 자체가 다른것을 확인할 수 있다. 이처럼 '비어있는 요소'와 'undefined를 할당한 요소'는 출력 결과부터 다르다. '비어있는 요소'는 순회와 관련된 많은 배열 메서드들의 순회 대상에서 제외된다.

```js
1 var arr1 = [undefined, 1];
2 var arr2 = [];
3 arr2[1] = 1;
4
5 arr1.forEach(function (v,i)) { console.log(v, i); }); // undefined 0 / 1 1
6 arr2.forEach(function (v,i)) { console.log(v, i); }); // 1 1
7
8 arr1.map(function(v,i) { return v + i});             // [NaN,2];
9 arr2.map(function(v,i) { return v + i});             // [empty,2];
10
11 arr1.filter(function(v) { return !v; });             // [undefined]
12 arr1.filter(function(v) { return !v; });             // []
13
14 arr1.reduce(function (p,c,i) { return p + c + i },'' ); // undefined011
15 arr1.reduce(function (p,c,i) { return p + c + i },'' ); // 11
```

 arr2의 경우 각 메서드들이 비어있는 요소에 대해서는 **어떠한 처리도 하지 않고 건너뛰었음**

``undefined``의 경우 그 자체로 값이다. 비록 'empty'를 의미하긴 하지만 하나의 값으로 동작하기 때문에 이때의 프로퍼티나 배열의 요소는 고유의 키값이 실존하며 순회의 대상이 될 수 있다. 한편 사용자가 아무것도 하지 않은 채로 접근했을 때 자바 스크립트 엔진이 하는 수 없이 반환해주는 ``undefined``는 해당 프로퍼티 내지 배열의 키값 자체가 존재하지 않음을 알 수 있다. 값으로써 어딘가에 할당된 ``undefined``는 실존하는 데이터인 반면 자바스크립트 엔진이 반환해주는 ``undefined``는 무나 그대로 값이 없음을 나타낸다.
 
``var a``라는 구문에 의해 식별자 ``a``에 자동으로 ``undefined``가 '할당된다'고 소개하는 것이 일반적이다. 하지만 원래는 자바스크립트가 실제로 아무것도 할당하지 않고 끝나며, 이후 변수 ``a``에 접근하고자 할 때 비로소 ``undefined``를 반환하는 것이 맞다

2. null 
같은 의미를 가진 ``null``이라는 값이 별도로 있는데 굳이 ``undefined``를 써야 할 이유가 없다. '비어있음'을 명시적으로 나타내고 싶을 때는 ``undefined``가 아닌 ``null``을 쓰면 된다. ``null``은 애초부터 이런 용도로 만든 데이터 타입으로 이런 규칙을 따르는 한 ``undefined``는 오직 **'값을 대입하지 않은 변수에 접근하고자 할 때 자바스크립트 엔진지 반환해주는 값'**으로서만 존재한다.
 
추가로 ``null``은 한 가지 주의할 점이 있는데 ``typeof null``이 ``object``라는 점.
이는 자바스크립트 자체의 버그로 어떤 변수의 값이 ``null``인지 여부를 판별하기 위해서는 ``typeof`` 대신 다른 방법으로 접근해야 한다.

 
```js
1 var n = null;
2 console.log(typeof n);         // object
3
4 console.log(n == undefined);   // true
5 console.oog(n == null);        // true
6
7 console.log(n === undefined);  // false 
8 console.log(n === null)        // true
```