---
title:  "자바스크립트(JavaScript) - 얕은 복사와 깊은 복사"
excerpt: "자바스크립트의 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 얕은 복사, 깊은 복사, Shallow Copy, Deep Copy]

toc: true
toc_sticky: true

date: 2023-09-13
last_modified_at: 2023-09-13
---

# 자바스크립트의 데이터 유형
자바스크립트의 기본 데이터 타입(원시 타입)에는 ``string, number, null, undefined, symbol``등이 존재한다. 참조형 데이터 타입으로는 ``Object, Array``등이 존재한다.

# 얕은 복사와 깊은 복사
얕은 복사와 깊은 복사는 참조 주소와 참조 공간의 차이로 나눌 수 있다. **참조 주소를 공유한다면 얕은 복사, 참조 공간을 복사한다면 깊은 복사**라고 생각하면 된다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/ca9a1d5e-168a-497f-81a0-89e4f0f76a63)

이해하기 쉽게 예를 들어보자.

```js
var a = 3;
var b = a;

b = 5;

console.log('a : ' + a);
console.log('b : ' + b);

결과
a : 3
b : 5
```

```js
var a = 3;
var b = a;
a = 1;

console.log('a : ' + a);
console.log('b : ' + b);

결과
a : 1
b : 3
```
위 두 가지 예제를 통해 **기본 데이터 타입**의 경우 복사 후 값을 변경해도 다른 변수에 영향을 주지 않음을 확인할 수 있다.

다음은 참조형 데이터 타입의 예제를 보자

```js
var arrA = ['a', 'b', 'c', 'd'];
var arrB = arrA;

console.log('arrA : ', arrA);
console.log('arrB : ', arrB);

-------------------
결과
arrA : ['a', 'b', 'c', 'd']
arrB : ['a', 'b', 'c', 'd']
-------------------

console.log('값 변경 후');

arrA[0] = 'b';
arrB[1] = 'c';
console.log('arrA : ', arrA);
console.log('arrB : ', arrB);

-------------------
결과
arrA : ['b', 'c', 'c', 'd']
arrB : ['b', 'c', 'c', 'd']
-------------------

```

기존 배열 arrA를 복사한 arrB의 값을 변경해도 arrA의 값에 영향을, arrA의 값을 변경해도 arrB의 값에 영향을 준다는 사실을 알 수 있다.

맨 처음의 예제(기본 데이터 타입)를 얕은 복사, 그리고 이후의 예제(참조 데이터 타입)를 깊은 복사의 예제로 들 수 있다.

# Reference
https://www.csharp411.com/c-object-clone-wars/