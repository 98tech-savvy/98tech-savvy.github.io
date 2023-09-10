---
title:  "[Python] main 선언하기"
excerpt: "main 부분을 명시해줘서 불필요한 작업 최소화시키기"

categories:
  - Python
tags:
  - [Python, 파이썬, main, 메인 선언, 메인 부분 명시]

toc: true
toc_sticky: true

date: 2023-09-11
last_modified_at: 2023-09-11
---
# __name__ 이란?
Python으로 개발을 하다보면 아래와 같은 조건문을 종종 볼 수 있다.

``if __name__ == '__main__': ...``

일단 Python에서 ``__name__`` 변수는 Python 프로그램, 즉 .py 파일마다 기본으로 생성되는 전역 변수로, 프로그램(모듈)의 이름을 뜻한다.

1. 프로그램 최상위 환경의 이름
2. Python 패키지의 ``__main__.py`` 파일

# 사용하는 이유
C언어 같은 프로그래밍 언어의 경우에는 ``main``함수를 따로 선언해주어 main 부분을 분리시켜준다. 하지만 Python에서는 ``main``함수나 클래스 선언을 하지 않기 때문에 프로그램이 외부 모듈을 호출할 경우에 전체 코드를 모두 실행시켜버린다. 이 때 ``if __name__ == '__main__': ...`` 구문을 사용해주면, 불필요한 여러가지 작업들은 최소화 해줄 수 있다.