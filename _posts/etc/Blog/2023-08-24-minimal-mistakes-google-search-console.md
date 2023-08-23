---
title:  "minimal mistakes - 구글 검색에 블로그 노출시키기"
excerpt: "minimal mistakes 에서 구글 서치 콘솔을 활용해 자신의 블로그 포스팅을 구글에 노출시켜보자."

categories:
  - Blog
tags:
  - [Blog, Github, minimal mistakes, google search console, 구글 서치 콘솔, 블로그 노출, 구글 검색엔진, 미니멀 미스테이크]
toc: true
toc_sticky: true

date: 2023-08-24
last_modified_at: 2023-08-24
---

# Google Search Console
[Google Search Console](https://search.google.com/search-console/about)에 들어가준다. **'시작하기'**를 눌러주면 아래와 같은 화면이 나온다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/39fc6ad3-5f78-4fd1-aa01-16354b89d446)
도메인이 있다면 좌측의 [도메인]을 나처럼 github.io의 형태라면 [URL 접두어] 탭에서 자신의 블로그 주소를 써준다.
<br>

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/04fa6a3e-d5a9-435d-a6fc-48154d59cbf3)
그러면 위와 같이 주소의 소유권을 확인하기 위한 '확인 방법'이 여러 개 나타난다. 이 중 **권장 확인 방법인 'HTML 파일'**로 확인해보도록 하겠다.

``google~~~.html`` 파일을 받아주고 자신의 로컬 블로그 폴더에 파일을 넣어준다. 이 때 ``_config.yml``과 같은 경로에 위치시켜주면 된다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/e8555b3b-6a0b-467d-b218-0cabd665f5ba)
<br>

그리고 깃허브에 커밋해주고 파일이 올려질 때까지 잠시 대기한 후 확인 버튼을 눌러 확인해준다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/9d77be6d-60bb-4bc7-9977-71bf62771289)
위와 같은 화면이 나오면 성공.
<br>

그리고 Google 크롤러가 블로그의 파일들을 긁어갈 수 있게 sitemap.yml을 만들어준다. _config.yml이 있는 폴더에 ``sitemap.yml``이라는 빈 파일을 만들어주고 그 안에 아래의 내용을 집어넣는다.

```yml
---
layout: null
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    {% for post in site.posts %}
    <url>
        <loc>{{ site.url }}{{ post.url }}</loc>
        {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
        {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
        {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <priority>0.5</priority>
        {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
        {% endif %}

    </url>
    {% endfor %}
</urlset>
```

위와 동일한 위치에 ``robots.txt``를 만들고 아래의 내용을 집어넣는다
<br>

```yml
User-agent: *
Allow: /

Sitemap: https://자신의 블로그 주소/sitemap.xml
```
*자신의 블로그 주소에는 98tech-savvy.github.io와 같은 주소를 넣어준다*

깃허브에 커밋해준다.


<br>
커밋이 완료되면 자신의 구글 서치 콘솔로 돌아가서 색인생성 > Sitemaps로 들어가준다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/b8c8131d-28f3-4021-98d7-eb525b5e62bf)

아래와 같이 sitemap.yml 을 적어주고 제출 버튼을 클릭
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/93635c9e-85d0-4c7a-a915-7cf4d399db71)

아래의 [제출된 사이트맵]에 **성공**이라는 단어가 보인다면 끝.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/3e12e6c5-0f64-49d9-b4d2-f83c556ad7e7)

<br>

# 노출될 때 까지 걸리는 시간 소요
구글 검색에 실제로 노출될려면 짧게는 3-5일, 길게는 1달이 넘게도 기다리는 사람도 있다고 한다.