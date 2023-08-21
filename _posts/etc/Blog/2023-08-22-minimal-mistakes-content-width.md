---
title:  "minimal mistakes - 본문 영역, 글자 크기 조절, 하이퍼링크 밑줄 제거"
excerpt: "minimal mistakes 테마에서 본문의 전체적인 영역크기와 글자의 크기를 조절하고 하이퍼링크의 밑줄을 제거해보자"

categories:
  - Blog
tags:
  - [Blog, Github, minimal mistakes, content width, 본문 영역, 글자 크기 조절, 하이퍼링크 밑줄 제거, 링크 밑줄 제거, 미니멀 미스테이크]
toc: true
toc_sticky: true

date: 2023-08-22
last_modified_at: 2023-08-22
---

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/f4b0918c-9fff-4d7a-9371-a3733c941078)

현재는 설정해둔 상태라 본문의 영역이 내가 편하게 읽을 수 있을만큼 넓지만, 기본의 minimal-mistakes는 아래와 같이 굉장히 짧다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/85e47013-003f-49fa-ac5b-d6be8372d3c5)

글자의 크기, 본문의 영역을 조절하고 싶다면

# 본문 크기 조절

## _variables.scss
- 자신의 로컬 블로그 폴더(minimal-mistakes가 설치되어있는) > _sass > _minimal-mistakes > _variable.scss

- _variable.scss 에서 "Grid" 찾기

```yml
/*
   Grid
   ========================================================================== */

$right-sidebar-width-narrow: 100px !default;
$right-sidebar-width: 210px !default;
$right-sidebar-width-wide: 260px !default;
```

본문의 너비가 아닌, 양쪽의 sidebar를 조절하는 구문이다. 직접적으로 아닌 간접적으로 본문의 크기를 넓혀준다.

# 글자 크기 조절

## _reset.scss
- 자신의 로컬 블로그 폴더(minimal-mistakes가 설치되어있는) > _sass > _minimal-mistakes > _reset.scss

```yml
html {
  /* apply a natural box layout model to all elements */
  box-sizing: border-box;
  background-color: $background-color;
  font-size: 18px;

  @include breakpoint($medium) {
    font-size: 18px;
  }

  @include breakpoint($large) {
    font-size: 18px;
  }

  @include breakpoint($x-large) {
    font-size: 18px;
  }

  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}
```

2023-08-22 기준으로 위쪽에서 7번째 줄에 위치한 html {} 코드에서 ``font-size``의 크기를 조절해주면 된다.

# 하이퍼링크 밑줄 제거

## _base.scss
- 자신의 로컬 블로그 폴더(minimal-mistakes가 설치되어있는) > _sass > _minimal-mistakes > _base.scss

a {
  text-decoration: none; // <-- 추가한 코드

  &:focus {
    @extend %tab-focus;
  }

  &:visited {
    color: $link-color-visited;
  }

  &:hover {
    color: $link-color-hover;
    outline: 0;
  }
}

a {} 코드에서 ``text-decoration: none;``을 추가해준다.