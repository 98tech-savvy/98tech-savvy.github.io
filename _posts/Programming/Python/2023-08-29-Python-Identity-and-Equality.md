---
title:  "[Python] 동일성과 동등성"
excerpt: "동일성(is)와 동등성(==)의 차이점"

categories:
  - Python
tags:
  - [Python, 파이썬, 동일성, 동등성, Identity, Equality, is, ==]

toc: true
toc_sticky: true

date: 2023-08-29
last_modified_at: 2023-08-29
---


Python에서 값을 비교하려면 ``is``연산자 혹은 ``==``연산자를 사용한다.

- ``is` : **동일성(Identity)** 비교
객체가 할당된 메모리 공간(ID)이 동일한지 비교한다

- ``==`` : **동등성(Equality)** 비교
단순히 값이 같은지 비교한다.

아래와 같은 코드로 이해를 쉽게 해보자.

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a is b)
print(a == b)

--------------
False
True
```

``a is b``는 메모리 공간에 a가 할당된 공간과 b가 할당된 공간이 다르기 때문에 ``False``를 출력했고
``a == b``는 a와 b가 ``[1, 2, 3]``으로 같으므로 ``True``를 출력했다.

> Singleton 객체와 대조하는 경우 ``==``연산보다는 메모리의 주소를 참조하는 ``is`` 연산을 사용하는 것을 권장한다. ``is``연산이 조금 더 빠르고 메모리 주소가 고정된 Singleton 객체와 대조하는 경우 좋기 때문