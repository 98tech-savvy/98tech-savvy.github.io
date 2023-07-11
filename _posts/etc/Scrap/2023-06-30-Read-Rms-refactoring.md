---
title:  "[Read] 코드 악취를 맡는 후각 훈련의 시간"
excerpt: "홍혜린님의 개발자로써 읽어보기 좋은 글"

categories:
  - Read
tags:
  - [Read, 읽어볼만한 글, 개발자 글, 취업준비생]

toc: true
toc_sticky: true
 
date: 2023-06-30
last_modified_at: 2023-06-30
---

# [코드 악취를 맡는 후각 훈련의 시간, 홍혜린님](https://helloworld.kurly.com/blog/rms-refactoring/)

<h2 id="리팩토링의-시작">리팩토링의 시작</h2>
<p>모든 프로젝트에는 저마다의 사연이 있을 텐데요.</p>

<p>제가 담당하게 된 RMS(Receiving Management System - 입고관리 시스템)는 프로젝트 초기에 많은 부분이 미흡한 상태에서 진행되었습니다.
성능이나 기능상 이슈는 없었지만, 프로젝트의 시작부터 함께하셨던 유일한 동료분 께서는 큰 아쉬움을 안고 늘 이야기 하셨습니다.</p>
<blockquote>
  <p>조금만 수정해서 될 일이 아니다. 시간만 있다면 다 갈아엎고 싶다</p>

  <p>아예 새로 짜는 것이 낫지 않을까요?</p>
</blockquote>

<p>1명이었던 개발자는 어느덧 3명이 되었고, 큰 미션들을 어느 정도 끝내고 나자 저희에게 리팩토링을 위한 한 달여의 시간이 주어졌습니다.
막상 리팩토링만을 위한 시간이 주어지자, 짧지 않은 기간에 합당한 결과물을 만들어 내야 한다는 부담감과 어디서부터 어떻게 진행해야 하나 막막함이 밀려왔습니다.</p>

<h2 id="무엇을-리팩토링-해야-할까">무엇을 리팩토링 해야 할까?</h2>
<blockquote>
  <p>프로그램의 악취를 제거하기 위해서는 악취를 맡아야 한다.</p>

  <p>그런데, 무슨 냄새가 악취인 거죠..?</p>
</blockquote>

<h3 id="리팩토링-대상과-범위를-분류하자">리팩토링 대상과 범위를 분류하자</h3>

<p>프로젝트의 크기가 작지는 않았기 때문에 무작정 모든 소스에서 리팩토링 대상을 추출할 수는 없었습니다.</p>

<p>먼저 메인 기능과 코드의 유사성(비슷한 동작을 하지만 도메인만 다른 기능들)을 기준으로 파트를 8개로 분류했습니다.
그리고 3차로 나누어 리팩토링을 진행하고, 각 단계별로 QA 검증을 거쳐 나누어 배포하기로 하였습니다.</p>

<p>그중 1차는 함께 진행해보며 리팩토링의 기준과 과정을 정의하고 공유하기로 했습니다.</p>

<p><img src="/post-img/rms-refactoring/refactoring-category.png" alt="리팩토링 범위분류"></p>

<h3 id="최소한의-기준을-만들자">최소한의 기준을 만들자</h3>
<p>명확한 기준 없이 자체적으로 대상을 찾아오는 것은 너무나 막막하고 정리하기도 어려운 일이었습니다.
저희는 하던 일을 접어두고 <code class="language-plaintext highlighter-rouge">리팩토링과 관련된 책을 최소 1권 이상 읽기</code> 미션을 수행했습니다.
그리고 협의하여 아래와 같은 기준을 만들고 조건을 만족하는 코드를 만났을 때 무조건 멈춰서 고민해보기로 했습니다.</p>

<blockquote>
  <ul>
    <li>30라인이 넘는 코드</li>
    <li>3중 이상의 중첩 조건문</li>
    <li>5개 이상의 parameter 사용</li>
    <li>사용하지 않는 method, class or package import</li>
    <li>주석 안의 코드</li>
    <li>불필요한 로그, 주석</li>
    <li>의미가 모호한 method, class 명</li>
  </ul>
</blockquote>

<h2 id="어떻게-리팩토링-해야-할까">어떻게 리팩토링 해야 할까?</h2>
<blockquote>
  <p>리팩토링 대상을 어떻게 효율적으로 공유하며, 같은 방향을 바라보고 진행할 수 있을까?</p>

  <p>리팩토링 후, 원래 잘 되던 로직이 안되면 어떡하지?</p>
</blockquote>

<h3 id="리팩토링-대상-로직과-리팩토링-방향을-todo로-작성하자">리팩토링 대상 로직과 리팩토링 방향을 TODO로 작성하자</h3>
<p>리팩토링 대상을 각자 찾아오기로 했을 때, 각각 메모장, 엑셀, TODO 형태로 정리해왔습니다.
이 중에 개발 툴에서 확인이 편리한 TODO 형태로 정리하기로 협의했습니다.</p>

<p>같은 리팩토링 방향을 가지고 있는 비슷한 코드도 혹시나 놓칠 수도 있기에 모든 라인에 TODO를 작성했습니다.</p>

<p><img src="/post-img/rms-refactoring/refactoring-todo.png" alt="리팩토링대상추출TODO"></p>

<p>처음에는 이 코드가 <code class="language-plaintext highlighter-rouge">어떤 기준에 부합하여 리팩토링 대상이 되었는지</code>와 <code class="language-plaintext highlighter-rouge">이렇게 변경되면 좋을 것 같다</code>는 의견을 각자 작성하고
팀 내 리뷰를 통해 결론적으로 <code class="language-plaintext highlighter-rouge">어떠한 형태로 변경하자!</code>라는 방향을 기록하도록 했습니다.</p>

<h3 id="이미-개발된-로직에-대한-테스트-코드를-작성해보자">이미 개발된 로직에 대한 테스트 코드를 작성해보자</h3>
<p>당장은 필요 없어 보여도 과거의 나는 분명 이유가 있어서 그렇게 했을 거라 믿고, 과거 로직에 대한 테스트 코드를 작성했습니다.
모든 레벨에 대한 테스트 코드를 작성하고 싶었지만, 여건상 서비스 레벨의 mock 테스트만 작성했습니다.
가능한 한 모든 분기를 다 커버할 수 있도록 노력했습니다.</p>

<p><del>여기서 포기할 뻔했어요</del></p>

<p><img src="/post-img/rms-refactoring/refactoring-testcode.jpeg" alt="테스트코드작성"></p>

<h3 id="리팩토링-후-기존-기능-수행-여부를-검증해보자">리팩토링 후 기존 기능 수행 여부를 검증해보자</h3>
<p>리팩토링 후, return type이나 parameter 변경 등으로 인한 컴파일 오류만 제거한 뒤 테스트 코드를 실행했습니다.
생각보다 한 번에 모든 테스트가 통과하여 <code class="language-plaintext highlighter-rouge">어떻게 한 번에 되지?</code> 하는 불안함이 있었지만, 실제 로컬서버를 실행시켜 진행한 테스트에서도 정상적으로 데이터가 처리되는 것을 확인할 수 있었습니다.
그리고 저희 개발자 마음에 평화와 안정을 선물해주시는 QA 팀분들께서도 꼼꼼히 통합테스트를 진행해 주셨습니다.</p>

<p><img src="/post-img/rms-refactoring/refactoring-qa.png" alt="리팩토링 QA"></p>

<h2 id="그래서-뭐가-좀-나아졌을까">그래서 뭐가 좀 나아졌을까?</h2>
<blockquote>
  <p>한 달이라는 시간, 3명의 개발자가 투입되었다</p>

  <p>성능 이슈가 있었던 것도 아니었기에 겉으로는 티가 나지 않는 리팩토링의 결과를 어떻게 보여줄 수 있을까?</p>
</blockquote>

<h3 id="코드는-확실히-나아진-것-같은데">코드는 확실히 나아진 것 같은데</h3>

<h4 id="string-상수가-덕지덕지-exception-제거">String 상수가 덕지덕지 Exception 제거</h4>
<p>화면에 친절한 오류 메시지를 전달하기 위해 메시지만 지정하는 <code class="language-plaintext highlighter-rouge">RuntimeException</code>을 생성해서 사용중이었습니다.
조회하고자 하는 상품을 찾지 못한다는 exception이 여러 곳에서 발생하는데 메시지도 제각각에, <code class="language-plaintext highlighter-rouge">GoodsNotFound</code>라는 별도의 custom exception을 생성한 코드도 있었습니다.
<code class="language-plaintext highlighter-rouge">String</code> 상수의 사용도 줄이고, 테스트 코드 작성 시 원하는 에러가 발생했는지 확인하기 위하여 개선이 필요하다고 판단했습니다.
이에 <code class="language-plaintext highlighter-rouge">ExceptionType</code> 이라는 오류메시지를 속성으로 갖는 <code class="language-plaintext highlighter-rouge">enum</code>을 추가하고 이를 exception을 생성하고 검증하는데 사용했습니다.</p>

<p><img src="/post-img/rms-refactoring/refactoring-exception.png" alt="리팩토링 Exception"></p>

<h4 id="잘못된-공통코드-재분리">잘못된 공통코드 재분리</h4>
<p>검수와 검품 완료 정보를 처리하는 로직은 초기 아름다운 형태와 목적으로 공통함수로 분리되었었습니다.
하지만 이후, 각각에 맞는 내용이 추가되면서 공통코드에는 검수/검품 여부를 구분하는 수많은 <code class="language-plaintext highlighter-rouge">if</code> 문이 추가되었습니다.
그리고 그 <code class="language-plaintext highlighter-rouge">if</code>를 설명해야 하는 주석들도 추가되었습니다. 각자 처리하는 것이 더 가독성이 있을 것 같아 다시 분리했습니다.</p>

<p><img src="/post-img/rms-refactoring/refactoring-wrong-common.png" alt="리팩토링 WrongCommon"></p>

<h4 id="코드-라인-감소">코드 라인 감소</h4>
<p>코드량이 줄어든 것이, 절대적으로 더 나은 코드가 된 것을 보장할 수는 없습니다.
하지만 코드의 가독성을 높이니 자연스럽게 줄어들었습니다.</p>

<ul>
  <li>
    <p><code class="language-plaintext highlighter-rouge">CompletionService</code></p>

    <p>** 리팩토링 이전
  <img src="/post-img/rms-refactoring/refactoring-line-before_1.png" alt="리팩토링결과-라인수-before1"></p>

    <p>** 리팩토링 이후
  <img src="/post-img/rms-refactoring/refactoring-line-after_1.png" alt="리팩토링결과-라인수-after1"></p>
  </li>
</ul>

<hr>
<hr>

<ul>
  <li>
    <p><code class="language-plaintext highlighter-rouge">InspectionService</code></p>

    <p>** 리팩토링 이전
  <img src="/post-img/rms-refactoring/refactoring-line-before_2.png" alt="리팩토링결과-라인수-before2"></p>

    <p>** 리팩토링 이후
  <img src="/post-img/rms-refactoring/refactoring-line-after_2.png" alt="리팩토링결과-라인수-after2"></p>
  </li>
</ul>

<h4 id="테스트-코드-커버리지-증가">테스트 코드 커버리지 증가</h4>
<p>코드의 신뢰도가 상승했습니다.</p>

<ul>
  <li>
    <p>Service level Code Coverage</p>

    <p>** 리팩토링 이전
  <img src="/post-img/rms-refactoring/refactoring-cover-before_1.png" alt="리팩토링결과-커버리지-before1"></p>

    <p>** 리팩토링 이후
  <img src="/post-img/rms-refactoring/refactoring-cover-after_1.png" alt="리팩토링결과-커버리지-after1"></p>
  </li>
</ul>

<h3 id="우리도-나아갔을까">우리도 나아갔을까?</h3>
<p>코드가 개선된 만큼 저희도 발전 할 수 있었습니다.</p>

<h4 id="팀원-간의-프로젝트-이해도-상향-평준화">팀원 간의 프로젝트 이해도 상향 평준화</h4>
<p>입사 시기와 팀 합류 시기에 따라, 주어진 업무 외에 전체적인 프로젝트를 완전히 파악하기는 힘듭니다.
이에 저희는 의도적으로 리팩토링 담당 파트를 메인으로 담당하던 기능 외 파트가 될 수 있도록 진행했습니다.
리팩토링 대상을 추출하고 리팩토링을 진행하고 테스트코드를 작성하며 프로젝트 전체에 대한 이해도가 상향 평준화되었습니다.</p>

<h4 id="테스트-코드-작성-거부감-줄이기">테스트 코드 작성 거부감 줄이기</h4>
<p>TDD를 시도해보다가 그 막막함에 포기해본 경험, 한 번쯤 있으실 거라고 생각합니다.
비록 구현된 코드의 테스트 코드 작성이었지만, 수십 개의 코드를 작성하며 테스트 코드에 대한 거부감과 두려움이 줄어들었습니다.</p>

<h4 id="코딩의-시야가-넓어짐">코딩의 시야가 넓어짐</h4>
<p>이 코드가 왜 리팩토링 대상인지, 리팩토링한다면 어떤 식으로 개선되어야 할 지
리팩토링 대상을 추출하는 과정에서 다양한 사람들의 의견을 나눴습니다.</p>

<p>리팩토링을 진행하며, 리뷰 당시 찾지 못했던 부분도 추가로 눈에 보이는 것을 느꼈습니다.
<code class="language-plaintext highlighter-rouge">null</code> 처리, <code class="language-plaintext highlighter-rouge">Optional</code>, <code class="language-plaintext highlighter-rouge">Stream</code> 사용법 등 평소에 생각하지 못했던 부분이나 습관처럼 잘못 사용하고 있던 부분에 대해 시야가 넓어지고 개선되었습니다.</p>

<h2 id="이-또한-리팩토링-대상">이 또한 리팩토링 대상</h2>
<p>현재 작성 시점을 기준으로 리팩토링은 2차까지 완료되어 배포된 상황이고 3차는 진행 예정 중에 있습니다.
3차까지 완료된다고 해도 리팩토링은 끝이 아닐 겁니다. 지금 최선을 다해 개선한 코드도 시간이 지나면 또 리팩토링이 필요한 코드가 되겠죠.
처음부터 잘 짜는 것도 중요하지만 개선하고 유지하는 것 또한 중요하다고 생각합니다.
시간이 촉박하다, 다른 할 게 많다는 이유로 많은 회사와 개발자들이 리팩토링만을 위한 기간을 할애하기가 쉽지 않습니다.
이러한 과정이 필요함에 공감하고 그 기회를 주고 배려해주신 많은 분께 감사드립니다.</p>

<p>물류개발팀은 냄새를 잘 맡는 개코 개발자분들도, 함께 훈련하실 비염 개발자분들도 환영합니다 :)</p>

<p>채용공고를 <a href="https://www.wanted.co.kr/wd/7799">Java 서버 개발자(물류시스템)</a> 참고해주세요.</p>
