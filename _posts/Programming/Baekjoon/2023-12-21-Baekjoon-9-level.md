---
title:  "백준 단계별로 풀어보기 정답 모아보기 - 약수, 배수와 소수"
excerpt: "백준 단계별로 풀어보기 9단계, 약수, 배수와 소수 문제 정답 총정리"

categories:
  - Baekjoon
tags:
  - [백준, Baekjoon, 프로그래밍 문제, 파이썬, 단계별로 풀어보기 9단계, 약수, 배수와 소수]

toc: true
toc_sticky: true

date: 2023-12-21
last_modified_at: 2023-12-21
---

# 5086 - 배수와 약수
```py
while True:
    num1, num2 = map(int, input().split(" "))
    if num1 + num2 == 0:
        break
    else:
        if num2 % num1 == 0:
            print("factor")
        elif num1 % num2 == 0:
            print("multiple")
        else:
            print("neither")
```

# 2501 - 약수 구하기
```py
# p를 q로 나누었을 때 나머지가 0이면 q는 p의 약수이다
# >> p % q == 0 -> True

N, K = map(int, input().split(" "))

arr = []
for i in range(1, N + 1):
    if N % i == 0:
        arr.append(i)

try:
    print(arr[K - 1])
except:
    print(0)
```

# 9506 - 약수들의 합
```py
# n이 자신을 제외한 모든 약수들의 합과 같으면, 그 수는 완전수이다.

while True:
    n = int(input())

    if n == -1:
        break
    else:
        arr = []
        temp = 0
        for i in range(1, n + 1):
            if n % i == 0:
                arr.append(i)
                temp += i
        temp -= n
        if n == temp:
            print(f"{n} = {arr[0]}", end="")
            for i in range(1, len(arr) - 1):
                print(f" + {arr[i]}", end="")
            print("")
        else:
            print(f"{n} is NOT perfect.")
```

# 1978 - 소수 찾기
```py
N = int(input())
arr = list(map(int, input().split(" ")))

resume = 0


def is_prime_number(x):
    for i in range(2, x):
        if x % i == 0:
            return False  # 소수 아님
    return True


for i in arr:
    if i == 1:
        continue
    if is_prime_number(i) == True:
        resume += 1
print(resume)
```

# 2581 - 소수
```py
import math

num_min = int(input())
n = int(input())
arr = [True for i in range(n + 1)]  # n만큼의 배열을 만들고 그 수를 전부 True로 채워줌

# 쉬운 방법에서 n의 제곱근(가운데 약수)만큼 확인해도 답이 나오는데 지장이 없어서 math.sqrt(n) 활용해 코드 개선
for i in range(2, int(math.sqrt(n)) + 1):
    if arr[i] == True:  # i가 소수일 때(남은 수)
        j = 2  # 배수
        while i * j <= n:
            arr[i * j] = False  # 수를 False로 바꿔줌
            j += 1

temp = []
for i in range(2, n + 1):
    if arr[i] and i >= num_min:
        temp.append(i)

if temp == []:
    print(-1)
else:
    print(sum(temp))
    print(temp[0])
```

# 11653 - 소인수분해
```py
import math

n = int(input())
prime_num = 2
while True:
    if n % prime_num == 0:
        n /= prime_num
        print(prime_num)
    else:
        prime_num += 1

    if n == 1:
        break
```