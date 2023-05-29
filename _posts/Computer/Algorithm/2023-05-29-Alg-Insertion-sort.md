---
title:  "[Alg] 삽입 정렬 알고리즘"
excerpt: "작은 수 부터 큰 수 순서로 배열하는 정렬 알고리즘을 만들어보자"

categories:
  - Algorithm
tags:
  - [Algorithm, 알고리즘, 선택 정렬, Selection sort, 정렬]

toc: true
toc_sticky: true
 
date: 2023-05-29
last_modified_at: 2023-05-29
---

# 삽입 정렬 알고리즘

```python
def find_val_pos(arr, value):
    for i in range(0, len(arr)):
        if value < arr[i]:
            return i

    return len(arr)


def insertion_sort(arr):
    result = []
    while arr: # arr의 배열이 남아있는 동안
        value = arr.pop(0) # arr의 배열에서 한 개(첫 번째 인덱스)를 빼주고
        value_pos = find_val_pos(result, value) #find_val_pos 함수에서 result 결과값에 value가 어떤 위치에 들어가야하는지를 계산한다
        result.insert(value_pos, value) # value_pos의 위치에 value를 result에 저장한다.

    return result


def main():
    arr = [35, 9, 2, 85, 17]

    print(insertion_sort(arr))


if __name__ == "__main__":
    main()
```

# 알고리즘의 동작 방식

``arr = [35, 9, 2, 85, 17]``인 배열 arr을 insertion_sort 함수로 호출해주면

1. 시작
<br>arr = [35, 9, 2, 85, 17]
<br>result = []

2. arr에서 첫 번째 값을 빼서 result에 넣는다
arr = [9, 2, 85, 17]
<br>result = [35]

3. arr에서 첫 번째 값을 빼서 result의 앞에 넣는다
<br>arr = [2, 85, 17]
<br>result = [9, 35]

4. arr에서 첫 번째 값을 빼서 result의 앞에 넣는다
<br>arr = [85, 17]
<br>result = [2, 9, 35]

5. arr에서 첫 번째 값을 빼서 result의 뒤에 넣는다
<br>arr = [17]
<br>result = [2, 9, 35, 85]

6. arr에서 첫 번째 값을 빼서 result의 9와 35사이에 넣는다
<br>arr = []
<br>result = [2, 9, 17, 35, 85]

7. arr이 비었으므로 종료함
<br>result = [2, 9, 17, 35, 85]

# 일반적인 삽입 정렬 알고리즘

```python
def ins_sort(arr):
    for i in range(1, len(arr)): # 1부터 n-1까지
        key = arr[i] # i번 위치 값을 key에 저장

        j = i - 1 # j를 i 바로 왼쪽 위치에 저장

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j] # 삽입할 공간이 생기도록 오른쪽으로 이동
            j -= 1
        
        arr[j + 1] = key # 찾은 위치에 key를 저장

```

# 전개 방식


현재 1번째
KEY : 9
J : 0
NOW ARRAY : [35, 35, 2, 85, 17]
NOW J : -1
반복문 탈출
RESULT ARRAY : [9, 35, 2, 85, 17]

현재 2번째
KEY : 2
J : 1
NOW ARRAY : [9, 35, 35, 85, 17]
NOW J : 0
NOW ARRAY : [9, 9, 35, 85, 17]
NOW J : -1
반복문 탈출
RESULT ARRAY : [2, 9, 35, 85, 17]

현재 3번째
KEY : 85
J : 2
반복문 탈출
RESULT ARRAY : [2, 9, 35, 85, 17]

현재 4번째
KEY : 17
J : 3
NOW ARRAY : [2, 9, 35, 85, 85]
NOW J : 2
NOW ARRAY : [2, 9, 35, 35, 85]
NOW J : 1
반복문 탈출
RESULT ARRAY : [2, 9, 17, 35, 85]

[2, 9, 17, 35, 85]


# 알고리즘 분석
특별한 경우를 제외하고 O($n^2$)