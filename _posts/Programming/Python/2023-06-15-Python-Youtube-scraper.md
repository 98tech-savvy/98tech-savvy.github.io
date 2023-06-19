---
title:  "[Python] 해당 유튜브 페이지의 댓글 스크래핑해보기"
excerpt: "Python을 활용해 유튜브 페이지의 댓글들을 스크랩해보았다."

categories:
  - Python
tags:
  - [Python, RPA, 업무자동화, Scarper, 스크랩, 크롤링, 스크래퍼, 유튜브, 유튜버 댓글 스크래핑]

toc: true
toc_sticky: true

date: 2023-06-15
last_modified_at: 2023-06-15
---

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/42a50b08-de7c-4200-942e-2910d4c439b0)

유튜브 페이지의 댓글을 스크랩하는 프로그램을 만들어보았다. 스크래핑에서 가장 중요한건 페이지의 로딩과 필요한 태그를 빨리 찾는 능력인 것 같다

기본 agent로 실행시키니 닉네임이 제대로 출력되지않아서 따로 agent를 설정해주었다.

위의 사진은 침착맨님의 영상으로 테스트한 엑셀파일.