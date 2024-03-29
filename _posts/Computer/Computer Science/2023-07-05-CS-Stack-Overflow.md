---
title:  "스택오버플로우(Stack Overflow)란"
excerpt: "스택오버플로우(Stack Overflow)란 무엇일까"

categories:
  - Computer
tags:
  - [Computer, 스택오버플로우, StackOverflow]

toc: true
toc_sticky: true

date: 2023-07-05
last_modified_at: 2023-07-05
---

Stack Overflow는 Stack영역의 메모리가 지정된 범위를 넘어갈 때 발생한다. 

보통 함수에서 지역 변수를 선언하게되면 Stack이라는 메모리 영역에 할당되는데, 함수들이 호출될 때마다 각 함수에 선언된 지역 변수들은 Stack에 할당되었다가 해제된다.

그러다 해당 변수의 크기가 Stack보다 크거나, 함수를 무한으로 호출하고 있거나, Stack을 넘어가 다른 곳에 위치하고 있는 경우 **Stack Overflow**가 발생한다.

1. 해당 변수의 크기가 Stack보다 큼

2. 함수를 무한으로 호출

3. Stack을 넘어가 다른 영역에 위치함

# 스택오버플로우 해결방법
스택오버플로우를 해결하려면 위의 3가지를 반대로만 해주면 된다.

1. 해당 변수의 크기를 Stack보다 작게 만듬

2. 함수 무한 호출을 막음

3. 존재하지 않는 인덱스나 주소를 지정하고 있지는 않은지 확인

4. Stack이 아닌 Heap에 할당하기
동적할당을 사용해 저장하게 되면 Stack이 아닌 Heap에 저장하게 된다.

5. Stack의 크기 조절하기
Stack의 크기를 직접 늘려주어서 ~~해당 변수의 크기보다 스택의 크기를 늘려주면 된다~~

# 스택오버플로우 사이트

## [Stack Overflow](https://stackoverflow.com/)

개발을 하다보면 한 번쯤은 일어나게되는 오류여서 그런지, 해외에는 스택오버플로우라는 사이트 자체가 있다. 개발자들을 위한 커뮤니티로 보통 Q&A가 주를 이루는데, 재야의 고수분들이 열심히 답변을 달아주시고 게시판도 활성화가 잘 되어있는 편이라 개발자 커뮤니티중에서는 가장 유명하고 가장 이용자가 많다.