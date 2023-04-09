---
title:  "[Python] 파일, "
excerpt: "Python의 파일을 다루는 방법과 "

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, 파일입출력, Pickle]

toc: true
toc_sticky: true

date: 2023-04-09
last_modified_at: 2023-04-09
---

# 파일입출력
프로그래밍에서 파일을 다룰 때는 일반적으로
1. 파일을 연다 (Open)
2. 파일에 어떤 내용을 쓰거나 읽는다 (Read/Write)
3. 파일을 닫는다 (Close)

의 순서로 진행한다. 파이썬에서 파일을 열거나, 기록하거나, 닫기 위해서는 어떻게 해야할까?

## 파일을 여는 방법
파이썬에서 파일을 열기 위해서는 open() 함수를 사용한다.
``open("File name", "Open mode", encoding="encoding type")``
File name에는 파일의 이름과 확장자를, Open mode에는 [읽기(R), 쓰기(W), 이어쓰기(A)], encoding type에는 일반적으로 utf8 을 적어주면 된다. 굳이 encoding 까지 적을 필요는 없으나 혹시 모를 에러(인코딩으로 글자가 깨진다거나)에 대비해 꼭 적어주는 습관을 들이자.

### 쓰기 모드 (Write)
쓰기 모드로 파일을 열고 나서 파일을 기록하게 되면 전부 '덮어쓰기'로 쓰여지게된다. 이전의 기록들이 사라진다는 뜻.

``` python
score_file = open("score.txt", "w", encoding="utf8") #score.txt를 쓰기(w)모드 ,utf8형식으로 엶
print("수학 : 100", file=score_file)
print("영어 : 90", file=score_file)
score_file.close() #파일을 닫음
```

이 코드를 작성하면 디버깅창에 수학과 영어의 점수가 뜨지 않는다. print()문 내에 file=score_file로 score.txt에 직접 출력해주었기 때문에 디버깅 창에 뜨지 않는 모습을 볼 수 있다.

### 이어쓰기 모드 (Append)
Apeend의 뜻은 추가하다. '이어쓰기' 혹은 '추가쓰기'로 생각해주면 편할 것 같다.

``` python
score_file = open("score.txt", "a", encoding="utf8") #score.txt파일을 이어쓰기(a)모드, utf8형식으로 엶
score_file.write("국어 : 100\n")
print("과학 : 80", file=score_file)
score_file.close()
```

쓸 때에는 변수.write("")의 형식으로 쓸 수도 있다. 이 때 write문은 자동으로 줄 바꿈을 해주지 않기 때문에 \n(개행문자)를 추가해준 모습이다.

### 읽기 모드 (Read)
'읽기 모드'이기 때문에 글의 내용을 추가하거나 덮어쓸수 없다.

``` python
score_file = open("score.txt", "r", encoding="utf8") #score.txt 파일을 읽기(r)모드, utf8형식으로 엶

#score_file.write("참 잘했어요\n") #오류 io.UnsupportedOperation: not writable가 발생하는 곳, '읽기 모드'이므로 쓸 수 없음
print(score_file.read())
score_file.close()
```

``` python
print(score_file.read())
```

를 해주게 되면 그 파일의 전체 내용을 읽어서 디버깅창에 표시하는것을 볼 수 있다. 한 줄 한 줄 읽어내리고 싶다면 readline()을 활용해주면 된다.

``` python
score_file = open("score.txt", "r", encoding="utf8") #score.txt 파일을 읽기(r)모드, utf8형식으로 엶

print(score_file.readline(), end="") #줄바꿈을 없애기 위해 end=""를 넣어줬는데, 이 파일의 끝에도 개행이 들어가있고, print도 자체적으로 개행을 하기 때문에 하나의 줄바꿈을 없애준 것
print(score_file.readline(), end="")
print(score_file.readline(), end="")
print(score_file.readline(), end="")

score_file.close()
```

하지만 이렇게 했을 때에 파일의 내용이 많으면 많을 수록 readline을 얼마나 해야하는지 착잡해질 것이다. 이 때 while문이나 for문을 사용해주면 간단하게 해결할 수 있다.

``` python
#---1번째 방법---#
score_file = open("score.txt", "r", encoding="utf8") #score.txt 파일을 읽기(r)모드, utf8형식으로 엶

while True:
    line = score_file.readline()
    if not line: #더 이상 읽을 내용이 없다면
        break #반복문을 나간다
    print(line, end="")

#---2번째 방법---#
score_file = open("score.txt", "r", encoding="utf8") #score.txt 파일을 읽기(r)모드, utf8형식으로 엶

for line=score_file.readlines in lines: #readline이 아니라 readlines 이다. 전부 읽어서 line 이라는 리스트에 저장한다.
    print(line, end="")
```

while문은 break를 통한 탈출을, for문은 readline()를 활용한다는 것을 알아두면 좋을 것이다.

## pickle, pickle을 쓰는 이유
pickle은 프로그램에서 사용하고 있는 데이터를 파일 형태로 저장하거나 불러올 수 있게 해주는 모듈이다. *'그러면 위의 파일 함수들을 사용하면 되는거 아닌가?'* 라고 생각을 해서 구글링을 해봤는데, **클래스<sup>class</sup>자체를 통째로 파일로 저장했다가 그것을 그대로 불러올 수 있어 유용한 모듈이라고 한다. 그리고 pickle을 사용하면 바이너리<sup>binary</sup>형태로 저장되어서 파일의 용량또한 매우 작아진다고 한다**.

### pickle 사용법
pickle을 이용해 데이터를 저장하고자 할 때에는
``dump(data, file_name)``을 사용한다.
data에는 저장할 데이터를, file_name에는 데이터를 저장할 파일을 적어주면 된다.

또 **읽기, 쓰기**를 할 때에는 바이너리 형태의 파일이기 때문에 **r대신 rb를, w대신 wb**를 사용해준다.

- 쓰기

``` python
import pickle #pickle 모듈 가져오기

profile_file = open("profile.pickle", "wb") #파일형식은 pickle, 읽기모드는 "wb"
profile = {"이름":"김철수", "나이":22, "취미":["파이썬", "자바스크립트"]} #{} -> [] -> ()
print(profile)

pickle.dump(profile, profile_file) #profile 데이터를 profile_file에 저장(이 때, profile.pickle을 열었으므로 profile.pickle에 저장이 됨)
profile_file.close()
```

바이너리 파일로 저장해주어서 vscode나 일반 텍스트에디터로는 열 수 없다.

- 읽기

``` python
import pickle #pickle 모듈 가져오기

profile_file = open("profile.pickle", "rb") #rb형태로 profile.pickle 열기
profile = pickle.load(profile_file) #profile.pickle의 변수 profile_file을 읽어와서 그대로 profile에 저장함
```

pickle.load() 함수로 pickle형식의 파일을 읽을 수 있다.

## with
프로그램에서 파일을 열어줬을 때는 반드시 파일을 닫아주는 작업을 해주어야한다(파이썬에서는 .close()로 그 역할을 수행한다). 이렇게 파일을 열고 닫아줘야하는 귀찮은게 싫다면, with문을 사용해주면 된다.

with문은 파일을 열고 나서 close()문을 선언하지 않아도 자동으로 파일을 닫아준다.

``` python
with 작업 as 변수명:
    실행 명령문
```

with 뒤의 작업에 open()함수를 넣어주고, open()을 통해 열린 파일은 as 뒤의 변수명에 저장된다. 

# 클래스(Class)
클래스는 붕어빵 기계의 틀과 같다. 틀은 하나지만 붕어빵은 계속해서 만들어낼 수 있는 것처럼 클래스도 클래스 하나로 계속해서 객체를 만들어낼 수 있다.

같은 정보(속성)를 가진 변수와 함수를 한 군데 묶어준다고 생각하면 좋다. 예를 들어 스타크래프트의 마린, 히드라, 탱크, 레이스 등은 전부 '유닛' 임으로 '유닛' 클래스로 묶어주는 것이다.

여러가지 아이들

``` python
#마린, Hp=40, Damage=5
marine_hp=40
marine_damage=5

#히드라, Hp=75, Damage=8
hydra_hp=75
hydra_damage=8

#탱크, Hp=150, Damage=40
tank_hp=150
tank_damage=40
```

이렇게 하면 처음에는 괜찮을지는 몰라도 마린의 수가 늘어나면 marine2_hp=40 ... marine100_hp = 40 까지, 탱크나 히드라도 늘어나고 다른 종류의 유닛들도 많아지니 겉잡을 수 없이 복잡해질 것이다. 그럴 때 클래스를 사용해주면

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage
      print("{} : hp {} damage {}".format(self.name, self.hp, self.damage))

Marine = Unit("마린", 40, 5)
Hydra = Unit("히드라", 75, 8)
Tank = Unit("탱크", 150, 40)

결과:
마린 : hp 40 damage 5
히드라 : hp 75 damage 8
탱크 : hp 150 damage 40
```

이렇게 깔끔하게 코드를 정리하고 편리하게 사용할 수 있다.

## 객체, 인스턴스
우리들은 class를 사용해서 변수를 정의해줄 때 이 변수를 '객체'라고 한다. 또 '인스턴스'라고도 한다. 공부할 때, 정리할 때 이 단어들이 자꾸 혼용되어서 헷갈려서 구글링을 해보았다.

### 객체와 인스턴스의 차이
위의 코드에서, Unit 클래스를 만들고 Marine을 만들어주었다. 이 때 Marine은 '객체'이고 또 객체 Marine은 Unit의 '인스턴스'이다. 이 말이 무슨말이냐면 **객체와 인스턴스는 Marine을 가리키지만 인스턴스는 그 객체가 어떤 클래스의 객체일 때도 사용한다.** 라는 뜻이다.

## 멤버 변수
멤버 변수란 **메소드 밖**에서 호출된 변수를 뜻한다(메소드 안에서 호출된 변수는 '지역 변수'라고 한다). 함수의 지역변수와 프로그램의 전역변수를 멤버 변수와 클래스로 좁혀놨다고 생각하면 편할지도,

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage

    def attack(location):
        print("{}이 {}방향으로 공격합니다.".format(self.name, location))
```

일 때 self로 사용하는 친구들이 멤버 변수, 메소드 내에서 사용하는 location같은 친구들을 지역 변수라고 한다.

또 멤버 변수는 아예 클래스 바깥에서 인자를 추가해줄 수 있는데

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage

    def attack(location):
        print("{}이 {}방향으로 공격합니다.".format(self.name, location))

Ultra = Unit("울트라", 400, 20)
Ultra.ArmorUpgrade = True

if Ultra.ArmorUpgrade == True:
  print("{]의 방어력 업그레이드가 완료되었습니다".format(Ultra.name))
```
와 같이 사용할 수 있다. 이 인자는 Ultra 객체에 한해 사용되는 것으로, 만약에

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage

    def attack(location):
        print("{}이 {}방향으로 공격합니다.".format(self.name, location))

Ultra1 = Unit("울트라1", 400, 20)
Ultra1.ArmorUpgrade = True
Ultra2 = Unit("울트라2", 400, 20)

if Ultra1.ArmorUpgrade == True:
  print("{}의 방어력 업그레이드가 완료되었습니다".format(Ultra1.name))

if Ultra2.ArmorUpgrade == True:
  print("{}의 방어력 업그레이드가 완료되었습니다".format(Ultra2.name))
```

와 같이 사용하려한다면
``AttributeError: 'Unit' object has no attribute 'ArmorUpgrade' = Unit오브젝트에 ArmorUpgrade라는 속성이 존재하지 않습니다.``라는 오류를 뿜으며 디버깅에서 정지될 것이다.

## 상속
Unit에 체력과 Hp, 데미지가 들어가기로 위의 코드에 선언했다. 그리고 나만의 스타크래프트가 업데이트를 진행하며 [힐 유닛]을 추가하기로 했다. 힐 유닛이라도 체력, hp, 데미지는 동일하게 들어가있는데 이럴 때 사용하면 좋은 것이 '상속'이다.

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage

class HealUnit(Unit): #Unit 클래스 상속
    def __init__(self, name, hp, damage, heal):
      Unit.__init__(self, name, hp, damage)
      self.heal = heal
```

``` python
class HealUnit(Unit):
```
을 보면 HealUnit의 괄호안에 Unit이 들어가있는데, 이 뜻은 Unit클래스의 모든 멤버변수와 메소드를 HealUnit에서 사용하겠다는 뜻이다.

이렇게 **서로 관련이 있는 클래스들 중 공통적인 부분이 있는 클래스를 '부모' 클래스로 정의하고 '자식' 클래스에서 필요한 부분을 확장하며 사용하면 코드의 중복을 방지하고 작업을 최소화할 수 있다.**

### 다중상속
이번의 업데이트에 '힐 공중유닛'인 '의료선'을 추가하기로 했다. 그래서 '날 수 있는 기능'을 먼저 만들기로 했고 그 뒤에 의료선을 추가하기로했다.

``` python
class Flyable:
    def __init__(self, flying_speed):
      self.flying_speed= flying_speed
    
    def flying(self, name, location):
      print("{} : {}방향으로 날아갑니다.".format(self.name, self.location))
```

날 수 있는 기능과 힐을 할 수 있는 기능이 둘 다 포함된 클래스를 만들려면 어떻게 해야할까? 그 때 우리는 '다중상속'을 사용하면 된다. 쉽게 생각해서 '부모를 여러명 두기'라고 생각하면.. 된다?

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage

class HealUnit(Unit): #Unit 클래스 상속
    def __init__(self, name, hp, damage, heal):
      Unit.__init__(self, name, hp, damage)
      self.heal = heal

class Flyable:
    def __init__(self, flying_speed):
      self.flying_speed= flying_speed
    
    def flying(self, name, location):
      print("{} : {}방향으로 날아갑니다.".format(self.name, self.location))

class FlyableHealUnit(HealUnit, Flyable):
    ...
```

``` python
class FlyableHealUnit(HealUnit, Flyable):
    ...
```

이렇게 해주면 FlyableHealUnit 클래스는 HealUnit의 모든 멤버변수와 메소드 + Flyable의 모든 멤버변수와 메소드를 사용할 수 있게 되는 것이다.

## 메소드 오버라이딩
만약 Unit의 Move 메소드가 '지상 유닛' 전용으로 설계되었다면 '공중 유닛'을 만들 때에는 Unit 메소드부터 뜯어고쳐야하는 귀찮음을 겪어야할 것이다(괜히 건드렸다가 복잡해지는 프로그램도 덤이다). 그럴 때는 '메소드 오버라이딩'을 통해 가볍게 해결할 수 있다.

``` python
class Unit:
    def __init__(self, name, hp, damage):
      self.name = name
      self.hp = hp
      self.damage = damage
    
    def move(self, location,move_speed):
      print("[지상 유닛 전용]")
      print("{} : {} 방향으로 {}의 속도로 이동합니다".format(self.name, location, move_speed))

#현재 공중유닛의 move가 없어서 공중유닛 클래스의 move를 만들어줘야함
class FlyUnit(Unit):
    def __init__(self, name, hp, damage):
      Unit.__init__(self, name, hp, damage)
    
    def move(self, location, fly_speed)
      print("[공중 유닛 전용]")
      print("{} : {}방향으로 {}의 속도로 이동합니다.".format(self.name, location, fly_speed))
```

그리고 실제로 FlyUnit의 객체를 만들고 실행을 해보면 [공중 유닛 전용]으로 출력이 되는걸 볼 수 있다. 쉽게 말해서 **메소드 오버라이딩 = 덮어쓰기**라고 생각하면 된다.

## pass
코드를 짤 때 사용하는 문구 중 하나로, 이 문구가 있으면 **아무것도 하지 않고 지나감**이라는 뜻이다. 코드를 임시로 짜둘 때(프로그램의 토대를 만들 때) 유용하게 사용하는 문구다.

``` python
class BuildingUnit(Unit): #다음 업데이트 때 쓸 내용
    def __init__(self, name, hp, location):
        pass
```

## super()
우리들은 위의 예제들을 보면서 FlyableHealUnit이 HealUnit과 Flyable을 다중상속받은걸 볼 수 있었다. 기본적으로 상속받은 클래스의 메소드를 쓸 때에는 Unit.name이나 HealUnit.Heal처럼 [상속받은클래스.메소드]의 형태로 사용하는데, **최상위 부모 클래스(제일 첫 번째의)의 메소드를 사용하려면, 혹은 접근하려면 super() 를 사용**해주면 된다. 아래 예제에서는 super()은  클래스를 가리키는 문구가 되겠다.

``` python
class Unit:
    def __init__(self):
        print("Unit")

class Unit2:
    def __init__(self):
        print("SecondUnit")

class Unit3(Unit, Unit2):
    def __init__(self):
      super().__init__()

Unitunit = Unit3()
```

**super()의 경우 사용할 때에 self를 사용하지 않는다.** 

위의 코드를 실행하면 제일 첫 번째에 있던 Unit의 생성자가 호출되는 것을 볼 수 있다.