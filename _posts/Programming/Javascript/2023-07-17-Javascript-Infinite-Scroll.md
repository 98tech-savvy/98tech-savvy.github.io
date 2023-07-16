---
title:  "자바스크립트(JavaScript)의 무한 스크롤 API"
excerpt: "자바스크립트의 무한스크롤 API(Infinite Scroll API)인 IntersectionObserver를 사용해보자."

categories:
  - Javascript
tags:
  - [자바스크립트, 무한스크롤, IntersectionObserver]

toc: true
toc_sticky: true

date: 2023-07-17
last_modified_at: 2023-07-17
---

유튜브나 인스타그램, 페이스북같은 여러 페이지에서는 스크롤을 내리면 짧은 시간 뒤에 컨텐츠들이 로드되는 UX(User eXperience, 사용자 경험) 방식을 사용하고 있다.

만약 페이지를 만드는 웹 개발자가 이러한 스크롤 방식을 구현하려면 **스크롤을 할 때마다 이벤트를 발생시키는 방법**이나 자바스크립트 API인 **IntersectionObserver**를 사용해 구현할 수 있다. 하지만 전자의 경우 코드가 복잡해지고 로직이 쌓이면서 버그가 발생할 수 있기 때문에 만들어진 API를 활용하는게 좋은 방법이라 생각한다.

# IntersectionObserver

IntersectionObserver 인터페이스는 기본적으로 브라우저의 뷰포트(Viewport)와 API내에서 설정한 요소(Element)의 교차점을 관찰해서 요소가 뷰포트에 있는지, 없는지(사용자 화면에 있는지 없는지)를 구별하는 기능을 제공한다.

## 생성
``new IntersectionObserver()``를 통해 생성한 인스턴스로 관찰할 대상을 등록하고 관찰대상을 지정할 수 있다. 이 때 생성자는 2개의 인수(callback, options)를 가진다.

```js
const obs = new IntersectionObserver(callback, options);
observer.observe(element)
```

### callback
관찰자가 타겟(관찰대상)에 변화가 생기거나, 등록했을 때 callback 함수를 실행시킨다. callback은 2개의 인수(entries, observer)를 가진다.

#### entries
[IntersectionObserverEntry](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry)에서 여러 속성들을 확인할 수 있다.

#### observer
callback이 실행되는 해당 인스턴스를 참조한다.

### options

```js
const options = {
    root: null,
    rootMargin: '0px 0px 0px 0px'
    threshold: 0, 
};
```

#### root
뷰포트 대신 사용할 요소 객체(루트 요소)를 지정한다. 이 때 지정해주지않으면 기본 값은 뷰포트(null)이다.

#### rootMargin
바깥 여백(margin)을 이용해 root의 범위를 확장하거나 축소할 수 있다. px나 %로 나타낼 수 있다.

CSS의 Margin을 생각하면 편함.

#### threshold
타겟의 가시성이 얼마나 필요한지를 백분율로 표시한다.
예를 들어 ``threshold: 0.3``일 때 타겟의 가시성이 30%일 때 옵저버가 실행된다.