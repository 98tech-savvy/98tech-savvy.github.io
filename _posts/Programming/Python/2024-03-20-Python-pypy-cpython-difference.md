---
title:  "[Python] pypy3와 Python3(CPython)의 차이점"
excerpt: "Python3와 pypy3의 차이점에 대해 알아보자"

categories:
  - Python
tags:
  - [Python, 파이썬, CPython, 파이썬3, C파이썬, pypy3, 파이파이]

toc: true
toc_sticky: true

date: 2024-03-20
last_modified_at: 2024-03-20
---

# Python3(CPython)

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/9221ab17-7b7f-47a7-bb95-50bd38a68a5e)

Python3는 CPython이라고도 불리며 Python과 C로 구성된 언어이다. 그래서 특이하게 인터프리터 언어이면서 컴파일 언어인데, 개발자가 작성한 Python 코드를 byte code로 컴파일한 후에 이를 인터프리터가 실행하는 방식이다. 가장 널리 사용되며 Python 패키지, C 확장 모듈 & 호환성이 가장 높다. 일반적으로 오픈 소스 Python을 작성할 때 가장 기본적으로 사용한다.


# Pypy3

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/8506df5a-629f-471e-be1c-9409e8ddda47)

Python3 언어와 문법이 같지만 JIT 컴파일(Just-in Time Compile) 방식을 도입한 언어이다. JIT 컴파일이란 프로그램을 실행하기 전에 컴파일 하는 대신에, 실행하는 시점에 필요한 부분만 즉석으로 컴파일 하는 방식으로 자주 쓰이는 코드를 캐싱하는 기능이 있어서 인터프리터 언어의 느린 실행속도를 개선할 수 있다.

# Python3와 Pypy3의 차이점

1. 실행 속도
Pypy3는 JIT 컴파일 방식으로 반복적이고 복잡한 코드에서 Python3보다 더 빠른 실행속도가 나온다.

2. 호환성
대신 Pypy3는 실행 속도 향상을 위해 더 많은 메모리를 사용한다.

3. 메모리
CPython은 C 확장 모듈과 호환성이 높지만, Pypy3는 일부 C 확장 모듈에서 문제가 발생할 수 있다.

결과적으로 간단한 코드를 짤 때에는 Python3가 메모리, 속도, 라이브러리 호환 측면에서 우세하고 반복이 많은 복잡한 코드를 사용할 경우에는 Pypy3가 우세하다.