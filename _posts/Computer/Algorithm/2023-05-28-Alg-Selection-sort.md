---
title:  "[Alg] 선택 정렬 알고리즘"
excerpt: "작은 수 부터 큰 수 순서로 배열하는 정렬 알고리즘을 만들어보자"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 선택 정렬, Selection sort, 정렬]

toc: true
toc_sticky: true
 
date: 2023-05-28
last_modified_at: 2023-05-28
---

# min 함수 활용

```python
def func(arr):
    temp = []
    for i in range(0, len(arr)):
        temp.append(min(arr))
        arr.remove(min(arr))

    return temp


def main():
    arr = [35, 9, 2, 85, 17]
    print(func(arr))
```

# 배열 하나로 바꾸기

```python
def func(arr):
    for i in range(0, len(arr)):
        min_idx = 0

        for j in range(i + 1, len(arr)):
            if arr[j] < arr[i]:
                min_idx = j
                arr[i], arr[min_idx] = arr[min_idx], arr[i]

    return arr


def main():
    arr = [35, 9, 2, 85, 17]

    arr = func(arr)
    print(arr)


if __name__ == "__main__":
    main()
```

# 알고리즘 분석

리스트 안의 자료를 한 번씩 비교해야하므로 O($n^2$) ($\frac{n(n-1)}{2}$ 이므로)