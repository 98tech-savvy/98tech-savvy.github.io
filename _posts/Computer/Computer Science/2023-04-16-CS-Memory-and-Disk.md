---
title:  "[CS] 메모리와 디스크의 핵심, 순차 논리"
excerpt: "컴퓨터는 비트를 어떻게 기억할까? 시간을 표현하는 방법과 램의 종류부터, 그리고 오류를 검출하는 여러가지 방법들"

//현재 카테고리: Computer, Blog, Python, License, Java, Javascript, VSCode, Git
categories:
  - Computer
tags:
  - [Computer, 컴퓨터과학, CS, 순차 논리, 메모리와 디스크 핵심, 오류를 검출하는 방법, 램의 종류]

toc: true
toc_sticky: true

date: 2023-04-16
last_modified_at: 2023-04-16
---

# 순차 논리<sup>sequential logic</sup>
**순차 논리**라는 말은 '**순**서대로 **차**례대로 **논리**!' 라고 생각하면 된다.
예를 들어 1부터 100까지 정수의 합계를 계산한다고 할 때, 현재 처리 중인 수가 어떤 수인지 알 수 없다면 1부터 100까지 정수의 합계를 계산할 수 없을 것이다. 사람은 직관적으로 시간을 알 수 있지만, 디지털 회로에서는 시간을 자연스럽게 다룰 수 없기 때문에 입력의 현재 상태와 과거 상태를 고려해 시간을 만들어 내고 과거를 기억하기 위한 회로를 만들어야하는 것이다.

# 시간을 표현하는 방법
하루는 1일이고, 1일은 24시간이고, 24시간은 1440분, 1440분은 86400초이다.
지구가 한 바퀴를 다 돌면(자전하면) '하루'라고 부르기로 했고, 1초는 지구 자전의 1/86400이다. 우리들은 지구의 주기같은 외부 이벤트로 시간을 표현할 수 있고, 괘종시계의 진자(똑딱이는 부분)가 오가는 시간을 주기로 활용해 시간을 측정할 수 있다.

## 발진자
![image](https://user-images.githubusercontent.com/128434645/232190417-adb24326-b5c1-4d0c-b1fa-dea779d2785e.png)
*[Wikipedia, Negative-feedback amplifier](https://en.wikipedia.org/wiki/Negative-feedback_amplifier)*

위 그림은  인버터의 출력과 입력을 연결 시킨 것이다. 인버터의 출력은 다시 입력으로, 입력은 다시 출력으로 반영되는데 이것을 **피드백<sup>feedback</sup>**이라고 하고, 이로 인해 출력은 **0과 1 사이를 진동한다.**

크리스털<sup>crystal</sup>을 사용하면 좀 더 안정적인 발진자를 만들 수 있는데, 크리스털을 전선에 연결하고 크리스털을 압축시키면 크리스털은 전기를 만들어낸다. 그리고 전기를 가하면 크리스털이 구부러지는데, 이러한 현상을 **피에조 전기<sup>piezoelectric</sup>**라고 부른다. 이러한 크리스털 발진자에 전자적인 단극쌍투 스위치를 사용해 전기를 가하고, 다시 전기를 얻어낸다. 입력한 전기로부터 크리스털이 전기를 만들어내는 시간은 예측이 가능하고 매우 정확해 적은 비용으로 효율적인 발진자를 만들 수 있다.

## 클록<sup>clock</sup>
발진자는 컴퓨터에 클록<sup>clock</sup>(시간을 셀 수 있게 해주는 신호)을 제공한다. 이 클록은 음악에서 드럼으로 템포를 조절하는 것과 같은 역할을 하는데, 회로의 페이스를 결정한다. 회로의 최대 클록 속도나 가장 빠른 템포를 회로의 전파 지연 시간에 의해 결정한다.

## 래치<sup>latch</sup>
![image](https://user-images.githubusercontent.com/128434645/232191330-9d720409-0a5e-468d-aa7c-9502b78f82c7.png)
*OR 게이트 래치*

이 회로는 위의 인버터와 달리 값을 반전시키지 않기 때문에 진동시키진 않는다.
out이 0으로 시작한다고 할 때, in에 1을 넣어주면 out이 1이 된다. 그리고 out(출력)이 OR의 다른쪽 입력(in의 다른쪽)에 들어가기 때문에 in에 다시 0을 넣어준다해도 이 out은 계속 1이 된다. 우리들은 **과거를 기억하는** 회로를 만들어냈다. 하지만 이 회로만으로는 0을 만들어 줄 수가 없기 때문에 AND게이트를 추가해줘서 피드백을 끊고 회로를 리셋할 방법을 만들어준다.
<br><br><br>
![image](https://user-images.githubusercontent.com/128434645/232192201-dcde027c-2a80-42b4-93e5-e5350a015b9d.png)
*AND-OR 게이트 래치*

인버터의 출력부분에 $reset$위의 바<sup>bar</sup>($\bar{reset}$) 기호는 하드웨어 기호에서 반전<sup>opposite</sup>을 뜻한다. $\bar{reset}$이 0이면 $reset$은 1이고, set을 1로 해준다면 

set = 1, reset = 0:
```
reset'0' > [INVERTER]reset'1' > [AND]'1'
             set'1' - [OR]'1' > 
```

AND와 OR 전부 1(High)의 값을 얻고, set을 0으로 바꿔준다고해도 AND와 OR은 계속해서 1을 출력한다.

하지만 reset이 1로 바뀐다면

set = 0, reset = 1:
```
1: reset'1' > [INVERTER]reset'0' > [AND]'0'
                set'0' - [OR]'1' >

2: reset'1' > [INVERTER]reset'0' > [AND]'0'
                set'0' - [OR]'0' >
```
의 순서로 AND와 OR이 0으로 바뀌기 때문에 최종적으로 out에 0을 출력하게 된다.
<br><br><br>

![image](https://user-images.githubusercontent.com/128434645/232194396-f02f7583-7020-4881-a931-510cfc5f7521.png)
*S-R 래치*

위 회로는 좀 더 똑똑하게 1비트 메모리를 만드는 방법이다. **S**et-**R**eset **래치**라고 하며, 액티브 로우(1을 0으로 표현, 인버터 생각하면 됨)입력이 들어오면 보수<sup>complementary</sup>출력을 제공한다. 이 보수 출력이 제공되면 출력의 한 쪽은 액티브 하이, 다른 쪽은 액티브 로우가 된다.

NOR게이트를 쓰면 입력이 액티브 하이인 S-R래치를 만들 수 있지만, 전력과 복잡도, 비용면에서 비효율적이다.

'AND-OR게이트 래치'에 비해 대칭적이라 set, reset 신호의 지연 시간이 비슷하다는 장점이 있다.

## 플립플롭<sup>flip-flop</sup>
위의 게이트들은 데이터 변경으로 인해 잘못된 결과가 생길 수 있다. 그래서 우리들은 그 잘못될 가능성을 최소화하기위해서 논리 수준이 특정 값에 머무는 동안 데이터를 잡지 않고 논리 수준이 한 수준에서 다른 수준으로 전이되는 중간에 데이터를 잡아내는 방식을 사용한다. 이런 방식을 **에지<sup>edge</sup>**라고 부른다. 에지에 의해 데이터 변화가 촉발되는 래치<sup>edge-triggered latch</sup>를 **플립플롭**이라고 한다.

![image](https://user-images.githubusercontent.com/128434645/232195475-210ddc86-1ecc-498c-9887-05b2df6f8a59.png)
*[Positive, Negative Edge Trigger](https://www.electrically4u.com/wp-content/uploads/2020/10/Edge-triggering.png?ezimgfmt=ng:webp/ngcb4)*

- Positive Edge triggering : D플립플롭이라고 부르며, 클럭이 상승할 때 플립플롭이 동작하는 방식이다. 0에서 1로 변할 때 상승 에지<sup>Rising Edge</sup>을 검출한다.

- Negative Edge triggering : 클럭이 하강할 때 플립플롭이 동작하는 방식으로, 하강 에지<sup>Falling Edge</sup>를 검출한다.

상태가 0에서 0으로, 1에서 1로 변하지 않는 경우에는 에지 트리거는 이벤트를 발생시키지 않는다.

![image](https://user-images.githubusercontent.com/128434645/232195783-be6e479a-4cad-40e9-b948-25d829cf5726.png)
[D-type flip-flop Schemetic](https://pfnicholls.com/Electronics/Dtype.html)

D 플립플롭의 스키매틱 기호다. S-R래치와 2개를 제외하곤 똑같고 S, R은 $\bar{S}$, $\bar{R}$이다(스키매틱 상에서는 보이지 않지만 S, R 박스 앞에 동그라미(O)표시가 있어서 값이 반전된 S바, R바다). 왼쪽의 D와 Ck는 데이터(Data)와 클록(Clock)을 뜻한다. Ck신호가 바뀔 때(0에서 1로) D의 값이 플립플롭에 저장되는 방식이다.

클록이 바뀔 때 데이터에서는 셋업 타임(설정 시간)과 홀드 타임(유지 시간)을 두는데, 셋업 타임에는 입력 신호가 안정적으로 유지돼야 하는지를 나타내고, 클록 에지가 발생한 이후에 얼마나 오랫동안 입력 신호가 안정적으로 유지하는지를 나타낸다.

![image](https://user-images.githubusercontent.com/128434645/232196382-0a168e57-048b-4dcb-96f5-1184b6d4fba8.png)
*[Setup time and Hold time](https://www.vlsi-expert.com/2011/04/static-timing-analysis-sta-basic-part3a.html)*

![image](https://user-images.githubusercontent.com/128434645/232196460-59c72df8-6f7b-42c8-8e8a-22c732d7870c.png)
*[Clock, Data, Q](https://en.wikipedia.org/wiki/Flip-flop_%28electronics%29)*

그림에서 D의 값이 셋업 타임과 홀드 타임을 제외한 나머지 시간에는 D의 값이 변하더라도 출력에 영향이 없음을 알 수 있다. 그리고 전파 지연 시간이 지나야 D입력과 무관하게 안정적으로 유지됨도 알 수 있다. 보통 셋업 타임(**S**et**U**p time)을 t<sub>su</sub>, 유지 시간(Hold time)을 t<sub>h</sub>라고 한다.

## 카운터
위의 플립플롭을 응용한 회로 중에는 순서대로 수를 셀 수 있는 **카운터<sup>counter</sup>**가 있다.

![image](https://user-images.githubusercontent.com/128434645/232197191-b95696d3-da8c-4ae9-a686-1b7db04d99c9.png)
*[3 bit ripple counter](https://www.electricaltechnology.org/2018/05/digital-asynchronous-counter-ripple-counter-types.html)*

이 카운터는 **리플 카운터<sup>ripple counter</sup>**라고 하는데, 물에서 물결이 퍼지듯이 개수를 센 결과가 퍼지기 때문에 리플 카운터라고 부른다. Q<sub>0</sub>이 Q<sub>1</sub>를, Q<sub>1</sub>이 Q<sub>2</sub>를, 비트가 더 있으면 이러한 과정이 계속해서 반복된다(직렬로 연결된 회로의 단점?).

각 비트가 다른 비트의 상태 변화에 따라 약간의 시차를 두고 바뀌기 때문에 **비동기식 카운터<sup>asynchronous counter</sup>**라고 부른다. 언제 결과를 살펴봐야하는지 알기 어렵다는 단점이 있다(각 비트가 다른 비트의 상태 변화에 따라 약간의 텀을 두기 때문에).

그래서 우리들은 상태 변경을 동시화하기 위해서 **동기적 카운터<sup>synchronous counter</sup>**를 설계하기로 했다. 리플 카운터와 달리 동기적 카운터는 상태 변경이 동시에 (동기화되어) 일어나는데 이 말은 플립플롭에 같은 클록을 **병렬로 연결**했다는 사실을 암시한다.

![image](https://user-images.githubusercontent.com/128434645/232197981-dbe4ac89-ba77-46ac-bfe3-7d6e0fb763b0.png)
*[3-bit synchronous binary counter](https://www.iitg.ac.in/cseweb/vlab/Digital-System-Lab/up_counter.php?id=13)*

모든 플립플롭에 같은 클록이 병렬로 들어가기 때문에 이 카운터의 모든 플립플롭의 상태는 동시에 변한다. 위의 리플 카운터와 동기적 카운터 모두 전파 지연을 고려해서 출력이 어느 시점에 올바른지 알아야하지만, 연속적으로 퍼지는 리플 카운터의 단점은 없어졌다.

## 레지스터
이 'D 플립플롭'을 사용하면 그 유명한 **레지스터<sup>register</sup>**라는 회로를 쉽게 구할 수 있다(D 플립플롭을 사용하면 값을 쉽게 기억할 수 있기 때문에). 레지스터는 클록을 공유하는 여러 D 플립플롭을 한 패키지에 집어넣은 것이다.

![image](https://user-images.githubusercontent.com/128434645/232199157-994b96c0-1d05-4cf8-9ef0-a9ff719b30d6.png)
*[4-bit Shift register with flip flop](https://stackoverflow.com/questions/30151197/4-bit-shift-register-with-flip-flop)*

<br><br><br>

# 메모리 조직과 주소 지정
위의 레지스터를 사용하면 여러 비트를 저장할 수 있다. 하지만 더 많은 정보를 저장하려면 어떻게 해야할까? 단순하게 생각하면, 레지스터를 여러개 쌓는 것부터 시작할 수 있을 것이다.

![image](https://user-images.githubusercontent.com/128434645/232289130-61aed5f2-6644-4382-9a40-73e886dabb02.png)
*[SpringerLink](https://link.springer.com/chapter/10.1007/978-3-319-56839-3_13)*

그림처럼 **디코더**와 **레지스터**를 기본 요소로 활용해 레지스터에 각각의 번호를 주는 것으로 어떤 레지스터를 사용할 지 지정할 수 있다. 여기에 레지스터에 각각의 번호를 주는 것을 주소<sup>**address**</sup>라고 한다. 디코더의 출력을 레지스터의 입력을 활성화하는 용도로 한다.

그리고 레지스터의 출력을 선택할 **셀렉터**와 메모리 컴포넌트의 출력을 한 출력으로 연결하는 **트라이스테이트**를 활용해 메모리 회로를 만들 수 있다.

![image](https://user-images.githubusercontent.com/128434645/232289557-959d532b-e7b4-4bbc-8217-6bb93cf6954b.png)
*한 권으로 읽는 컴퓨터 구조와 프로그래밍*

근데 이 회로의 문제는 뭐냐하면, 하드웨어 설계자들이 설계를 할 때 패키지에 집어넣을 때 32비트면 32개가.. 전원도 연결하고.. 이런식으로 설계구상을 하는 부분붙 숨이 턱턱 막힌다는 것이다. 그래서 하드웨어 설계자들은 "굳이 메모리를 동시에 읽고 쓸 필요가 있을까?"라는 생각으로 입/출력 데이터 연결 부분을 합치고 $read/\bar{write}$ 제어신호를 사용해 연결을 많이 줄였다. 이렇게 단순화하면 아래의 스키매틱 기호를 만들 수 있다.
![image](https://user-images.githubusercontent.com/128434645/232289801-748b0a44-011f-4ac7-a2be-df3fa11ee362.png)
*한 권으로 읽는 컴퓨터 구조와 프로그래밍*

그림에서 보면 화살표가 일반적인 → 가 아닌, 커다란 화살표 ⇒ 모양임을 볼 수 있다. 이런 식으로 연관된 신호를 버스<sup>bus</sup>라고 부르고 사람들을 실어나르는 대중교통처럼 비트를 이동시키는 대량의 교통 수단이라고 생각하면 된다(따라서 위 그림처럼 메모리에는 **주소 버스**와 **메모리 버스**가 존재함). 

메모리의 크기가 많아지면 주소에 연결할 비트 수도 많아지는데 보통 주소를 **행(가로)**과 **열(세로)** 부분으로 나눠서 메모리 배열에 지정한다. 
|디코더|열Y0|열Y1|열Y2|열Y3|
|-----|--|--|--|--|
|행Y0|ㅁ|ㅁ|ㅁ|ㅁ|
|행Y0|ㅁ|ㅁ|ㅁ|ㅁ|
|행Y0|ㅁ|ㅁ|ㅁ|ㅁ|
|행Y0|ㅁ|ㅁ|ㅁ|ㅁ|
*열과 행 어드레싱*


이렇게 메모리가 16 장소밖에 없다면 주소에 대해 고민할 필요는 없겠지만, 컴퓨터에는 훨씬 더 많은 메모리가 있고 이런 것들을 처리하기 위해 우리들은 **멀티플렉싱**으로 주소 라인의 수를 반으로 줄인다. 멀티플렉싱한 주소를 저장하기위한 레지스터를 추가해주기만하면 끝난다.
![image](https://user-images.githubusercontent.com/128434645/232292417-271e1495-a765-4427-b730-b6dee07f8e03.png)

주소가 열, 행 2부분으로 나뉘어서 들어오기 때문에 행 주소를 먼저 지정해주고, 열 주소를 변화시키는 식으로 현대의 대형 메모리칩들은 주소를 처리한다.

***메모리 칩의 크기 = 깊이<sup>depth</sup>(행) * 너비<sup>width</sup>(열)***

# 정적 램, 동적 램

정적 램<sup>static RAM</sup> : SRAM이라고 부르고 비용이 비싸지만 속도가 빠르다. 각 비트에 트랜지스터가 6개씩 들어가서 트랜지스터가 공간을 차지하기 때문에 수십억~수조 비트를 저장하기에 좋은 선택이 아니다.

동적 램<sup>dynamic RAM</sup> : DRAM이라고 부르고 **커패시터**라는 아주 작은 버킷에 전자를 담고 트랜지스터를 **1개**만 사용해서 뚜껑을 덮는다. 문제는 전자가 날아가기 때문에 가끔씩 메모리를 **갱신**해주어야 한다.

DRAM은 집적도(단위 면적당 비트 수)가 높기 때문에 큰 메모리 칩에 활용할 수 있다. 주소가 더 많고, 그렇기 때문에 주소 멀티플렉싱(위에서 설명한) 방식을 사용한다.

SRAM과 DRAM은 둘 다 **휘발성** 메모리기 때문에 전원이 끊어지면 데이터가 사라진다. **코어 메모리**는 **비휘발성** 메모리로 비트를 도넛 모양(토러스라고 함)의 쇳조각에 저장한다. 코어는 아주 오래된 기술이지만 '비휘발성'이라는 매력적인 장점이 있기 때문에 요즘에도 코어 메모리와 RAM의 장점을 합친 자기저항성 메모리를 개발하는 연구가 이뤄지고 있다고 한다.

# 읽기 전용 메모리
**R**EAD-**O**NLY-**M**EMORY, ROM이라고 부르며 딱 한 번 쓸 수 있으며 그 이후에는 읽기 밖에 못해서 ROM이라고 부른다(한 번 쓸수는 있네) 전자레인지 같은 프로그램에서는 ROM이 유용하다

가장 초기 형태의 ROM은 역시 IBM카드라고 볼 수 있다. 비트를 종이에 구멍으로 뚫어 표시하는.. 수능이나 학교에서 시험을 치룰 때 쓰는 OMR카드의 초기 버전이라고 생각하면 된다.

![image](https://user-images.githubusercontent.com/128434645/232294788-182564b1-5c81-446b-a3ef-a974fe71fb00.png)

이러한 IBM카드 방식을 **순차적** 메모리라고 하는데, 이 말은 데이터를 일정한 순서로만 읽을 수 있다는 뜻이고 장기적으로 저장하는 데이터를 저장하는 경우에 유용했다.

과거의 프로그래머들은 **마스크 프로그래머블** ROM을 사용했는데, 프로그램을 작성하고 그 비트 패턴을(대단하다) 돈과 함께 반도체 제조사로 보내면 반도체 제조사는 비트 패턴을 마스크로 바꿔서 프로그램이 들어 있는 칩으로 만들어서 돌려주는 방식을 사용했다.

마스크는 너무 비싸기도하고 기다리는 시간도 있기 때문에 **PROM(프로그래머블 읽기 전용 메모리)**가 만들어졌는데, 이 또한 읽기 전용이었기 때문에 프로그램의 오류라도 났다하면 한 장 버리고 한 장쓰고.. PROM이 산처럼 쌓이기 쉬웠다. 그래서 엔지니어들은 PROM 다음으로 **지울 수 있는 읽기 전용 메모리 ERPOM**을 출시했고, 특별한 자외선 빛 아래 넣어두면 저장된 내용을 지울 수 있었다(이게 읽기 전용인가싶다). 이후에는 **전기로 지울 수 있는 읽기 전용 메모리 EEPROM**이 나왔는데 이건 진짜 읽기 전용 메모리가 아니다. 내부 데이터를 아무 순서로나 쓰고 읽을 수 있는데(기술적으로 RAM) 왜 읽기 전용 메모리라고 부르는지 의아하고, 데이터를 쓰는데 시간이 오래 걸리고 RAM보다 비싸서 ROM의 대체제로 쓰였다고 한다.

# 블록 장치
공부를 하면 할 수록 익숙한 친구들이 나오기 시작한다. 

대량 저장장치로 알려진 디스크 드라이브는 정말 많은 데이터를 저장할 수 있다. 저장방식은 고급 중국집을 생각하면 되는데, 음식을 올려놓고 먹고싶은 음식을 테이블을 돌리면 먹을 수 있게 되있는 구조의 원형 테이블을 영화에서든 실제로든 본 적이 있을 것이다. 여기서 원판은 디스크의 판<sup>platter</sup>(비트를 저장하는 곳), 손으로 돌리는건 디스크 헤드<sup>disk head</sup>가 그 역할을 대신해 비트를 저장하고 읽어들인다.

이 디스크 드라이브는 물리적으로 저장하기 때문에 다른 유형의 메모리에 비해 상대적으로 느리고 기계 부품이 시간이 지날수록 마모가 되어 고장나기가 쉽다. 이 문단의 헤더 '블록 장치'의 '블록' 대신 역사적으로 '섹터'라고 불려왔고, 디스크에서 읽기 쓰기가 가능한 가장 작은 단위를 말한다(최근에는 1섹터에 4096byte를 저장함)

# 플래시 메모리와 SSD

## 플래시 메모리
**플래시 메모리**는 가장 최근의 EEPROM 형태의 매체이다. DRAM과 비슷하게 버킷에 전자를 담는 방식으로 작동하지만 이 버킷이 엄청나게 크고 견고하게 만들어져서 **전자가 새지 않는다!** 하지만 뚜껑을 계속 열고 닫고 하다보면 경첩이 느슨해져서 끊어져버린다. RAM처럼 원하는 위치를 마음대로 읽을 수 있고, EEPROM보다 더 빨리 지울수 있고 저렴하다. 하지만 데이터를 기록하기 위해서 먼저 0을 채워 넣어야하는데 이 플래시 메모리는 0을 1로는 바꿀 수 있어도 원하는 비트만 0으로 되돌릴 수는 없다. 전체를 0으로 돌려야하기때문에 내부를 블록으로 나눠서 블록 단위로 지우고 값을 쓸 수 있다. 따라서 플래시 메모리는

읽을 때 - 임의 접근 장치
쓸 때 - 블록 접근 장치

라고 생각할 수 있다.

## SSD
고체 상태 드라이브(Solid-State Drive)라고 하며 최근에 대부분의 하드 디스크가 이 SSD로 교체되고 있다. 디스크 드라이브 모양의 패키지에 넣은 플래시 메모리라고 생각하면 되는데 속도도 빠르고 저장 용량도 많아서 인기가 많다. 플래시 메모리는 점차 낡기 때문에 가능한 모든 블럭이 똑같은 수준으로 낡도록 조정하는 프로세서가 들어 있다.

# 오류 감지와 정정

## 패리티
**패리티<sup>parity</sup>**를 사용하면 1비트만 잘못되어도 이를 감지할 수 있다. 데이터에서 1로 설정된 비트의 개수들을 세고 이 개수가 짝수인지 홀수인지 나타내는 비트를 데이터에 덧붙이는 방식이다.

**짝수 패리티**는 모든 비트를 XOR한 값을, **홀수 패리티**는 XOR한 값의 보수를 사용한다.

|0|1|1|0|0|0|1|1|
|-|-|-|-|-|-|-|-|
이라는 8비트가 있다고 했을 때 0부터 7까지(8개) 서로서로 XOR을 해준다.

```
짝수 패리티 비트
0 1 1 0 0 0 1 1
└┬┘ └┬┘ └┬┘ └┬┘
 1   1   0   0
 └─┬─┘   └─┬─┘
   0       0
   └───┬───┘
       0 ---> 패리티 비트
```

가장 단순한 방법이고, 문제점이 있다 오류가 짝수 번 발생하면 오류가 발생하지 않은 경우와 구분이 불가능하다는 점이다. 패리티는 오류가 '홀수'일 때만 알아낼 수 있다.

***끊임없이 변화하는 데이터를 처리할 때 유용한 패리티***

## 해밍 코드
리처드 해밍이라는 분이 발명한 **해밍코드<sup>hamming code</sup>**는 더 많은 비트를 사용해 더 많은 오류를 감지하고 오류 횟수가 작으면 오류가 일어난 부분을 바로 수정할 수도 있다.

해밍 코드는 각각의 데이터 비트에 추가적인 검사 비트를 추가하여 만들어지는데, 이 검사 비트가 해당 비트와 연관된 다른 비트들의 값을 사용해 오류를 검출하고 수정한다.

***데이터 손실을 최소화하고 안정성을 높일 수 있어 데이터 통신 및 저장시스템에서 사용***

## 체크섬
체크섬(Checksum)은 데이터의 각 지점(예: 바이트)을 $n$비트 값으로 더하고 $n$비트를 넘어가는 값은 무시한다.

체크섬은 일반적으로 데이터 패킷의 끝에 추가되어서 수신 측에서 수신된 데이터와 체크섬을 다시 합산해 검사한다. 이 수신된 데이터에 오류가 있다면 체크섬의 결과(합산 결과)가 일치하지 않아서 오류가 있다는 것을 알 수 있다.

체크섬에는 크게 각 비트의 값에 가중치를 부여하여 합산하는 방법과 일정한 크기의 블록으로 데이터를 나누어 각 블록의 합을 이용해 체크섬을 계산하는 방법이 있는데, 후자의 경우에는 TCP/IP 프로토콜에서 주로 사용된다.

***실시간으로 대량의 데이터를 전송하는 환경에서 유용한 체크섬***

## 순환 중복 검사(CRC)
**순환 중복 검사**라고 하는 친구는 수학적으로 체크섬보다 나은 대체제다(해시 코드도 또 다른 더 나은 대체제다). 데이터 블록의 비트들을 다항식으로 표현하고 이 다항식을 이용해 검사 값을 생성하는데 검사 값을 송신 측에서 생성해 데이터와 함께 전송하면 수신 측에서 수신된 데이터와 함께 이 검사 값을 다시 계산해 오류를 검출한다.

일반적으로 CRC는 체크섬보다 더 강력한 오류 검출 능력을 가지고 있고, TCP/IP, 이더넷, USB등 다양한 곳에서 활용된다.
