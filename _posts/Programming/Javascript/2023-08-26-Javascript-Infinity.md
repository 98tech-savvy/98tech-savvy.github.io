---
title:  "자바스크립트(JavaScript) - 무한대(Infinity)란?"
excerpt: "자바스크립트의 무한대(Infinity)에 관해 알아보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, Infinity, 무한대]

toc: true
toc_sticky: true

date: 2023-08-26
last_modified_at: 2023-08-26
---

# 무한대(Infinity)
무한대(Infinity)는 자바스크립트 전역 객체의 프로퍼티(Property)이다. 그러므로 전역 범위에서 사용이 가능하다.

전역 객체의 프로퍼티인 Infinity는 양의 무한대(+∞)이며, 초기값은 Number.POSITIVE_INFINITY이다.

만약 Infinity 앞에 마이너스 기호(-)가 붙어있다면, 그것은 음의 무한대(-∞)를 의미하며, 초기값은 Number.NEGATIVE_INFINITY이다.

이 Infinity는 어떤 숫자를 0으로 나눌 경우의 반환값으로 나오는데, 만약 음수를 0으로 나눴을 경우에는 -Infinity가 나오게 된다.

# 무한대 연산
Infinity의 타입은 숫자(Number)이므로 연산이 가능하다.

# 무한대 체크 (Infinity Check)
만약 숫자가 유한대인지 확인하려면 ``isFinite()`` 와 Number 객체의 ``Number.isFinite()`` 메서드를 사용할 수 있다.

``isFinite()``는 확인하기 전에 타입을 숫자 형식으로 바꾼다. ``Number.isFinite()``는 숫자 형식으로 바꾸지 않고 확인을 한다.

```js
isFinite("100") => true
Number.isFinite("100") => false
```

Infinity는 셀 수 없는 무한대 숫자이므로 false를 반환한다.

```js
isFinite(Infinity); => false
Number.isFinite(Infinity); => false
```