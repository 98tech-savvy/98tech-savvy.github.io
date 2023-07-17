---
title:  "HTML, CSS"
excerpt: "HTML, CSS"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Javascript
tags:
  - [HTML, CSS, 자바스크립트]

toc: true
toc_sticky: true

date: 2023-06-13
last_modified_at: 2023-06-13
---

# 컴퓨터 기본 지식

확장자 : 컴퓨터가 어떻게 인식해야 하는 지 알려주는 정보
부모/자식 관계 : 상위 폴더가 하위 폴더를 담고 있는 형태
형제 관계 : 폴더나 파일이 같은 Depth에 위치한 형태

src > commons > libraries, styles, types

src -> commons : 부모 -> 자식
libraries, styles, types : 형제

# HTML
**HTML<sup>HyperText Markup Language</sup>**은 웹을 이루는 가장 기초적인 구성 요소로, **마크 업 언어**이다. 여기서 마크업 언어란 **태그 등을 이용해 문서나 데이터 구조를 명기하는 언어**를 뜻한다.

HTML의 **요소(Element)**는 **열린 태그**와 **닫힌 태그**, **콘텐츠**로 이루어지는데, 태그들은 다양한 고유기능들을 가지고있으며 다음과 같은 구조를 가진다. 예를 들어

```js
<p>(열린 태그)This is content</p>(닫힌 태그)</sup>
```

와 같은 식이며, 몇몇의 특정한 태그들은 닫힌 태그가 없는 구조가 있다. 태그 안에 **속성<sup>Attribute</sup>**을 넣어서 특수한 속성을 추가해줄 수 있다.

태그는 **in-line**과 **block**으로 태그 자체의 사이즈 크기가 구분되곤하는데, block은 한 줄 전체(div, h1, hr, p), in-line은 그 태그가 지정한 크기만큼만(span, input, img, a) 자리를 차지한다.

## 종속 태그
select, ol, ul, table ... 등이 있음

ol : Oldered List
ul : Unoldered List

태그 단독으로 사용이 불가능하고 부모+자식 관계로 사용해야 사용이 가능한 태그

## HTML의 구조

```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>HTML Element</title>
  </head>
  <body>
    <p>Hello HTML!!</p>
  </body>
</html>
```

``<html></html>`` : 최상위 부모 요소(가장 위의 요소)

``<head></head>`` : document title, 외부 파일 참조, metadata 설정 등이 위치하며 브라우저에 표시되지않는 정보들을 가지고 있다고 보면 된다. 페이지 설명, CSS, 문자 집합 선언 등

``<title></title>`` : 페이지의 제목을 설정해준다.

``<body></body>`` :
페이지의 본문을 담당하며, 웹 브라우저에 출력하는 모든 요소가 위치하고있다
헤더(header)와 네비게이션(nav), 섹션(section)등이 들어간다.

예전에는 \<div> 태그로 모두 작동(지금도 작동함)했으나 단어를 구분해줘서 코드를 쉽게 이해할 수 있게 해 협업에 도움을 준다.

VSCODE에서 !를 입력하면 기본 html을 가져올 수 있다.
## Box Model

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/d9b4ded3-3b8c-4994-bcf5-9e42a10f1bfc)

모든 HTML의 요소들은 박스(box) 모양으로 구성되어있고, 보통 4가지로 HTML을 구분한다.

1. padding
content와 border 사이의 간격
2. border
content와 padding 주변을 감싸는 테두리
3. margin
border와 이웃 요소(주변 요소)사이의 간격
4. content
박스의 실질적인 내용

# CSS
CSS<sup>Cascading Style Sheets</sup>는 **스타일 시트 언어**로 HTML 요소를 좀 더 화려하게, 색감있게 꾸며주는데 사용한다. 화면에 어떻게 렌더링할지 정의해주는 언어라고 생각하면 된다.

**웹 페이지는 HTML(뼈대) CSS(살) Javascript(근육)으로 이루어진다고 생각하면 좋다.**

## CSS 기본 문법

### 단일 속성 지정
```css
선택자{
    속성: 값;
}
```
### 다중 속성 지정

```css
선택자{
    속성: 값;
    속성: 값;
    속성: 값;
    속성: 값;
}
```

## CSS 사용방법

### html 태그 속성에 입력
``<a style="background-color: #ffee55; color: #36e52k;">``
태그에 CSS 속성이 바로 기록되어 있어, 별다른 지정이나 연결이 필요하진 않으나
유지보수에 어렵다(태그 안에 속성이 많아질수록 번잡해지니)

- 장점
스타일 적용 태그 즉시 확인 가능

- 단점
한번에 하나의 태그에만 적용 가능
전체 코드 가독성 나쁨
관심사 분리 x

### \<style> 태그에 입력
태그와 CSS속성이 html내에서 분리되어 있어서 어떤 태그에 CSS 속성을 적용할 지 연결해준다.

유지보수 측면에서 유리하다

- 장점
전체 코드 가독성 향상
유지보수 용이

- 단점
태그와 CSS 연결 필요
관심사 분리 X

### CSS 파일 만들어 불러오기
태그와 CSS 속성이 파일로 분리되어 있어서 어떤 태그에 CSS 속성을 적용할 지 연결해주어야 함.

- 장점
전체 코드 가독성 향상
유지보수 용이
관심사 분리 O

- 단점
태그와 CSS 연결 필요

## CSS 선택자

- 전체 선택자
```css
* {
    color: rebeccapurple;
}
```

- 태그 선택자
```css
div {
    color: rebeccapurple;
}
```

- class 선택자
```css
.container {
    color: rebeccapurple;
}
```
class 선택자는 중복이 가능하다.

- id 선택자
```css
#userinfo {
    color: rebeccapurple;
}
```
고유의 id를 선택자로