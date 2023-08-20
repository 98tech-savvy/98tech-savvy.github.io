---
title:  "블로그에 유튜브 동영상 삽입하기"
excerpt: "마크다운 파일에 유튜브 동영상을 삽입하는 방법을 알아보자."

categories:
  - Blog
tags:
  - [Blog, Github, Youtube, Youtube Link, 유튜브]

toc: true
toc_sticky: true

date: 2023-07-12
last_modified_at: 2023-07-12
---

# 두 가지 방법

## 1. HTML 태그 사용
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/302e5746-4eb1-43d4-bb07-40384c6c561f)
동영상을 우클릭 하면 **[ <> 소스 코드 복사 ]** 라는 버튼이 나온다. 그 버튼으로 소스 코드를 복사한 후에 마크다운 파일에 붙여넣으면 끝.

<iframe width="1280" height="720" src="https://www.youtube.com/embed/ZMQbHMgK2rw" title="The Fastest Maze-Solving Competition On Earth" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 2. minimal-mistake 테마의 video-helper
**minimal-mistake theme** 에서는 video-helper 라는 편의기능이 있다. 

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/b164a829-1821-4899-b1c4-7dc24af585d2)

watch?v= 뒤의 주소를 복사 한 후에

```
{% include video id="ZMQbHMgK2rw" provider="youtube" %}
```

위의 코드를 마크다운 파일에 입력해주면 끝.

{% include video id="ZMQbHMgK2rw" provider="youtube" %}
