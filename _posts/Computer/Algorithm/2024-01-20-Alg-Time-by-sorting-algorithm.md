---
title:  "정렬 알고리즘 별 시간 복잡도 정리"
excerpt: "정렬 알고리즘에 대해 대략적인 시간 복잡도를 테이블로 정리해보았다"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 데이터 구조, 버블 정렬, 선택 정렬, 삽입 정렬, 퀵 정렬, 병합 정렬, 기수 정렬, 알고리즘 별 시간 복잡도]

toc: true
toc_sticky: true
 
date: 2024-01-20
last_modified_at: 2024-01-20
---

# 정렬 알고리즘에 따른 시간 복잡도
![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/6ba0328c-cdd4-4c8f-87da-d936303cbf6f)

|알고리즘|시간 복잡도|
|--|--|
|버블 정렬(Bubble Sort)|$O(n^2)$|
|선택 정렬(Selection Sort)|$O(n^2)$|
|삽입 정렬(Insertion Sort)|$O(n^2)$|
|퀵 정렬(Quick Sort)|$O(n^2)$|
|병합 정렬(Merge Sort)|$O(n\log n)$|
|기수 정렬(Bubble Sort)|$O(kn)$ k: 최대 데이터의 자릿수|
|Arrays.sort()|$O(n^2)$|
|Collections.sort()|$O(n\log n)$|

**최악**을 가정한 시간복잡도로, 보통 퀵 정렬이 병합 정렬보다 빠른 편이다(병합정렬이 메모리도 더 많이 잡아먹음).

# 시간 복잡도 문제의 일반적인 계산
보통 경우의 수가 10의 8승($10^8$) = 1초로 잡고 문제를 풀이한다.