---
title:  "[Blog] jekyll 코드블럭 라인번호(line-number) 표시하기"
excerpt: "jekyll로 만든 블로그에 코드블럭에 라인번호 표시하고 복사 용이하게하기."

//현재 카테고리: Comptuer, Blog, Python
categories:
  - Blog
tags:
  - [blog, markdown, 마크다운, 코드블럭, 줄 번호, 라인넘버]

toc: true
toc_sticky: true

date: 2023-04-11
last_modified_at: 2023-04-11
---

# 라인넘버가 없는 불편함
![image](https://user-images.githubusercontent.com/128434645/231088585-7cf276b1-ef67-4691-a079-7c52e9f30c2c.png)
이와 같은 예제코드를 작성할 때, 왼쪽에 라인넘버<sup>line number</sup>표시가 없으면 무언가를 수정할 때도, 알려줄 때에도 힘들다. 저 코드블럭에 라인넘버를 어떻게 표시해줄 수 있을까?

# config.yml
jekyll을 사용해 블로그를 만들었으면 그 해당 테마에 config.yml이 있을 것이다. 그 config.yml을 열어주고

markdown ←을 검색해주던가 없으면

``` yml
markdown: kramdown
kramdown:
    syntax_highlighter: rouge
    syntax_highlighter_opts:
        block: 
            line_numbers: true
```

이 문구를 추가해주고 config.yml을 저장해주고 닫아준다.

# 라인넘버 복사 방지
내 블로그를 이용하는 사람들이나 내가 이후에 블로그 안의 코드를 사용할 일이 생겼을 때, 우리들은 보통 드래그-복사를 한다. 하지만 드래그를 해보면 라인넘버까지 같이 드래그되는 불상사가 있는데, scss파일을 설정해주면 라인넘버가 같이 드래그 되지 않는다.

이 설정은 **minimal mistakes theme**에서 진행했다.

위치 : ==_sass/minimal-mistakes/_syntax.scss==
에 ==/* line numbers*/== 구문을 수정해준다.

``` sass
    /* line numbers*/
    &.gutter,
    &.rouge-gutter {
      padding-right: 1em;
      width: 1em;
      color: $base04;
      border-right: 1px solid $base04;
      text-align: right;
    }
```
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
``` sass
    /* line numbers*/
    &.gutter,
    &.rouge-gutter {
      padding-right: 1em;
      width: 1em;
      color: $base04;
      border-right: 1px solid $base04;
      text-align: right;
      
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      -khtml-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
```