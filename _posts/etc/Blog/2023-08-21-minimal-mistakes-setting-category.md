---
title:  "minimal mistakes - 카테고리 세팅하기"
excerpt: "minimal mistakes 테마에서 원하는 카테고리를 넣어보자"

categories:
  - Blog
tags:
  - [Blog, Github, minimal mistakes, category]
toc: true
toc_sticky: true

date: 2023-08-21
last_modified_at: 2023-08-21
---

# navigation.yml

- 자신의 로컬 블로그 폴더(minimal-mistakes가 설치되어있는) > _data > navigation.yml

```yml
# main links
main:
  - title: ""
    url: 
  # - title: "About"
  #   url: https://mmistakes.github.io/minimal-mistakes/about/
  # - title: "Sample Posts"
  #   url: /year-archive/
  # - title: "Sample Collections"
  #   url: /collection-archive/
  # - title: "Sitemap"
  #   url: /sitemap/
```

이 곳은 블로그 우측 상단에 카테고리 탭이다. 나는 현재 사용하고 있지 않기 때문에 ""로 표시해두었지만, 우측 상단의 카테고리를 이용하고 싶다면 ``-title : ""``에 원하는 카테고리 이름을 적어주고, url을 상대주소(/page name/)로 넣어주면 된다.

# 페이지 수정
- 자신의 로컬 블로그 폴더(minimal-mistakes가 설치되어있는) > _pages > 페이지이름.md

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/d4f30110-4382-4ddf-a201-181c8e117ac6)

이렇게 좌측에 나오는 카테고리를 만들고 싶다면, _pages 폴더를 건드려주면 된다. 원하는 카테고리의 페이지 파일을 만들어주고 (ex. test.md)

```yml
---
title: "Test"
layout: archive
permalink: categories/test
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories.Test %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
```

## 건드려야 할 내용
1. title
""안에 원하는 제목을 넣어주자
2. permalink
permalink에 카테고리의 제목을 적어준다
3. assign posts
site.categories.의 뒤에 원하는 제목을 넣어준다

