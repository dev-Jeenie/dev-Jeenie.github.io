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

async - await를 사용한 경우. <br/>

- 코드가 간결하다
- 비동기 요청이 "성공한 경우"만 다루고, "실패한 경우"는 catch 절에서 분리한다
- "실패한 경우"에 대한 처리를 외부에 위임할 수 있다

성공 경우만 모아져 있어서 함수의 역할이 명확하게 드러난다<br/>
이 함수는 ***성공하는 부분만 책임***지고, 다른 경우는 외부에 더 ***잘할 수 있는 부분에 위임***한 것!<br/>

=> 좋은 코드의 징조 <br/>

### 3-3. 좋은 코드의 특징

- 성공, 실패의 경우를 분리해서 처리할 수 있다
- 따라서 비즈니스 로직을 한눈에 파악할 수 있다

<strong style="color:black;background-color:white;font-weight:bold">함수의 책임이 명확하게 드러나는 것 ! </strong> <br/>


### 3-4. 나쁜 코드의 특징

- 성공, 실패의 경우가 섞여서 처리된다
- 따라서 비즈니스 로직을 파악하기 어렵다

함수의 크기가 커지고, <br/>
<strong style="color:black;background-color:white;font-weight:bold">함수가 하는 역할이 명시적으로 드러나지 않는다 </strong> <br/>


## 4. 지금까지 비동기 처리를 어떻게 했는가?


<img src="/assets/images/async_handling_5.png" /><br/>

promise를 반환하는 함수를 React hook의 인자로 넘기고, <br/>
 promise의 상태 변화에 따라 hookd이 반환하는 data, error 의 값을 적절히 채워주는 것 <br/>

<img src="/assets/images/async_handling_6.png" /><br/>

비동기인 foo를 가져오는데<br/>
foo가 에러라면 실패 메시지,<br/>
foo가 없으면 로딩 중,<br/>
foo가 있으면 안녕하세요 메시지.<br/>

***문제점***

- 성공, 실패가 섞여서 처리된다
- 실패의 처리를 외부에 위임하게 어렵다

# 비동기 작업이 여러개라면 더 심각해진다

<img src="/assets/images/async_handling_7.png" /><br/>

foo와 bar 값을 비동기로 가져오고, bar를 가져오려면 foo가 있어야하는 상황. <br/> 

bar는 foo의 로딩까지 기다리고, if문은 복잡해진다. <br/>

<img src="/assets/images/async_handling_7.png" /><br/>

# 비동기 작업의 일반적인 상태는

***한개일 경우***
- 로딩 중
- 에러
- 완료됨

> 그럼 두개일 경우의 상태는, 9가지 경우의 수를 가지게 된다. <br/>
***비동기 호출이 많아질 수록 더욱 복잡해진다!*** <br/>




# ***React에서의 비동기 처리는 매우 어렵다***

- 성공하는 경우에만 집중해서 컴포넌트를 구성하기 어렵다
- 2개 이상의 비동기 로직이 개입할 때, 비즈니스 로직을 파악하기 점점 어려워진다

# 만약 컴포넌트가 아닌 함수였다면?

