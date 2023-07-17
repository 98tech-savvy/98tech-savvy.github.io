---
title:  "컴퓨터가 용량을 표시하는 방식, Gib, Mib, Gb, Mb"
excerpt: "당연히 1Gb면 1024Mb아니야? 1Gb는 1000Mb입니다. 잘못된 표기로 인해 혼란스러운 사람들을 위해 용량의 표기 방식을 정리해보았다."

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Computer
tags:
  - [Computer, 용량의 표기 방법, Gib, Mib, Gb, Mb, Tb, Tib]

toc: true
toc_sticky: true

date: 2023-04-29
last_modified_at: 2023-04-29
---

# 포스팅을 하게 된 이유
여느 때와 다름없이 공부를 하며 '구글이시여 도와주시옵소서'하며 지식을 요구하다가 흥미로운 게시글을 보았다.

![image](https://user-images.githubusercontent.com/128434645/235011708-e1e4557c-5299-47f5-a98b-ac82c59f70b1.png)
*[출처, pgr21](https://www.pgr21.com/freedom/97915)*

***'어? 그러네'***

책과 구글링으로 병행하며 컴퓨터과학을 공부하고 있던 내가 책에서 보이는 단위 Gib, Mib같은 단위를 볼 때마다 알고는 있었지만 아직도 Gb, Mb같은 단위가 더 보편적으로 쓰이는 느낌이라 책에서 보이는 단위가 어색했다. 그리고 생각해보니 컴퓨터와 관련이 없는 사람들은 10Gb면 10000Mb, 10MB면 10000Kb로 보겠구나(당연하게도)하는 생각이 들었다. 나도 잘못된 표기에 익숙한게 아니었더라면 10000으로 보았을 것이니까 말이다.

그리고 이건 관련 없는 사람들이 알지 못한게 문제가 아니라 IT업계가 표기를 이상하게 한 잘못이라는 것이 문제다. 표기를 잘못해놓고 알아주길바라는건 시험문제 잘못내놓고 맞춰주길바라는 것과 같다고 생각한다.

그래서 오늘은 Gib Mib같은 단위가 만들어지게 된 배경과 차이점에 대해서 알아보도록 하겠다.

# Kib, Mib, ... 누가 만들었는데?
키비바이트, 메비바이트, 기비바이트 등의 이름은 [IEC<sup>International Electrotechnical Commission</sup>, 국제전기기술위원회](https://iec.ch/homepage) 라는 곳에서 1998년 11월에 기존의 단위와의 혼동을 줄이기위해서(1998년에 혼동을 줄이기 위해서 만들었는데 아직까지 쓰고있다...) 만들어졌다.

혼동이라함은 위의 게시글처럼 1Gb라 표기된 걸 1024로 볼지, 1000으로 볼지는 사람마다 다르다는 것이다. 실제로 위 게시글의 작성자분도 그러한 컴플레인으로 고민하게 되신 것 같다.

>　
>**Kib, Mib 같은 단위들은 2진수(2의 제곱)의 단위고**
>**Kb, Mb 같은 단위들은 10진수(10의 제곱)의 단위다**
> 　

# 각각의 단위

|접두어|기호|단위|접두어|기호|단위|
|--|---|--|---|--|--|
|KiloByte|KB|$10^3$|KibiByte|KiB|$2^{10}$|
|MegaByte|MB|$10^6$|MebiByte|MiB|$2^{20}$|
|GigaByte|GB|$10^9$|GibiByte|GiB|$2^{30}$|
|TeraByte|TB|$10^{12}$|TebiByte|TiB|$2^{40}$|
|PetaByte|PB|$10^{15}$|PebiByte|PiB|$2^{50}$|
|ExaByte|EB|$10^{18}$|ExbiByte|EiB|$2^{60}$|
|ZettaByte|ZB|$10^{21}$|ZebiByte|ZiB|$2^{70}$|
|YottaByte|YB|$10^{24}$|YobiByte|YiB|$2^{80}$|

2진수들의 단위가 참 이쁘다. 10으로 떨어지는 단위들이 참 매력적인 것 같다.

Mib를 'MibiByte(미비바이트)' 라고 잘못 알고 계시는 분들이 많은데, 주변 접두어 Kibi와 Gibi, 그리고 Meb'i'가 어우러져서 오는 혼동으로 'MebiByte(메비바이트)'가 맞는 표기이다.

# 정리

앞으로는 KiB나 MiB같은 제대로 된 단위표기를 해줘서 혼동을 없애줬으면 좋겠다.

만약 포스팅을 보시는 분들 중에 제곱의 단위를 변환하고싶으신 분들은 편하게 구글의
[구글 데이터 크기 변환](https://www.google.co.kr/search?q=kb+kib+%EB%B3%80%ED%99%98&newwindow=1&dcr=0&sxsrf=APwXEdf0X_CUsl_SB_E1-YXoYYwCuvEm5w%3A1682639981713&ei=bQxLZJCYK4OB-AaV47BQ&ved=0ahUKEwjQgpSzosv-AhWDAN4KHZUxDAoQ4dUDCA8&uact=5&oq=kb+kib+%EB%B3%80%ED%99%98&gs_lcp=Cgxnd3Mtd2l6LXNlcnAQAzIFCCEQoAE6CggAEEcQ1gQQsAM6BQgAEIAEOgQIABAeOgYIABAFEB46CAgAEAgQHhAKOgYIABAIEB5KBAhBGABQ0wVY_g1g6w5oAnABeAGAAYcBiAGmB5IBAzEuN5gBAKABAcgBCsABAQ&sclient=gws-wiz-serp) 링크를 이용해주면 편할 것이다.