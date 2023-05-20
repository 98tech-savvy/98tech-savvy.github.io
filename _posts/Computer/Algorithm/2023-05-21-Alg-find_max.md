---
title:  "[Alg] 최댓값을 구하는 알고리즘"
excerpt: "정해진 수 들중 최댓값을 구하는 알고리즘"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 최댓값 구하기, 최댓값 찾기]

toc: true
toc_sticky: true
 
date: 2023-05-21
last_modified_at: 2023-05-21
---

랜덤으로 만든 배열 arr의 첫 번째 값을 temp에 저장하고, temp에 저장한 값과 arr의 다음 인덱스 값을 비교해서 큰 값을 temp에 저장하는 식으로 만든 알고리즘

```python
import random

def main():
    arr = random.sample(range(1, 99), 10)
    print(arr)

    temp = arr[0]
    for idx, val in enumerate(arr):
        try:
            print(f"{idx} - 현재 값 : {temp} 비교 값 : {arr[idx+1]}")

            if temp < arr[idx + 1]:
                temp = arr[idx + 1]
            else:
                temp = temp     
        except:
            break

    print(f"가장 큰 값 : {temp}")
    

if __name__ == "__main__":
    main()

```