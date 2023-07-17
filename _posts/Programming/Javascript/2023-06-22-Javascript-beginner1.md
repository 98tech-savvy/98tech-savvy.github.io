---
title:  "자바스크립트 공부 정리"
excerpt: "자바스크립트 공부 정리"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Javascript
tags:
  - [HTML, CSS, 자바스크립트]

toc: true
toc_sticky: true

date: 2023-06-22
last_modified_at: 2023-06-22
---

# 자바스크립트의 비교연산자

<, >, <=, >=, =\==, !==

자바스크립트는 같은가? 를 ===로, 다른가? 를 !==로 표현한다.

# 동치 연산자의 종류

동치 연산자는 느슨한과 엄격한으로 나눌 수 있다.

느슨한 동치 연산자
==, != 같은 연산자를 말한다. 타입 비교 없이 값만 같으면 불리언 값을 출력한다.

엄격한 동치 연산자
=\==, !== 같은 연산자를 말한다. 타입과 값이 같아야만 불리언 값을 출력한다.

# 자바스크립트의 조건문

if ~ else

```js
if(조건) {
    
} else {
    
}
```

if ~ elseif ~ else

```js
if(조건) {
     
} else if {

} else if {

} else {

}
```

예제

```js
const profile = {
    name : "철수",
    age : 12,
    school : "다람쥐초등학교"
}

if (profile.age >= 20) {
    console.log("성인입니다")
} else if (profile.age >= 8 && profile.age <=19){
    console.log("학생입니다") 
} else {
    console.log("어린이입니다")
}
```

# 진짜 같은 값, 거짓 같은 값

진짜 같은 값(Truthy)는 따로 거짓 같은 값으로 정의된 게 아니라면 전부 진짜 같은 값으로 평가된다.

|값|설명|
|--|---|
|false|키워드 false|
|0|숫자 zero|
|-0|음수 zero|
|0n| BigInt 라고 하며 불리언으로 사용될 경우 숫자와 같은 규칙을 따른다. 0n은 거짓 같은 값|
|""| 빈 문자열(string)|
|null|아무런 값이 없음|
|undefined|undefined - 원시값|
|NaN|NaN - 숫자가 아님|

# 반복문

반복문은 ``for (초기식; 조건식; 증감문) { 실행할 내용 }`` 으로 작성해주면 된다.

```js
for (let i=0; i<5; i=i+1){
    console.log("Hello")
}
```

증감식이 없어도 for 문을 쓸 수 있다

```js
for (let i=0; i<5;){
    console.log(i+"hello")
    i++;
}

VM67:2 0hello
VM67:2 1hello
VM67:2 2hello
VM67:2 3hello
VM67:2 4hello
```

\* 문자열 안에 변수를 집어넣는 방법
'문자열 ${변수} 중간의 변수' 

# 자바스크립트의 수학 객체

Math.max(num1, num2, ...) : 최댓값을 구한다
Math.min(num1, num2, ...) : 최솟값을 구한다
Math.random() : 0~1의 수를 랜덤으로 생성한다
Math.round(num) : num을 소숫점을 반올림한다
Math.ceil(num) : num을 소숫점을 올림한다
Math.floor(num) : num의 소숫점을 버린다

\* 랜덤 수를 생성하기
String(Math.floor(Math.random() * 100000)).padStart(6, "0")

.padStart : 자릿수 만큼 없으면 그 뒤에 값(여기선 "0")을 덧붙인다.

# DOM

**DOM<sup>Document Object Model</sup>**

document.getElementById("tagID").InnerText :
HTML파일에서."tagID"라는 id를 가진 태그를 선택해서.제어한다

# 함수

```js
function 함수이름(매개변수) {
    코드
}
```

# 화살표 함수

자바스크립트를 개발한 사람은 어지간히 귀찮은게 싫었나보다.

const hello = (name) => {
    코드
}

function 대신 => 라는 기호를 사용해주면 함수로 선언해줄 수 있다.. ㅋㅋㅋ

# 내장함수

자바스크립트의 내장함수

(시간 입력은 ms 단위로 입력)

1. 시간 지연 함수
setTimeout(func, time)

2. 시간 반복 함수
setInterval(func, time)
