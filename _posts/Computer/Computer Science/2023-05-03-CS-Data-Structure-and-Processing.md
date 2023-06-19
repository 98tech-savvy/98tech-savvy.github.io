---
title:  "[CS] 데이터 구조와 처리"
excerpt: "데이터를 구성하고 처리하는 방법"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Computer
tags:
  - [Computer, 데이터, 데이터 구조, 데이터 처리]

toc: true
toc_sticky: true

date: 2023-05-03
last_modified_at: 2023-05-03
---

# 기본 데이터 타입
프로그래밍 언어는 다양한 기본 데이터 타입을 제공한다. 이 타입에는 크기(비트 수)와 해석(부호의 존재, 문자인지, 포인터인지, 불리언인지 등)이라는 두 가지 측면이 존재한다.

**포인터**는 부호가 없는 정수이며, 정숫값이 아니라 메모리 주소로 해석한다. 집 주소라고 생각하면되는데 집 주소가 '집 그 자체'는 아니지만 집을 찾을 때 사용할 수 있는 녀석인것처럼 포인터로 원하는 값이 있는 위치를 알아낼 수 있다.

# 배열
배열은 같은 타입의(일반적인 컴퓨터 개발 규정에 배열 원소의 타입은 모두 같아야함) 집합들이라고 생각하면 된다. {1, 2, 3, 4, 5, 6}이나 {101호, 102호, 102호, 201호, 202호, 203호}같은, 이 안에 원소들이 위치한 공간(ex: {1, 2, 3, 4, 5, 6}은 {0, 1, 2, 3, 4, 5}번째에 위치해있음)을 인덱스<sup>index</sup>({0,1,2,3,4,5})라고 하고 원소({1,2,3,4,5,6})은 그대로 원소<sup>element</sup>라고 부른다.

프로그래밍 언어는 다차원 배열을 지원하기도 하는데 인덱스의 갯수에 따라 차원이 달라진다.
예를 들어 100동 1호, 100동 2호, 200동 1호, 200동 2호의 경우는 '동'과 '호'의 인덱스가 2개이기 때문에 2차원, '층'이 추가된다면 3차원의 배열로 해석할 수 있다.

다차원배열의 경우에는 주소 공간상에서 열 인덱스가 바뀔 때보다 행 인덱스가 바뀔 때 더 많은 이동이 일어난다.

# 비트맵
**비트맵**은 비트의 배열이다. Bitmap은 Map of bits라는 뜻으로, 비트의 지도라는 뜻이다. 35비트를 8비트 바이트 5개짜리로 담을 수 있고, 이 비트번호 17을 찾고싶다면 17/8(1바이트)로 나누어서 2가 나오므로 세 번째 바이트(0번째 바이트를 더해준)에 있음을 알 수 있다.

비트맵에는 위의 배열인덱스와 0x07을 AND해서 얻은 하위 3비트를 통해(비트 마스크)를 통해 다음 4가지 연산을 쉽게 수행할 수 있다.

```
00010001 #예를 들어본 17
00000111 AND #0x07
-------------
00000001

얻은 값 1만큼 왼쪽으로 시프트 하면 마스크값이 나옴
```


- 비트 설정하기
INDEX = INDEX OR MASK
- 비트 지우기
INDEX = INDEX AND (NOT MASK)
- 비트가 1인지 검사하기
INDEX AND MASK ≠ 0
- 비트가 0인지 검사하기
INDEX AND MASK = 0

# 문자열
문자열은 여러 문자로 이뤄진 시퀀스를 말한다.

문자열은 배열과 마찬가지로 그 길이를 알아야하는데, 가변 문자열 데이터의 경우 길이가 변하기 때문에 문자열의 길이를 미리 알 수 없다. 이 때는 그냥 큰 배열을 사용하는 경우가 있지만 문자열의 길이를 따로 추적할 방법이 필요하다.

1. 문자열 안에 길이를 저장한다
예를 들어 첫 번째 바이트에 문자열의 길이를 넣어준다. 이 때에는 문자열의 길이가 255자로 제한된다는 단점이 있다.

2. 문자열의 끝에 NUL값을 넣는다
이는 C에서 사용하는 방법인데, 문자열 터미네이터(문자열 끝을 표시하는 문자)로 NUL값을 사용해서 문자열의 길이를 알아낼 수 있다. 하지만 중간에 NUL문자를 넣을 수 없다는 단점이 있고, 터미네이터가 NUL값을 발견할 때 까지 문자열을 세야한다는 단점이 있다.

# 단일 연결 리스트
배열은 목록을 저장하기에 가장 효율적인 방법이다. 하지만 데이터의 양이 가변적이라면 더 큰 배열을 만들고 그 배열에 저장해주어야하기 때문에 배열은 적합하지않다(너무 큰 배열을 잡아버리면 메모리 낭비이기때문에) 

**연결 리스트**는 목록에 들어갈 원소의 개수를 모를 경우 적합한 방식이다. 현재 원소의 개수만큼 구조체에 next포인터(다음 원소 주소를 저장)와 데이터를 담아 저장한다. 마지막의 next포인터에는 NULL을 집어넣어 연결 리스트의 끝(꼬리)임을 알린다.

리스트에는 원소를 쉽게 추가할 수 있지만 삭제는 좀 더 복잡한 방법으로 이루어진다. 원소를 추가할 때에는 구조체를 하나 더 추가해주면 끝이지만, 삭제할 때에는 next포인터가 가리키는 주소를 바꿔주어야하기 때문이다.

*배열은 메모리에 연속적으로 위치하지만 리스트 원소는 메모리의 어느 곳에나 존재할 수 있음*

# 동적 메모리 할당
연결 리스트에 새 노드를 추가할 때 메모리를 얻어야하는데 이 메모리는 어디서 얻어오는걸까?
MMU가 없다면 **힙 영역**에서 메모리를 얻어온다. 배열같은 메모리는 **정적**이고 이 메모리의 주소는 바뀌지 않지만, 리스트 노드같은 존재는 **동적**으로 필요에 따라 생기기도하고 사라지기도 한다. 프로그램은 이 힙 영역을 관리할 수 있어야 하는데, 사용중인 메모리와 사용가능한 메모리를 알아야한다.

# 가비지 컬렉션
가비지 컬렉션은 동적 메모리를 효율적으로 관리해주는 '도구'이다. C언어의 경우는 malloc과 free함수를 통해 메모리를 관리해주지만, 자바나 파이썬같은 언어는 위 함수대신 **가비지 컬렉션**을 구현해 메모리를 관리한다. 단점으로는 프로그래머가 가비지 컬렉션을 제어할 수 없기 때문에 프로그램이 일을 하는 도중 문제가 생길 수도 있고, 불필요한 참조가 남는 경우가 있기 때문에 메모리를 더 많이 사용하는 경향도 있다.

# 이중 연결 리스트
단일 연결 리스트에서는 삭제하기 위해서 원소의 바로 앞 원소를 찾아야했다. 이 단점을 메모리를 더 사용해줌으로써 해결할 수 있는데, **이중 연결 리스트**라는 녀석이다. next(다음 원소) 포인터와 previous(이전 원소) 포인터를 가지고있어서 노드를 앞에서부터 찾아내 delete할 필요가 사라진다.

# 계층적 데이터 구조
위의 데이터 구조들은 전부 **선형적**이다. 선의 형태를 띄고 있다는 뜻인데, 연결 리스트에 물건을 가져와야 된다고 할 때 리스트를 순회해서 찾아야한다. 리스트의 길이가 N이라면 최대 N만큼 노드를 순회해서 원하는 노드인지 비교해야한다.

가장 간단한 계층적 데이터 구조에는 **2진 트리**가 있다. 노드가 최대 2개의 다른 노드와 연결될 수 있다는 뜻이다.
![image](https://user-images.githubusercontent.com/128434645/235852920-849d7a92-364e-41ba-a6d8-4156e47e9587.png)

위의 그림과 같은 형태를 띄고 있는데, N번 순회해야하는 선형적 구조와는 다르게 더 적은 횟수로 원하는 값을 찾을 수 있다.