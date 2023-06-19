---
title:  "[Blog] 마크다운 문법 정리"
excerpt: "블로그 포스팅에 필요한 마크다운의 문법을 정리해보았다."

//현재 카테고리: Comptuer, Blog, Python
categories:
  - Blog
tags:
  - [blog, markdown, 마크다운, HTML, Posting]

toc: true
toc_sticky: true

date: 2023-04-03
last_modified_at: 2023-04-03
---
# 마크다운이란?
John Gruber에 의해 2004년에 만들어졌고 현재 가장 많이 쓰이는 인기있는 언어이다. 별도의 도구없이 작성이 가능하고 여러 형태로 변환이 가능하기 때문에 글들을 간단하게 기록하고 가독성을 높일 수 있는 강점이 부각된다.

# 마크다운 문법 정리
아래의 글은 [마크다운 가이드 사이트](https://www.markdownguide.org/)를 참고해서 만들었다.

## 헤더(Headers), \#
앞에오는 **\#** 의 갯수에 따라 그 문장의 글씨 크기가 달라진다. 제목, 부제등을 정할 때 사용하며, HTML의 \<h1>, \<h2> 등의 효과와 같다. 사용할 때에는 문장의 앞에 쓰고, 한 칸을 띄워서 사용한다.

<h1>＞Header size1 </h1>

|Markdown|HTML|
|---|---|
|\# Header size1 |\<h1>Header size1\</h1>|

<h2> ＞Header size2 </h2>

|Markdown|HTML|
|---|---|
|\# Header size2 |\<h2>Header size2\</h2>|

<h3> ＞Header size3 </h3>

|Markdown|HTML|
|---|---|
|\# Header size3 |\<h3>Header size3\</h3>|

<h4> ＞Header size4 </h4>

|Markdown|HTML|
|---|---|
|\# Header size4 |\<h4>Header size4\</h4>|

<h5> ＞Header size5 </h5>

|Markdown|HTML|
|---|---|
|\# Header size5 |\<h5>Header size5\</h5>|

<h6> ＞Header size6 </h6>

|Markdown|HTML|
|---|---|
|\# Header size6 |\<h6>Header size6\</h6>|

<br>

\#과 \##은 제목과 부제로 주로 사용되기 때문에, **대체 문법** 또한 있다. 문장의 아래에 **===** 와 **---** 를 사용해주면 된다.

<h1> ＞Header size1 </h1>

Header size1<br>
\===========

<h2> ＞Header size2 </h2>

Header size2<br>
\---------------------

## 줄바꿈(Line Breaks)

줄을 바꾸기 위해서는 \<br> 또는 줄의 끝에 두 번 이상의 스페이스(빈 칸)를 해주고 엔터를 눌러준다.

|Markdown|HTML|
|---|---|
|줄바꿈  <br>줄바꿈|줄바꿈\<br><br>줄바꿈|

## 굵게(Bold), \**

글자를 강조하기 위해 **굵은 글씨**를 사용하려면, 강조할 글자의 앞과 뒤에 \**로 감싸주면 된다.

|Markdown|HTML|
|---|---|
|\** 굵게 \**|\<strong> 굵게 \</strong>|

## 기울게(Italic), \*

글자를 *기울게* 하기 위해선 기울게 할 글자의 앞과 뒤에 \*로 감싸주면 된다.

|Markdown|HTML|
|---|---|
|\* 기울게 \*|\<em> 기울게 \</em>|

## 굵고 기울게(Bold Italic), \***

글자를 ***굵으면서 기울게*** 하고싶다면 단순하게 \***를 앞과 뒤에 넣어주면 된다.

|Markdown|HTML|
|---|---|
|\*** 굵고 기울게 \***|\<em>\<strong> 굵고 기울게 \<em>\<strong>|

## 취소선(Cancel Line)

글자에 ~~취소선~~ 을 추가하고 싶으면 글자의 앞과 뒤에 \~~를 추가해주면 된다.
```
~~취소선~~
```

## 하이라이트(Hightlight)

흔하게 허용되는 마크다운 문법은 아니다. 실제로 지금 블로그(Github)에서도 ==글자== 로 하이라이트 되진 않아서 HTML을 사용해서 표시하고 있다. 글자를 굵게 만드는 것도 좋지만 형광펜을 사용해 강조한 듯한 표시(하이라이트)를 주고싶다면, 글자의 앞과 뒤에 '\=='를 추가해주면 된다. 블로그에 포스팅 할 때 사용하고 싶다면 \<mark>내용\</mark>을 사용해주자.

오직 한 가지 우리가 두려워해야 할 
  일은 <mark>두려움 그 자체다</mark>. \- 루즈벨트

`` 오직 한 가지 우리가 두려워해야 할 
  일은 두려움 그 자체다. - 루즈벨트 ``<br>
`` 오직 한 가지 우리가 두려워해야 할 
  일은 두려움 그 자체다. - 루즈벨트 ``


## 블럭 인용(Blockquotes)
인용구를 블럭으로 감싸고 싶다면 \>를 사용하면 된다. 인용구 안에서는 다른 마크다운 문법도 사용할 수 있다.
>*도전한 뒤의 실패보다 <mark>아무것도 하지 않는 것을 두려워하라</mark>. - HONDA*

인용구는 겹치게 할 수 있는데, 인용구의 안에 다시 \>를 사용해주면 된다.
> 실패에 관한 인용구
>>*도전한 뒤의 실패보다 아무것도 하지 않는 것을 두려워하라. - HONDA*

## 목록(Lists)
순서를 매기기위해서 혹은 정렬하기위해서 사용하는 목록(Lists)은 **순서를 매기는 방식(Ordered Lists)**과 **순서가 없는 방식(Unorderd Lists)**으로 표현할 수 있는데. 순서를 매기는 방식은 1. 2. 3. 식으로 숫자로 순서를 매기고, 후자는 대쉬(-), 별표(*), 플러스(+) 등으로 목록을 나타낼 수 있다.

### 순서를 매기는 방식(Ordered Lists)

|Markdown|HTML|
|---|---|
|1. 첫 번째 <br>2. 두번째 <br>3. 세번째|<ol><br><li>첫 번째</li><br><li>두 번째</li><br><li>세 번째</li><br></ol>|

1. 첫 번째
2. 두 번째
3. 세 번째

### 순서가 없는 방식(Unordered Lists)

|Markdown|HTML|
|---|---|
|- 첫 번째 <br>- 두 번째 <br>- 세 번째|<ul><br><li>첫 번째</li><br><li>두 번째</li><br><li>세 번째</li><br></ul>|
|+ 첫 번째 <br>+ 두 번째 <br>+ 세 번째|<ul><br><li>첫 번째</li><br><li>두 번째</li><br><li>세 번째</li><br></ul>|
|* 첫 번째 <br>* 두 번째 <br>* 세 번째|<ul><br><li>첫 번째</li><br><li>두 번째</li><br><li>세 번째</li><br></ul>|
|* 첫 번째 <br>* 두 번째 <br>　* 두 번째의 첫 번째<br> 　* 두 번째의 두 번째<br>* 세 번째|<ul><br><li>첫 번째</li><br><li>두 번째</li><br><li>세 번째</li><br></ul>|

- 첫 번째
- 두 번째
  - 두 번째의 첫 번째
  - 두 번째의 두 번째
- 세 번째

## 코드블럭(Code Blocks)

개발자의 블로그라면 많이 사용하게 될 코드블럭(Code Blocks)이다. 기본적으로 4번의 스페이스바 또는 한 번의 탭을 쓰면 사용할 수 있다. **목록(List)** 안에 있을 경우는 8번의 스페이스바 또는 두 번의 탭을 사용하면 된다.

    <html>
      <head>
        <title>Code Blocks</title>
     </head>

백틱(\`)을 사용해서 단어나 문장을 코드로 나타낼 수 있다.<br>
\`코드 → `코드`

백틱을 안에 포함하려면 (\`\`)로 묶어준다.<br>
``Code `Code` Code``

(\`\`\`)를 사용하면 코드블럭을 좀 더 이쁘게, 문법을 강조하여 나타낼 수 있다.
(\`\`\`)로 코드를 묶고 그 뒤에 자신이 사용한 언어를 써주면 된다.

```python
  print("Hello Python!")
```

(\`\`\`)를 사용해서 강조할 수 있는 언어들은 다음과 같다.

|Markdown|Language|
|---|---|
|bash|Bash|
|cs|C#|
|cpp|C++|
|css|CSS|
|diff|Diff|
|html|HTML, XML|
|http|HTTP|
|ini|Ini|
|json|JSON|
|java|Java|
|javascript|JavaScript|
|php|PHP|
|perl|Perl|
|python|Python|
|ruby|Ruby|
|sql|SQL|

그 외 더 많은 언어는 [SUPPORTED_LANGUAGES](https://github.com/highlightjs/highlight.js/blob/main/SUPPORTED_LANGUAGES.md)를 참고하자.

## 수평선(Horizontal Rules)

단락을 구분지을 필요가 있을 때 사용한다. 별표(\*\*\*), 대쉬(\-\-\-), 언더바(\_\_\_)

---

***
___

## 링크(Links), \[]()

하이퍼 링크를 걸어줄 때 사용한다. 표시할 내용을 []로 감싸고 링크를 ()안에 넣어준다.
마크다운 문법을 사용할 수 있다.

이 글은 ***[마크다운 사이트](https://www.markdownguide.org/)***를 참고했다.<br>
``
이 글은 ***[마크다운 사이트](https://www.markdownguide.org/)***를 참고했다.
``

URL이나 E-mail을 넣고싶을 땐 <> 를 사용하면 된다.<br>
<98tech-savvy@gmail.com><br>
``
<98tech-savvy@gmail.com>
``
<https:/www.98tech-savvy.github.io><br>
``
<https:/www.98tech-savvy.github.io>
``

## 이미지(Images), \!\[]()

이미지를 표시하고 싶을 때 사용한다. **\!\[대체 텍스트]\(이미지 주소)**의 구조이며 추가로 **\!\[대체 텍스트]\(이미지 주소 "팝업 텍스트")**으로 사진의 팝업 텍스트를 설정할 수 있다.

![새](https://cdn.pixabay.com/photo/2023/03/25/16/02/hummingbird-7876355_960_720.jpg "귀여운 새")

``
![새](https://cdn.pixabay.com/photo/2023/03/25/16/02/hummingbird-7876355_960_720.jpg "귀여운 새")
``

## 마크다운 문법을 표시하기(Escaping Character), \\

게시글을 작성할 때 마크다운 문법을 표시하기 위해서는 마크다운 문법의 앞에 **'\\'** 를 붙여주면 된다.

**굵게**
`**굵게**`

\*\*굵게\*\*
`\*\*굵게\*\*`
## HTML
수 많은 마크다운 응용 프로그램에서 마크다운 형식의 텍스트에 HTML 태그를 적용할 수 있다. 특정 HTML 태그가 마크다운 문법보다 표현하기 쉽다면 HTML 태그를 사용하는 것이 더욱 유용하다.

*추천하는 HTML 사용처 :  이미지 크기 조정, 텍스트 색상 지정 등*

## 표(Table)
테이블을 추가하려면 첫 번째 행에 열의 내용을 적어주고, 두 번째 행에 \|---|를 넣어서 열을 구분지어준다. 그리고 세 번째 행부터 차례대로 내용을 기입해주면 끝이다.

표에서는 대부분의 HTML태그를 사용할 수 없다(굵게, 기울게 등의 정도는 가능)
```
|내용|결과|
|---|---|
|지금은 4월이다|참|
|지금은 4월이 아니다|거짓|

```

|내용|결과|
|---|---|
|지금은 4월이다|참|
|지금은 4월이 아니다|거짓|

    
|---| 부분의 '---'의 왼쪽, 오른쪽, 양 옆에 ':'을 넣어주어 왼쪽 정렬, 오른쪽 정렬, 가운데 정렬을 할 수 있다.

```
|내용|결과|반대|
|:---|---:|:---:|
|지금은 4월이다|참|거짓|
|지금은 4월이 아니다|거짓|참|
```

|내용|결과|반대|
|:---|---:|:---:|
|지금은 4월이다|참|거짓|
|지금은 4월이 아니다|거짓|참|

## 체크리스트(Task Lists)
체크리스트(작업목록, 할 일 목록이라고도 함)를 사용해 확인 칸이 있는 체크리스트를 추가할 수 있다.
**빈 칸은 '- [ ]', 체크 칸은 '- [X]' 로 표시한다.**
- [ ] 공부를 안했는가
- [X] 포스팅을 썼는가
- [ ] 모니터를 보고있지 않은가

## 마치며
이렇게 마크다운 문법을 정리해보았다. 확실히 정리하며 알아간 부분이 많고 처음 쓸 때는 불편한 감이 있었는데 사용하면 사용할 수록 편리한 것 같다. 특히 코드블럭에 자동으로 문법 강조해주는 기능이 이뻐서 마음에 든다.