---
published: true
title: "우아하게 비동기 처리하기 ✨"
permalink: /CS/asyncHandling
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-07-03
last_modified_at: 2022-07-03
---
****
![]()


# 서론 

이 글은 토스팀의 <a href="https://www.youtube.com/watch?v=FvRtoViujGg">우아하게 비동기처리하기</a> 영상을 요약한 글입니다. <br/>

<!-- 웹서비스, UI 개발에서 가장 다루기 어려운 부분은 무엇인가?  -->

웹은 십여년전 Jquery 같은 라이브러리를 쓰며 명령형 프로그래밍을 하다가  <br/>

React, Vue.js와 같이 **`선언적 프로그래밍`을 지원하는 프레임워크**가 나옴으로써
개발자가 신경써야할 부분이 줄어들었다. <br/>

그럼에도 가장 다루기 어려운 것은 **비동기 프로그래밍** 

# 비동기 프로그래밍 

## 1. 비동기 프로그래밍은 무엇인가? 

> 요약하자면, <br/>
순서가 보장되지 않는 상황이라고 할 수 있다  <br/>

- 비동기처리를 하지 않았을 경우 
  - 웹브라우저가 서버에 요청을 함
  - 서버의 응답만 기다리고 다른 유저 인터렉션에 반응하지 않음
  - 웹브라우저는 그냥 멈춰있게 된다 

- 비동기처리를 했을 경우 
  - 웹브라우저가 서버에 요청을 함
  - 서버의 응답만 기다리는 게 아니라 다른 작업을 하면서 사용자에게 좋은 경험을 보여줌
  - 서버 응답이 돌아오면 다시 이어서 할 일을 한다 

> 이것이 대표적인 비동기 프로그래밍의 모습


## 2. 비동기 프로그래밍이 필요한 이유 

: 끊기지 않는 60프레임의 좋은 사용자 경험을 위해서!  <br/>

Java Script에서 `callback`, `promise`, `observable`과 같이
다양한 도구를 이용해 비동기 상황을 다루고 있다.  <br/>

하지만 아직까지 UI 프로그래밍에서 어려운 부분이다. 왜?  <br/>

> "좋은 코드"에 대한 생각 때문에. 

## 3. 좋은 코드란 

좋은 코드란 무엇인가?  <br/>

자신의 분명한 책임을 드러내는 `함수와 변수`,
`응집도`, `느슨한 결합`, `의존성의 역전` 등 많은 부분에 대한 이야기가 있다.

### 3-1. 예제 (1) 

<img src="/assets/images/async_handling_1.png" /><br/>
￼ 
이 코드는 x.foo.bar.baz 라는 프로퍼티에 안전하게 접근하기 위한 코드이다. 

# 함수의 목적 

이 코드가 하는 일은 결국 <br/>
<strong style="color:black;background-color:yellow">x.foo.bar.baz에 안전하게 접근하는 일 </strong>


이것의 문제점은 무엇인가? 

- 1) 하는 일은 단순한데 코드가 너무 복잡하다
- 2) 각 프로퍼티에 접근하는 핵심 기능이 코드로 잘 드러나지 않는다 

- x.foo가 있는지 검사한다
- x.foo.bar가 있는지 검사한다 

이런 노이즈 명령어가 많아서, 이 함수의 목적이 명확하게 드러나지 않음


# 예제 (1) 개선 

<img src="/assets/images/async_handling_2.png" /><br/>

최근 ECMA script에 추가된 optional chaining을 이용한 코드. 

- 코드가 간결하다
- "성공한 경우"를 생각하는 x.foo.bar.baz와 문법적 차이가 크지 않다
- 함수의 역할을 한눈에 파악할 수 있다 

nullable이 아닐 때,<br/>￼ 
즉 성공할 때 접근하는 모습을 나타내는
x.foo.bar.baz의 표현식과 **큰 차이가 없다**<br/>￼ 
(같은 역할을 하는 식이 비슷한 모습을 한다는 것은 매우 좋은 징조)


### 3-2. 예제 (2)

<img src="/assets/images/async_handling_3.png" /><br/>￼ 

JS에 Promise가 없을 때에 비동기 처리를 위해 callback을 사용함. <br/>￼ 

fetchUserEntity를 호출해서<br/>￼ 
그 결과를 callback으로 받는데, 에러가 있으면 그 에러를 emit한다. <br/>￼ 

그 결과값을 이용해서 사용자의 계좌목록을 가져옴 <br/>￼ 

에러가 있으면 에러를 emit <br/>￼ 

아니면 실제값을 emit <br/>

# 함수의 목적

이 함수가 하는 일은 결국

<strong style="color:black;background-color:yellow">
"user를 가져오고,<br/>￼ 
그 정보를 바탕으로 accounts를 가져오고,<br/>￼ 
그 값을 반환하는 일"</strong>



이것의 문제점은 무엇인가? 

- 1) 성공하는 경우와 실패하는 경우가 나뉘어있지 않다 
  - 실패하는 일에 대한 처리가 섞여서 함수의 목적이 가려졌다. 

- 2) 코드 작성하는 입장에서 매번 에러 유무를 확인해야한다 
  - 매번 비동기 처리를 할 때마다 에러 처리를 해줘야한다


# 예제 (2) - 개선 

<img src="/assets/images/async_handling_4.png" /><br/>
￼
