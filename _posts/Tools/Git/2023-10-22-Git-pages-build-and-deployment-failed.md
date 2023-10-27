---
title:  "[Git] Github 빌드 에러 - pages build and deployment failed"
excerpt: "깃허브 블로그가 빌드를 자꾸 실패한다. Liquid Exception: undefined method `gsub' for 10926:Integer in /_layouts/single.html"

categories:
  - Git
tags:
  - [Git, Blog, Github, pages build and deployment failed, 빌드 실패, "Liquid Exception: undefined method `gsub' for 10926:Integer in /_layouts/single.html"]

toc: true
toc_sticky: true

date: 2023-10-22
last_modified_at: 2023-10-22
---

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/c8582a38-cbee-4759-ba09-601204c0ba66)
~~*고치기 위한 수많은 흔적들*~~

블로그에 4월 1일부터 시작한 1일 1포스팅을 하던 도중, 이메일에 
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/f6f164f5-6f73-48ab-b174-52694a57da76)
이런 메일이 도착했다. 내용은 빌드가 실패했으니 살펴보라는 이메일..

아무것도 건들지않고 포스팅 파일만 업로드했을 뿐인데 갑자기 빌드를 실패해서 여러가지 가정을 해봤다.
<br>
1. 나도 모르는 새 어느 파일에 이상한 문자를 적음
2. jekyll이나 wsl이 업데이트되면서 에러를 뿜음
3. 파일의 형식이 잘못됨
<br>

일단 실패한 빌드내용을 살펴보았다.
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/25dc4217-1e33-4510-934d-18b395e241dd)
~~*그만 살펴보자*~~

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/1064f810-0e0c-40d5-be09-3b7694c57192)
<span style="color:red">
 *Liquid Exception: undefined method `gsub' for 10926:Integer in /_layouts/single.html*</red>

처음에 발견한 이 에러 코드가 문제라고 생각해서 구글링을 해보았는데 'undefined method 'gsub' ~ 까지의 문장은 있었으나 그 뒤의 문장과 해결책은 찾을 수 없었다. 해결책을 찾아보았다해도 내가 처한 상황이 아니었거나 적용되지않는 해결책이었다.


> 잘 모르겠다면 처음부터.

소중한 잔디가 심어진 내 레포지토리를 갈아버릴 순 없으니, 로컬 파일과 WSL을 초기화시킨뒤 전부 재설치하는 과정을 거쳤다. 하지만 그럼에도 해결은 되지않았다..<br><br>

## 해결
그래서 마지막 **3. 파일의 형식이 잘못됨**에 집중해보기로 했다. 그 전 날부터는 정상적으로 업로드됐던걸로 봐서는 전 날과 에러를 뿜던 날의 포스팅을 비교해보기로했다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/0b071d24-ce0d-4f3a-be73-fdf5d9c6c4ba)

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/ebcf9bd5-48fa-4d68-886a-9b6cf86fe87a)

사실 포스팅을 작성했을 때 ', 10926'의 주황색 하이라이트를 보며 약간의 의구심이 들긴했지만 설마 숫자 하나 태그에 못 적겠어 라는 안일함과 함께 휘발성 기억으로 날려보냈던게 생각이 났다.

그리고 숫자를 태그에서 지워주자..

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/ce075f92-189a-41ec-b5f0-09554fa290af)
~~*이렇게... 쉽게?*~~

해결은 되었지만 깃허브 빌드에 뜬 오류와 저 숫자의 상관관계를 모르겠다.