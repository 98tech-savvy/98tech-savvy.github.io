---
title:  "minimal mistakes - 구글 애널리틱스 사용하기"
excerpt: "구글 애널리틱스를 사용해 방문자 통계를 내보자"

categories:
  - Blog
tags:
  - [Blog, Github, minimal mistakes, analytics]
toc: true
toc_sticky: true

date: 2023-08-20
last_modified_at: 2023-08-20
---

블로그를 운영하면서 방문자 통계나 방문한 사이트를 추적하고 싶을 때 트래픽을 추적하고 보고하는 구글이 제공하는 웹 애널리틱스 서비스를 사용하면 된다.

# Google Analytics
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/25da16d4-1c35-4508-a4b9-bf4682a3ef5d)

[Google Analytics](https://analytics.google.com/analytics/web/) 에 구글 계정으로 로그인해주고 '측정시작'을 눌러준다

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/c4d325c1-f561-45c4-b6b8-798410d83941)

페이지에서 자신이 원하는 '계정이름'을 넣어주고 다음을 눌러준다

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/9abdd0a4-67b0-4435-b2c0-1ca0cbd8c672)
자신이 원하는 '속성 이름'을 정해주고 '보고 시간대'는 한국, 통화는 '대한민국 원(₩)'

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/a5673465-9cea-46f1-ba22-10ba1ba30626)

페이지에서 왼쪽 하단 톱니바퀴 모양 > 데이터 스트림 > 자신이 넣어둔 속성이름을 클릭해준다

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/306c7f68-5bec-4b36-87d3-0a7a0e4eeb6f)
위와 같은 화면이 나오는데, 측정ID를 복사해준다

이후 자신의 로컬 컴퓨터에 minimal-mistakes가 깔려있는 폴더에 들어가서 _config.yml파일을 열어준다.

그리고 찾기 기능을 활용해 Analytics 탭으로 가서

```yml
# Analytics
analytics:
  provider               : google-gtag # false (default), "google", "google-universal", "google-gtag", "custom"
  google:
    tracking_id          : 자신이 복사해둔 트래킹아이디
    anonymize_ip         : # true, false (default)
```

위와 같게 만들어준다. 이후 git push

잠시 뒤 구글 애널리틱스 페이지에 접속해보면 방문자 통계가 카운팅 되기 시작한다.