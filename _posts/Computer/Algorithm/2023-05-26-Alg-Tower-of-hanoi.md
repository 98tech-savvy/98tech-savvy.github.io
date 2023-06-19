---
title:  "[Alg] 하노이의 탑 옮기기 알고리즘"
excerpt: "n개의 원반을 가진 하노이의 탑을 옮기기 위한 원반 이동 순서를 출력하는 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 하노이의 탑, 원반 옮기기]

toc: true
toc_sticky: true
 
date: 2023-05-26
last_modified_at: 2023-05-26
---

[하노이의 탑 플래시게임](https://vidkidz.tistory.com/649) 사이트에서 하노이의 탑을 브라우저로 플레이 할 수 있다.

하노이의 탑 게임에는 규칙이 있다.

1. 큰 원반이 작은 원반보다 위에 있어서는 안된다
2. 한 번에는 하나의 원반만 옮길 수 있다

위의 규칙으로 첫 번째 기둥에서 마지막 기둥으로 원반들을 옮기면 게임을 클리어한다.

# 원반의 개수에 따른 움직임

## 원반 개수 - 1개

원반 개수가 1개라면, 단순히 1번 기둥에서 3번 기둥으로 옮기면 끝이다
`` 1 → 3``

## 원반 개수 - 2개

원반 개수가 2개라면,
```
1 → 2
1 → 3
2 → 3
```
의 과정을 거쳐야 마지막 기둥에 옮길 수 있다.

## 원반 개수 - 3개

```
1 → 3
1 → 2
3 → 2
1 → 3
2 → 1
2 → 3
1 → 3
```
의 과정을 거친다. 

## 원반 개수 - 4개

```
1 → 2
1 → 3
2 → 3
1 → 2
3 → 1
3 → 2
1 → 2
1 → 3
2 → 3
2 → 1
3 → 1
2 → 3
1 → 2
1 → 3
2 → 3
```
의 과정을 거친다.

## 원반 개수 - 5개

```
1 → 3
1 → 2
3 → 2
1 → 3
2 → 1
2 → 3
1 → 3
1 → 2
3 → 2
3 → 1
2 → 1
3 → 2
1 → 3
1 → 2
3 → 2
1 → 3
2 → 1
2 → 3
1 → 3
2 → 1
3 → 2
3 → 1
2 → 1
2 → 3
1 → 3
1 → 2
3 → 2
1 → 3
2 → 1
2 → 3
1 → 3
```

이렇게 계속 꾸역꾸역 원반의 개수를 늘려나가며 플레이할 수도 있겠지만, 진행되는 흐름이나 규칙을 찾는다면 좀 더 쉽게 플레이할 수 있을 것이다.

잘 보면 **원반 개수가 1개일 때를 제외**하고는, '원반의 개수-1개' 만큼의 원반들을 보조 기둥에 옮기고, 가장 큰 원반을 마지막 기둥에 옮긴 후에 다시 '원반의 개수-1개' 만큼의 원반들을 마지막 기둥에 옮기는 과정을 거치는걸 찾아낼 수 있다.

|원반의 개수|옮기는 횟수|
|--|--|
|1|1|
|2|3|
|3|3+1+3|
|4|7+1+7|
|5|15+1+15|

즉 $f(n) = 1 + 2f(n-1)$ 이라는 식이 나온다.

그리고 함수 안에 함수가 있는 형태이므로, 재귀함수의 형태다. 즉 재귀함수임을 인지하고 코드를 짜면 간단하게 구현해낼 수 있을 것이다.

(횟수는 차례대로 1, 3, 7, 15, 31이며 이는 $2^1-1, 2^2-1, 2^3-1, 2^4-1, 2^5-1$) 이다.

# 완성된 코드

```python
def hanoi(n, startpos, subpos, endpos):
    if n == 1: # n이 1일 때
        print(f"{startpos} → {endpos}")
        return

    # print(f"{startpos} -> {subpos}")
    # print(f"{startpos} -> {endpos}")
    # print(f"{subpos} -> {endpos}")

    hanoi(n - 1, startpos, endpos, subpos)
    print(f"{startpos} → {endpos}")
    hanoi(n - 1, subpos, startpos, endpos)
```

n이 1일 때(원반의 개수가 1개일 때) 첫 번째 기둥에서 마지막 기둥으로 옮긴다.
재귀함수를 통해 n이 1이 될 때까지 반복하며 ``print(f"{startpos} → {endpos}")``를 출력한다.

이 때

``hanoi(n - 1, startpos, endpos, subpos)`` 의 끝 기둥은 보조 기둥이고,
``hanoi(n - 1, subpos, startpos, endpos)`` 의 시작 기둥은 보조 기둥이다.

이해가 안 된다면 직관적으로 보면 이해가 단번에 될 것이다.

예를 들어 hanoi(4, 1, 2, 3) 을 호출해보겠다.

```
※ 참고 ※
hanoi(n, 1, 2, 3)
  hanoi(n - 1, start, end, sub)
  print(f"{startpos} → {endpos}")
  hanoi(n - 1, sub, start, end)
-------------------------------------
1.hanoi(4, 1, 2, 3)
  2.hanoi(3, 1, 3, 2)
    3.hanoi(2, 1, 2, 3)
      4.hanoi(1, 1, 3, 2)
        5.print(f"{1} → {2}")
      4.print(f"{1} → {3}")
      4.hanoi(1, 2, 1, 3)
        5.print(f"{2} → {3}")
    3.print(f"{1} → {2}")
    3.hanoi(2, 3, 1, 2)
      4.hanoi(1, 3, 2, 1)
        5.print(f"{3} → {1}")
      4.print(f"{3} → {2}")
      4.hanoi(1, 1, 3, 2)
        5.print(f"{1} → {2}")
  2.print(f"{1} → {3}")
  2.hanoi(3, 2, 1, 3)
    3.hanoi(2, 2, 3, 1)
      4.hanoi(1, 2, 1, 3)
        5.print(f"{2} → {3}")
      4.print(f"{2} → {1}")
      4.hanoi(1, 3, 2, 1)
        5.print(f"{3} → {1}")
    3.print(f"{2} → {3}")
    3.hanoi(2, 1, 2, 3)
      4.hanoi(1, 1, 3, 2)
        5.print(f"{1} → {2})
      4.print(f"{1} → {3}")
      4.hanoi(1, 2, 1, 3)
        5.print(f"{2} → {3}")
```
1 → 2
1 → 3
2 → 3
1 → 2
3 → 1
3 → 2
1 → 2
1 → 3
2 → 3
2 → 1
3 → 1
2 → 3
1 → 2
1 → 3
2 → 3

실제로 젤 처음 링크를 걸었던 플래시게임에 순서에 맞춰 놓으면 클리어 되는걸 볼 수 있다.

# 시간복잡도
위에서 짧게 괄호로 설명했듯이 횟수는 차례대로 1, 3, 7, 15, 31이며 이는 $2^1-1, 2^2-1, 2^3-1, 2^4-1, 2^5-1$이다. 즉 $2^n-1$ 이며 O($2^n$)이다. 