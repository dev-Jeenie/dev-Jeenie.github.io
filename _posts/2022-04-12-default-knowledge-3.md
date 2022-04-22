---
published: true
title: "👩🏻‍💻 배경지식 쌓기 Step (3) - AJAX, CORS, 브라우저 동작 원리, 웹 접근성"

permalink: /cs/defaultKnowledge3
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-04-21
last_modified_at: 2022-04-21
---
****
![]()

> 들어가기 전 <br/>

https://joshua1988.github.io/web-development/interview/frontend-questions/
<br/>
https://github.com/JaeYeopHan/Interview_Question_for_Beginner
<br/>
https://jbee.io/essay/for_junior_frontend_developer/
<br/>

위의 글들을 참조하여 배경지식을 찬찬히 쌓아보자.<br/>

## 1. AJAX (Asynchronous Javascript And XML)


비동기적으로 자바스크립트와 XML을 이용하는 방식(정보 교환 기법).<br/>

- 자바스크립트를 이용해 서버와 브라우저가 **비동기 방식으로 데이터를 교환**할 수 있는 통신 기능
- 브라우저가 가지고 있는 `XMLHttpRequest` 객체를 이용해 전체 페이지를 새로 고침하지 않고 일부 데이터만 로드하는 방법

자바스크립트로 서버에 데이터를 <strong style="color:black;background-color:yellow">**비동기 방식으로 요청**</strong>하는 것!

> 여기서 XMLHttpRequest 란? <br/>
> XMLHttpRequest allows JavaScript to make HTTP requests, and is the most basic part of AJAX. It allows a website to dynamically request more content, without reloading the entire page.<br/>
XMLHttpRequest는 자바스크립트가 HTTP 요청을 할 수 있게 하는 AJAX의 가장 기본적인 부분입니다. XMLHttpRequest는 웹사이트로 하여금 전체 페이지를 새로고침하지 않고도 더 많은 데이터를 요청을 할 수 있게 합니다.<br/>

출처 : https://webplatform.github.io/docs/apis/xhr/XMLHttpRequest/

여기서 중요한 부분은<br/>
`XMLHttpRequest` 객체를 사용하면 클라이언트는 **전체 페이지를 다시 로드하지 않고도** URL에 HTTP 요청을 할 수 있다는 것. <br/>




### 1-1. AJAX를 왜 쓰는거야?

=> ***비동기적*으로 요청하고 싶기 때문에!**<br/>

AJAX가 등장하기 이전에는, 웹 브라우저가 데이터를 요청하면 서버가 정보를 통째로 보내줬다.<br/>

동일한 소스임에도 새로운 데이터를 요청할 때마다 **모든 페이지를 새로 그리기 때문에**,<br/>
서버와 클라이언트 모두에게 안좋은 영향을 미친다.<br/>

그래서 `비동기적`으로 정보를 요청하는 기술이 필요해졌다.<br/>
모든 페이지를 랜더링한 뒤에도 필요에 따라서 데이터를 받아올 수 있도록 하는 것이다.<br/>
일부 데이터만 가져와서 변경할 수 있다면 클라이언트는 렌더링을 조금만 해서 부담을 덜고,<br/>
서버는 데이터를 조금만 보내서 부하가 적게 걸릴 것이다.<br/>

> 비동기 방식이란?<br/>
웹페이지를 새로고침하지 않고도 데이터를 불러오는 방식.<br/>
AJAX를 통해 서버에 데이터를 요청을 한 뒤에도 멈추지 않고 프로그램은 계속 돌아간다.<br/>

동기방식과 비동기방식<br/>
  <img src="/assets/images/default_3_async_2.jpeg" /><br/>
예제 )<br/>
  <img src="/assets/images/default_3_async_1.jpeg" /><br/>



### 1-2. AJAX를 사용 가능하게 만드는 것들
AJAX라는 기술은 여러가지 기술이 혼합적으로 사용되어 이루어진다.

- HTML
- DOM
- JavaScript
- XMLHttpRequest
- Etc


### 1-3. AJAX를 사용하는 이유

간단하게 말하자면 **페이지 전체를 새로고침하지 않기 위해서** 사용한다고 볼 수 있다.<br/>

HTTP 프로토콜은 클라이언트에서 request를 보내고, 서버에서 response를 받으면 이어져있던 연결이 끊긴다.<br/>
그래서 화면을 업데이트하기 위해서는 다시 request와 response의 과정을 거쳐야해서 페이지가 새로고침이 되어버린다.<br/>

AJAX는 HTML 페이지 전체가 아닌 일부분만 갱신할 수 있도록 **`XMLHttpRequest 객체`를 통해** 서버에 request한다.<br/>
JSON이나 XML형태로(보통 JSON을 사용한다) 필요한 데이터만 받아 갱신하기 때문에 그만큼의 자원과 시간을 아낄 수 있다.<br/>









## 2. CORS(Cross Origin Resource Sharing)

  <img src="/assets/images/cors.jpeg" /><br/>
  <img src="/assets/images/cors_1.png" /><br/>

CORS 정책이란 우리가 가져오는 리소스가 안전한지 검사하는 관문이다. <br/>

Cross Origin Resource Sharing를 직역하면 **교차 출처 리소스 공유**를 뜻한다. <br/>
여기서 말하는 `교차 출처`는 `다른 출처`를 의미한다. <br/>

웹 생태계에는 **다른 출처로의 리소스 요청을 제한**하는 것과 관련된 두 가지 정책이 존재한다.<br/>

- **CORS(Cross Origin Resource Sharing)**
- **SOP(Same-Origin Policy)**
  - `같은 출처에서만` 리소스를 공유할 수 있다
  - 단, CORS 정책을 지킨 리소스 요청은 출처가 다르더라도 허용

다른 `출처`로 리소스를 요청한다면 SOP 정책을 위반하게 되고,<br/> SOP의 예외조항인 CORS 정책을 지키지 않으면 아예 다른 `출처`의 리소스를 사용할 수 없게 되는 것이다.<br/>


그럼 이 ***`출처`***라는 게 대체 뭘까? <br/>



### 2-1. 출처(Origin)란?

https://www.naver.com/ 와 같은 URL은 여러개의 구성요소로 이루어져있다.<br/>

  <img src="/assets/images/cors_origin.png" /><br/>
  이미지 출처 : https://evan-moon.github.io/2020/05/21/about-cors/<br/>

  출처(origin)는 protocol과 host, 생략이 가능한 포트번호까지 모두 합친 것을 의미한다. <br/>

> 포트번호가 왜 생략이 가능해?<br/>
각 웹에서 사용하는 HTTP, HTTPS 프로토콜의 기본 포트번호가 정해져있기 때문에 생략이 가능한 것.<br/>



### 2-2. 이렇게 귀찮은 정책을 왜 만들어서?

개발자 입장에서는 이런 정책 때문에 번거로울 수 밖에 없다. 어차피 개발자는 정해진 서버하고만 통신하도록 만들텐데.... <br/>

하지만 웹 브라우저의 개발자 도구만 열어봐도 그 이유를 알 수 있다. 구조가 어떻게 작성되어있는지, 서버와 어떻게 어떤 방식으로 통신을 하는지, 출처는 어디인지 등의 모든 정보를 제재없이 열람할 수 있기 때문이다. <br/>

이런 상황 속에서 다른 출처의 어플리케이션이 서로 통신하는 것에 대해 아무런 제약도 존재하지 않는다면, 악의를 가진 사용자가 소스 코드를 쓱 구경한 후 CSRF(Cross-Site Request Forgery)나 XSS(Cross-Site Scripting)와 같은 방법을 사용하여 여러분의 어플리케이션에서 코드가 실행된 것처럼 꾸며서 사용자의 정보를 탈취하기가 너무나도 쉬워진다.<br/>



### 2-3. 출처 비교 방법

`Scheme`, `Host`, `Port`가 동일하면 두개의 출처가 같다고 판단하는 로직이다.

https://dev-jeenie.github.io:80  를 예로 들자면,<br/>

- **`Scheme`** : https://
- **`Host`** : dev-jeenie.github.io
- **`Port`** : :80

이 세가지만 같다면, 나머지가 다르더라도 같은 출처로 인정이 된다.<br/>


그리고 이러한 출처 비교 로직은 서버에 구현된 로직이 아닌 ***브라우저 자체에 구현되어있는 로직***이다.<br/>

만약 서버가 같은 출처에서 보낸 요청만 받겠다는 로직을 가지고 있는 경우가 아니라면,<br/>
CORS 정책을 위반하는 요청을 했다 하더라도 **서버는 정상적으로 응답**을 한다.<br/>
하지만 ***브라우저가 이 응답을 분석***해서 CORS 정책을 위반했다고 판단하면 이 응답을 보여주지 않고 갖다 버리는 것이다.<br/>

  <img src="/assets/images/cors_brower.png" /><br/>

이것이 왜 중요하냐면?<br/>
서버 간 통신에는 정책이 적용되지 않는다. 따라서 서버 입장에서는 정상적 요청을 받고 정상적 응답을 했다고 나오기 때문에, CORS 정책 위반사항을 모른다면 영문을 알 수가 없기 때문이다.<br/>


  

<!-- 

  <img src="/assets/images/cors_1.png" /><br/>


> 'https://api.lubycon.com/me'에서 오리진 'https://localhost:3000'으로 가져올 수 있는 액세스가 CORS 정책에 의해 차단되었습니다. 요청된 리소스에 'Access-Control-Allow-Origin' 헤더가 없습니다. 불투명한 응답이 필요에 적합한 경우, 요청 모드를 '노코어'로 설정하여 CORS가 비활성화된 리소스를 가져오십시오.<br/>


이는 HTTP 요청에 대해서 어떤 요청을 하느냐에 따라 각기 다른 특징을 가지고 있기 때문이다.

HTML → 기본적으로 Cross-Origin 정책을 따름
link 태그에서 다른 origin의 css 등의 리소스에 접근하는 것이 가능
img 태그등에서 다른 리소스에 접근하는 것이 가능
XMLHttpRequest, Fetch API 등 script 태그 내 → 기본적으로 Same-Origin 정책을 따름
자바스크립트는 서로 다른 도메인에 대한 요청을 보안상 제한한다. (브라우저 기본 설정은 하나의 서버 연결만 허용)
이 정책을 Same-Origin-Policy라고 한다.



 -->



## 3. 웹 브라우저 작동 원리

### 3-1. 












## 4. 웹 접근성







> 참조
<br/>
https://velog.io/@surim014/AJAX%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
<br/>
https://webplatform.github.io/docs/apis/xhr/XMLHttpRequest/
<br/>
https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F#thankYou
<br/>
https://evan-moon.github.io/2020/05/21/about-cors/