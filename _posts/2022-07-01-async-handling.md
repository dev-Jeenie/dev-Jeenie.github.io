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

- 만약 컴포넌트가 아닌 함수였다면?

<img src="/assets/images/async_handling_9.png" /><br/>

성공하는 경우만 집중해 복잡도 낮춤
일반적으로 작성하는 동기 로직과 큰 차이 없다


리액트에서, 지금까지 했던 것처럼
hook이나 state를 사용하는 방식으로는 이것처럼 간단하게 비동기 처리를 할 수 없다 

=> 그래서 어렵다 

2개 이상의 로직이 개입해서 복잡해질 때 더욱 어려워진다 

이 문제를 우아하게 해결해주는 도구가 있다. 

바로 React Suspense for Data fetching


React Suspense 

데이터를 가져오기 위한 suspense
아직 리액트 실험버전에서만 사용 가능


## suspense의 목표 

async await 같이 비동기를 처리하면서
"간단하고 읽기 편한 React 컴포넌트를 만들겠다 "

### 예제

<img src="/assets/images/async_handling_10.png" /><br/>
비동기적 동작을 하는 useAsyncValue를
동기적인 동작을 하는 useMemo로 치환을 한 예제. 

완벽히 똑같은 구조를 가진다. 

- 성공한 경우에만 집중
- 로딩 상태와 에러 상태가 분리
- 동기와 거의 같게 사용할 수 있다 

컴포넌트는 성공한 상태만 다루고
에러 상태와 로딩 상태는 외부에 위임하면서
동기적 코드와 큰 차이가 없는 코드를 만드는 것 

React Suspense for Data fetching는 
hook을 만들 수 있는 Low level API를 제공


## 에러 상태와 로딩 상태는 어떻게 분리하는가? 

만약 비동기 작업을 이렇게 처리한다면, 에러와 로딩은 어떻게 처리할까?

<img src="/assets/images/async_handling_11.png" /><br/>

매우 간단하다!
(함수 에러처리를 감싸는 catch문에서 하는 것과 유사) 

- 컴포넌트를 쓰는 쪽에서 로딩 처리와 에러 처리를 한다
- 로딩 상태는 가장 가까운 'Suspense'의 'Fallback'으로 그려진다
- 에러 상태는 가장 가까운 'ErrorBoundary'가 componentDidCatch()로 처리한다 

## try-catch 문과의 유사성

<img src="/assets/images/async_handling_12.png" /><br/>


async-await의 try/catch 문과
ErrorBoundary/Suspense는 거의 유사한 구조 

비동기 콜하는 함수나 컴포넌트가 가운데에 있고
실패하는 경우를 처리하는 부분이 그 부분을 감싸고 있다 

모든 실패할 수 있는 부분에 try catch를 감싸지 않는 것처럼
Suspense를 일으키는 모든 컴포넌트에
Suspense나 ErrorBoundary를 붙이는게 X 

<img src="/assets/images/async_handling_13.png" /><br/>


앱 전체에서 로딩 상태와 에러 상태를 처리해주는 핸들러를 선언한 예제. 

=> 이것처럼 적당한 부분 단위로 에러와 로딩 상태를 한 번에 처리한다! 

## 어떻게 사용하는가? 

비동기를 동기적으로 바꿔주는 Suspense의 사용방법은 간단하다.
사용하는 라이브러리에서 Suspense를 사용한다고 선언하기만 하면 된다. 

<img src="/assets/images/async_handling_14.png" /><br/>

- 1) Recoil의 async selector 기능
- 2) SWR, React Query의 { suspense: true } 옵션 사용 

이런 옵션을 사용한 이후에는 자동으로 컴포넌트의 Suspense 상태가 관리된다 

이렇게 React Query를 사용하면
로딩과 에러 처리를 바깥으로 위임하며 비동기 작업을 동기와 똑같이 처리 가능


## 어떻게 구현되는가? 
ㅈㄹㄴ롱ㅎㅇㅊ옿ㅇ퐇ㄱㅇㅎ

<img src="/assets/images/async_handling_15.png" /><br/>
￼
> React Team의 Sebastian Markbage의 Proof-of-concept
'runPureTask'를 실행시키면, 비동기 함수도 동기적으로 작성할 수 있다 

fetchTextSync는 원래 API호출로 비동기 작업이지만 동기처럼 사용되고 있다. 

이것을 가능하게 하는 건 runPureTask라는 런타임. 

### 토스팀의 예시 

TUBA 메신저의 메시지 상세화면 

<img src="/assets/images/async_handling_16.png" /><br/>


API를 호출해야하는 내용이 다양해서, 상당히 복잡한 비동기 처리가 필요 

=> 비동기 셀렉터 적용!
비동기 리소스를 selector 또는 selectorFamily로 정의할 수 있다 

<img src="/assets/images/async_handling_17.png" /><br/>

￼
templateSetSelector가 no라는 번호를 인자로 받음
=> fetchTemplateSet 비동기 호출을 보냄 

<img src="/assets/images/async_handling_18.png" /><br/>


위에서 정의한 비동기 리소스를 useRecoilValue를 이용해서 가져오려고 하면 Suspense 발생 

useRecoilValue 밑에는 templateSet을 가져왔다는 것을 타입적으로 완전히 보장할 수 있다! 

=> 이렇게 비동기 호출하는 컴포넌트를 적절하게 Suspense로 감싸주기만 하면 된다. 

redux나 다른 도구로 처리했다면 매우 복잡했을 것. 

# 좋은 사용자 경험 

데이터가 준비되는 대로 하나씩 자연스럽게 보여줄 수 있다. 

React suspense 덕분에 많은 비동기 처리를 깔끔하고 우아하게 처리할 수 있고, 코드의 복잡도 또한 줄일 수 있게 되었다. 

# React hooks와의 유사성 

react hooks 또한 비슷한 역할을 한다 

웹서비스의 코드 복잡도를 줄이고,
상태, 이펙트와 메모이제이션과 같이 자주 발생하는 작업들을 매우 쉽게 사용할 수 있게 해줌.



< 웹 서비스 코드 복잡도를 낮춘 방법 > 

react hooks와 Suspense를 비교해보자. 

1. React Hooks 

<img src="/assets/images/async_handling_19.png" /><br/>


react hooks는 어떻게 코드 복잡도를 줄였을까?
선언적인 API의 역할이 크다. 

이전의 Class component에서는 다양한 작업을 명령형으로 해줘야했다.
하지만 hooks로는 

- useState 상태를 사용한다고 선언
- useMemo 메모이제이션 한다고 선언
- useEffect 효과를 발생시킨다고 선언 

이렇게 선언만 하면 React 프레임워크가 실제 작업을 대신 해줬다. 

2. Suspense

<img src="/assets/images/async_handling_20.png" /><br/>


컴포넌트에서는 비동기적 리소스 선언
그 값을 읽어온다고 선언하기만 함.
그럼 실제 에러상태나 로딩상태 처리는 부모컴포넌트가 대신 한다.



에러처리의 복잡도를 낮춘 방법 이미지 

실패할 수 있는 함수는 throw문으로 에러를 발생시키고,
실제 에러처리는 컴포넌트를 감싸는 부모 함수가 대신 수행함 

대수적효과 이미지 

어떤 코드 조각을 감싸는 맥락으로 책임을 분리하는 방식을 대수적효과라고 한다. 

객체지향의 의존성 주입(DI), 의존성 역전(IoC)와 유사 

대수적 효과를 지원하는 언어에서
함수는 필요한 코드조각을 선언적으로 사용한다 

(메모이제이션이 필요하면 useMemo를 호출하는 방식) 

그럼 실제로 관련된 처리는 함수를 감싸는 부모 함수나, 런타임이 대신 처리하는 방식이다


# 추가적인 사용자 경험 향상의 방법 

추가적인 이미지 

React에서 컴포넌트의 렌더 트리를 부분적으로만 완성함으로써 사용자 경험을 크게 향상시킬 수 있다. 

=> 비동기작업 뿐만 아니라, 기존에 debounce 등으로 처리하던 무거운 동기적 작업에도 적용가능!