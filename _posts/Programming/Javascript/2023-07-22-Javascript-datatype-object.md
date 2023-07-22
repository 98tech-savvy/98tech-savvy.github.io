---
title:  "자바스크립트(JavaScript) 변수와 데이터타입, 객체"
excerpt: "자바스크립트의 데이터타입과 객체에 대해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 데이터타입, 객체]

toc: true
toc_sticky: true

date: 2023-07-22
last_modified_at: 2023-07-22
---

HTML은 웹 페이지를 구성하는 제일 기본적인 틀이고
CSS는 그 틀을 꾸며주는 마크업 언어이다.
그리고 JavaScript는 그 페이지를 동적으로 작동할 수 있게 도와주는(꾸며주는) 언어이다.

JavaScript를 개발할 때에는 VSCode, Chrome 개발자 도구 등을 사용하는데, Chrome 개발자 도구는 브라우저에 자바스크립트가 내장되어 있어서 쉽게 사용이 가능하다.

console.log() 로 콘솔에 ()안의 내용을 표시해 줄 수 있다. 이 때 사칙연산과 변수를 사용 가능하다.

# 변수

변수에는 var, let, const가 있다.

현재에는 var를 쓰지 않는다. 이유는 후술

변수 선언은 ``let 변수이름; const 변수이름;`` 으로 가능하다.

## 재할당과 재선언

||재할당 가능|재선언 가능|
|--|----|----|
|var|O|O|
|let|O|X|
|const|X|X|

재할당이 가능하다는 뜻은

```js
var text1 = 'nice'
console.log(text1)
var text1 = 'javascript'
console.log(text1)
```

라고 할 때

```js
>> nice
>> javascript
```

를 출력한다. 변수 text1을 '재할당' 한 것이다.

재선언은

```js
let text1 = 'nice'
let text1 = 'javascript'
```

라고 할 때 에러를 뿜는다. 그 이유는 위의 표에 let은 **재할당이 불가능**하다. 하지만

```js
let text1 = 'nice'
text1 = 'javascript'
```

는 가능하다. **재할당**은 아니지만 **재선언**을 해주어서 그렇다.

**const**의 경우 재할당과 재선언이 불가능하기 때문에 반드시 **선언과 동시에 초기화**해주어야 한다.

# 개발자끼리의 약속

1. 변수명은 동사가 아닌 명사로 선언한다
2. 첫 글자에는 숫자를 사용하지 않는다
3. 예약 키워드(new, break, do, if)는 변수의 이름으로 사용하지 않는다.
4. 변수 선언 방법 : 변수는 공백을 허용하지 않는다. 그렇기에 여러가지 방법으로 변수를 선언해준다.
    1. camelCase
        띄어쓰기 대신 대문자로 구분한다 (arrArray)
    2. PascalCase
        첫 글자도 대문자, 띄어쓰기 대신 대문자로 구분한다.
    3. snake_case
        언더바(_)를 사용해 띄어쓰기를 구분한다.

자바스크립트는 보통 camelCase로 구분한다.
        
# 데이터 타입
String, Number, Boolean, undefined, bull, symbol, Bigint, Object가 있다.

## String
문자열, 텍스트데이터를 의미한다(""와 ''로 문자열을 표현함)

## Number
모든 연산이 가능한 데이터(숫자) 타입이다. 가끔 NaN이라는걸 표시하는데 이 뜻은 **N**ot **a** **N**umber 라는 뜻으로 숫자가 아니라는 뜻이다.

# 배열과 객체

## Array
순서가 있는 데이터 집합을 저장할 때 사용한다.
let arr1 = ["e1", "e2"]

[]로 배열임을 알려준다.

이 때 e1과 e2는 arr1의 **요소**이며 이 값들은 고유한 **인덱스값(순서대로 0, 1, 2)**를 가진다. 인덱스값을 통해 요소에 접근할 수 있다.

### Property
데이터 타입마다 가지고 있는 고유한 속성을 나타낸다. ``Array.length``는 배열의 길이를 반환하는데, 이 때 시작하는 숫자는 1부터다.

### Method
어떠한 기능을 가지고 있는 명령어다.
``push(), pop(), indexOf(), includes()``등 자바스크립트에 내장되어있는 메소드가 있다.

1. push()
배열의 끝에 요소를 추가해준다
2. pop()
배열의 끝에 요소를 제거하고 그 요소를 반환한다
3. indexOf()
특정 배열에서 주어진 요소에 대한 인덱스를 반환한다
4. includes()
특정 배열에서 주어진 요소가 있는지 여부를 확인한다(이 때 반환값은 boolean)

### Object
 객체(Object)로 여러개의 프로퍼티(속성)을 가진 변수를 만들어낼 수 있음
```js
let userData = {
    name: "Jason",
    age: 25,
    gender: "Male"
};
```
여기서 name, age, gender가 property이다.
name: "Jason"에서 name은 Key, "Jason"은 Value 이다.

#### 객체의 데이터에 접근하는 방법

##### Dot notation
userData.name => "Jason"
userData.age => 25
객체.키 로 그 데이터에 접근하는 방법

##### Bracket notation
userData["name"] => "Jason"
userData["age"] => 25
객체["키"] 로 데이터에 접근할 수 있음

#### 객체 Method

##### Object.keys(userData)
객체의 모든 Key를 가져옴 ["name", "age", "gender"]


##### Object.values(userData)
객체의 모든 Value를 가져옴 ["Jason", 25, "Male"]