---
title:  "모듈과 패키지, 내장함수와 외장함수"
excerpt: "Python의 모듈과 패키지는 어떻게 만들고 사용하는지, 내장함수와 외장함수는 어디서 찾고 사용하는지"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, 예외처리, 모듈, 패키지, 내장함수, 외장함수]

toc: true
toc_sticky: true

date: 2023-04-10
last_modified_at: 2023-04-10
---

# 예외처리
우리들은 예상치 못한 실수, 혹은 잘못된 무언가를 에러<sup>error</sup>라고 부른다. 택배 기사가 12층에 택배를 가지고왔는데 아파트에 12층이 없는 경우, 고양이가 강아지 소리를 낼 경우? 프로그램에서는 굉장히 많은 에러 상황이 발생할 수 있고 이를 예측하고 처리하는 과정에서 완성도가 높고 사용성이 좋은 프로그램이 만들어진다.

예외처리를 하는 코드는 다음과 같다.
``` python
try:
    예외처리 할 코드
except 오류코드2:
    오류로 처리할 내용
except 오류코드2:
    오류로 처리할 내용2
...
except:
    오류로 처리할 내용(나머지 모든 에러)
```
if ~ elif ~ else의 구문처리와 비슷하다. 실제로 if와도 처리하는 방식이 비슷한 것 같다.

프로그램이 에러가 나올 때 마다 강제종료되는 상황을 없애주며 사용자의 실수를 오류로 지적하여 도움을 줄 수도 있다.
```python
if 조건: #ex) if apt_floor > 11: 
    raise 오류코드 #ex) raise 경비실에_맡기기
```
if와 raise를 이용해 어느 조건에 오류를 발생시킬 수도 있다.

## 사용자 정의 예외처리
```python
except ValueError: #값이 이상할 때
```
의 코드에 [ValueError] 같은 오류코드는 파이썬에서 기본으로 제공하는 오류코드다. 프로그램을 짜다보면 기본으로 제공하는 오류코드 외에 다른 오류코드가 필요할 때가 있으며 그 때 사용할 수 있는 것이 사용자 정의 예외처리다.<br>

클래스의 괄호()에 Exception이 들어간 클래스를 정의해주고

사용할 때에는 except 오류코드이름: 식으로 사용해주면 된다.
```python
class 오류코드이름(Exception):
    def __init__(self, ...)
```

## finally
finally 문은 **예외처리구문에서 예외처리가 발생을 하던 안하던 마지막에 반드시 실행하는 구문**을 말한다.

``` python
try:
    ~
    !Error1 발생!
except Error1:
    ~
except Error2:
    ~
finally:
    print("finally 문")

결과:
Error1 ~ 
finally문
```

이 코드에서 Error1이 발생되어도 finally의 구문은 실행된다.

# 모듈
파이프 배관공이 파이프 라인을 쉽게 설치하기 위해서 [ㄱ자 파이프] [1자 파이프] [+자 파이프]들이 들어있는 기성품 세트를 구매해서 사용하는 것처럼 **프로그래머들이 유지보수를 쉽게, 코드의 재사용을 수월해지게 하기 위해 사용하는 것이 모듈이다.**

모듈은 함수 정의나 클래스 등 서로 관련있는 혹은 비슷한 기능을 하는 파이썬 문장끼리 모여있는 것을 말한다. 그리고 필요한 기능끼리 모아주는 것을 **모듈화<sup>modularization</sup>**라고 한다.

## 모듈 사용법
그러면 실제로 모듈을 만들어보고 그 모듈을 다른 파일에 적용해서 사용해보도록 하겠다.

이 모듈은 성인/학생/노인 가격을 나눠주는 모듈이다.

sep_price.py
``` python
#이 파일의 이름은 sep_price.py 다.
#일반 가격
def normal_price(people):
    print("{}명 가격은 {}원 입니다.".format(people, people*10000))

#학생 가격
def student_price(people):
    print("{}명 가격은 {}원 입니다.".format(people, people*6000))

#노인 가격
def senior_price(people):
    print("{}명 가격은 {}원 입니다.".format(people, people*4000))
```

이 sep_price.py 파일을 저장해주고 새로운 파일을 만들어주자.

calculate_price.py
``` python
#이 파일의 이름은 calculate_price.py 다.
import sep_price #sep_price.py 를 불러옴. 경로를 지정해주는게 아니면 같은 폴더내에 있어야 가능

sep_price.normal_price(3)
sep_price.student_price(3)
sep_price.senior.price(3)
```

실제로 실행도 잘 되는 것을 확인할 수 있다. 하지만 이렇게 sep_price.normal_price, sep_price.student_price 처럼 계속해서 쓸려니 손가락도 아프고 지친다. 이럴 때에는 **[import 모듈 as 별칭]** 을 사용해주면 편리하다.

``` python
import sep_price as sp

sp.normal_price(3)
```

이렇게 별칭을 지정해주면 코드 짤 때 스트레스를 조금 줄일 수 있다. 또 from을 사용해서 불러와 줄 수 있다.

```python
from sep_price import * #sep_price 모듈의 *(모든 것)을 불러오겠다는 의미이다.
from sep_price import normal_price as np#sep_price 모듈의 normal_price 함수만 사용하겠다는 의미이다. 그리고 이 normal_price를 np라는 별칭으로 사용하겠다는 뜻
```

<br><br>

# 패키지
패키지는 '모듈들의 집합'이라고 생각하면 된다. 쉽게 말해서 **패키지 = 폴더, 모듈 = 파일** 이다.

## import 구문
import 구문을 사용할 때에는 그 대상이 '모듈이나 패키지'이어야 하며 클래스나 함수는 import 구문을 사용할 수 없다.

## from ~ import 구문
클래스, 함수를 사용하려면 [from ~ import]구문을 사용해주어야하는데, from ~ import 구문은 모듈, 패키지, 클래스, 함수 전부를 import 할 수 있다.
<br><br>

# __all__
random 모듈을 사용할 때, 우리들은
``` python
from random import *
```
구문을 통해 random 모듈을 불러와서 사용했음을 알 수 있다. 하지만 사용자가 만든 패키지에서 **\***를 사용하려 하면
``NameError: name '사용자가 만든 패키지 이름' is not defined``
라는 에러가 나오는걸 볼 수 있는데, 그 이유는 **패키지 안의 '공개 범위'**를 설정해주지 않아서 그렇다.

패키지 파일안에 __init__.py 파일을 만들고, __init__.py 파일 안에 

```python
#__init__.py
__all__ = ["모듈이름1", "모듈이름2"]
```

를 적어준다. 그러면 이 패키지의 '공개 범위'안에 [모듈이름1]과 [모듈이름2]가 들어가서

``` python
from 사용자_패키지 import *
```

을 해도 문제없이 실행됨을 볼 수 있다.
<br><br>

# 모듈 직접 실행
공부할 때의 짧은 예제와는 다르게 보통 프로그램 안의 모듈들은 10줄 안의 짧은 코드들이 아닌 수백줄 혹은 그 이상의 코드들로 짜여진 복잡한 모듈들이 많다.
그래서 우리들은 모듈에 에러가 없는지 직접 실행을 해보고 확인해주어야한다.

모듈을 직접 실행하는지, 외부에서 실행하는지 확인하려면 모듈 안에 이 코드를 넣어준다.

``` python
if __name__ == "__main__": #모듈이 직접 실행되는 경우
    print("모듈 직접 실행중")
else: #모듈이 외부에서 실행되는 경우
    print("모듈 외부 실행중")
```

이 코드는 외부(대화형 인터프리터나 다른 파일)에서 사용할 때 __main__ 값이 false가 되어서 else:의 코드가 진행되는 방식이다.
<br><br>

# 패키지, 모듈 위치
예제에서 패키지나 모듈을 공부할 때에는 그 패키지 폴더와 모듈 파일이 전부 같은 위치내에 있어서 문제없이 불러오고 사용할 수 있었다.

``` python
import random
import 사용자정의모듈
print(inspect.getfile(random))
print(inspect.getfile(사용자정의모듈))

결과:
C:\Python38\lib\random.py
C:\Users\User\Desktop\PythonWorkspace\사용자정의모듈.py
```

[사용자정의모듈]이 내 워크스페이스 안에 위치해서 사용할 수 있었지만, [random]은 'Python38'이라는 파이썬 설치 폴더내에 있어도 무리없이 사용할 수 있었다.
모듈을 여러 프로그램들을 개발함에 있어서 필요해서 계속 사용하고 싶을 때에는 C:\Python설치위치\lib\ 안에 넣어주면 문제없이 작동한다.
<br><br>

# pip install
개발자들은 수 많은 패키지를 사용하고 수 많은 패키지를 지금 이 글을 읽는 시간에도 개발하고 만들어내고있다.
파이썬에서 기본적으로 제공하는 패키지외에 다른 사람들이 만든 패키지를 사용하고싶으면(무조건 갖다쓰는건 추천하지않지만 이미 유용한 코드들이 있다면 해석하고 활용하는 건 좋다고 생각한다)
'pip install'을 사용해주면 된다.

일단 설치할 패키지를 찾아보자. [PyPI](https://pypi.org/search/)에 들어가면 수 많은 개발된 패키지들을 찾을 수 있다.
설치하고싶은 패키지를 찾고 들어가보면 제목아래에 코드블럭으로 감싸진 [pip install 패키지이름]을 찾을 수 있을것이다.

이 [pip install 패키지이름]을 VSCode같은 프로그램의 터미널에 직접 쳐주면(복사해주면) 패키지가 실행되고 문제없이 사용되는 모습을 볼 수 있다.

## pip list
현재 설치된 패키지의 버전과 이름을 확인할 수 있다.

## pip show 패키지이름
현재 설치된 패키지의 상세한 정보를 확인할 수 있다.

## pip install --upgrade 패키지이름
설치된 패키지에 업데이트가 필요할 때 사용해준다. 

## pip uninstall 패키지이름
설치된 패키지를 삭제해준다.
<br><br>

# 내장 함수
내장 함수란 이미 설치되어 있어 따로 포함해줄 필요없이(import를 할 필요없이) 바로 사용할 수 있는 함수들을 말한다. 예를 들어
input, dir 등이 있다. 

- input
사용자 입력을 받는 함수.

- dir()
어떤 객체를 넘겨줬을 때 그 객체가 어떤 변수, 함수를 가지고 있는지 표시해줌
dir(random)을 할 시 random 안의 모든 변수와 함수를 알려줌

그 외의 내장 함수들은 파이썬 사이트의 [내장함수<sup>Python Built-in functions</sup>](https://docs.python.org/ko/3/library/functions.html)를 참고하자.
<br><br>

# 외장 함수
외장 함수들은 따로 import를 해서 사용해야하는 함수들을 말한다.
[Python 모듈 목록<sup>Python Module Index</sup>](https://docs.python.org/ko/3/py-modindex.html)에서 확인할 수 있다.