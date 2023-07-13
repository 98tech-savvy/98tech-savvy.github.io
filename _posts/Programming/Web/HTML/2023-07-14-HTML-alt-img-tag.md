---
title:  "웹 사이트 로딩을 빠르게, img 태그 대체하기"
excerpt: "img 태그를 대체해서 로딩 속도를 늘리는 방법을 알아보자"

categories:
  - HTML
tags:
  - [HTML, img태그 대체, alt img tag, loading speed]

toc: true
toc_sticky: true

date: 2023-07-14
last_modified_at: 2023-07-14
---

# 웹 사이트 최적화
우리들은 웹 사이트를 만들면서 페이지의 로딩 속도 최적화에 심혈을 기울인다. 여러 가지 파일이 많을수록 로딩 속도는 느려지고 복잡해질수록 페이지 자체가 무거워진다. 이 때 img 태그를 대체해서 로딩 속도를 빠르게 해보는 여러 방법에 대해 알아보자

# 1. Lazy loading
img 태그를 대체하는 것은 아니지만, img 태그에 속성을 추가해주는 방법이다

```html
<img src="img source" loading="lazy" />
```

``loading="lazy"`` 속성을 주면 이미지를 즉시 로드하지 않고, 유저가 이미지를 실제로 볼 때 로딩을 한다.

> 모든 이미지를 한꺼번에 로드하는 대신 각 이미지를 하나씩 가져오는 방식

이 방법을 사용할 때에는 이미지 크기를 최적화해줘야한다.

# 2. srcset
장치마다 로드할 이미지를 다르게 정의할 수 있는 방법이다.

화면의 크기에 따라, 해상도의 크기에 따라 이미지의 크기를 다르게 정의해주어서 화면에 따른 최적화를 해줄 수 있다.

```html
<img
    srcset="img-small.jpg 500w,
    img-medium.jpg 1000w,
    img-large.jpg 2000w"
    src="img-small.jpg" />
```

이런 식으로 코드를 짜주면, 너비500에 small, 너비1000에 medium, 너비2000에 large, 그리고 srcset을 지원하지 않는 브라우저에는 img-small.jpg를 적용한다

브라우저가 srcset 태그가 있는 경우 스스로 판단해 어울리는 이미지를 불러온다.

# 3. sizes
이미지가 다양한 화면 크기에 표시되는 방식에 대한 추가 정보를 브라우저에 제공할 수 있다.

```html
<img
    sizes="(max-width: 500px) 400px,
    (max-width: 1000px) 800px,
    1200px />
```
viewport 가 0~500px 일 때 이미지는 400px로
viewport가 501~1000px 일 때 이미지는 800px로
그 이상일 경우 1200px 를 반환한다.

# 4. picture

```html
<picture>
    <source srcset="/img-vertical.jpg" media="(orientation: portrait)">
    <source srcset="/img-horizontal.jpg" media="(orientation: landscape)">
    <img src="/img-default.jpg">
</picture>
```

이런 식으로 source와 img 를 자식 태그로 사용해 줄 수 있으며,

위의 코드는 orientation(방향)이 세로일 때 img-vertical.jpg를, orientation이 가로일 때 img-horizontal.jpg를, 그 외의 경우에는 img-default.jpg를 반환한다.

위 ``<picture>`` 태그를 사용하면 사용하는 조건에 맞는(다크 모드, 화면 최소 너비 등) 이미지를 표시해줄 수 있다.

# 5. 다른 확장자의 이미지 사용하기

기본적으로 이미지를 표시할 때에는 jpeg 파일을 사용한다. 그러나 이 jpeg파일 대신 다른 대체 확장자를 찾아서 파일의 크기를 줄인다면, 그 자체만으로 홈 페이지 최적화를 할 수 있다.

예를 들어 Jpeg XL, WebP, avif 등의 확장자가 있다.