---
title:  "순차 탐색 알고리즘"
excerpt: "주어진 리스트에 특정한 값의 위치를 반환해주는 알고리즘, 선형 탐색(linear search) 알고리즘을 구현해보자"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 순차 탐색, linear search, 선형 탐색 알고리즘]

toc: true
toc_sticky: true
 
date: 2023-05-27
last_modified_at: 2023-05-27
---

리스트에 원하는 값의 인덱스(위치)를 반환해주는 알고리즘

```python
def func(arr, search_val):
    for idx, val in enumerate(arr):
        if arr[idx] == search_val:
            return idx

    return -1 # 값이 없을 때 -1

def main():
    arr = [17, 92, 18, 33, 58, 5, 33, 42]
    print(func(arr, 10000)) # -1
    print(func(arr, 92)) # 1 반환
```

최대 n번 비교를 해야하기 때문에 시간복잡도는 O(n)이다.

enumerate를 쓰기 싫다면 배열의 len값을 구해준 뒤 range(0, len(arr))로 범위를 지정하고 arr[i]로 비교를 하면 된다.