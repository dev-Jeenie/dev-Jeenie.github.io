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
  
> 이미지 출처 : https://evan-moon.github.io/2020/05/21/about-cors/<br/>

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

### 3-1. 브라우저란?

웹 브라우저는 동기적(Synchronous)적으로 (HTML + CSS), Javascript 언어를 해석해서 내용을 화면에 보여주는 응용 소프트웨어이다.<br/>
크롬, 인터넷 익스플로러 등 인터넷 프로그램을 예로 들 수 있다.<br/>

#### 3-1-1. 웹 브라우저가 동기적인 이유

- script 태그를 body 태그 하단에 위치시킨다. 왜?
  - script 로딩지연으로 인해 HTML 요소들이 렌더링에 지장을 받는 일이 생기지 않아 페이지 로딩 시간이 단축된다
  - DOM이 완성되기 전에 script 가 DOM을 조작한다면 에러가 발생한다
  - 자바스크립트는 렌더링 엔진이 아닌 자바스크립트 엔진이 처리한다


### 3-2. 브라우저의 주요 기능

- 사용자가 참조하고 싶은 웹페이지(자원)를 `서버에 요청`하고, `서버의 응답`을 받아 브라우저에 **보여주는 것**

`서버의 응답`은 주소를 통해 요청하는데, 이 주소를 **`URI(Uniform Resource Identifier)`**라고 한다.<br/>

브라우저는 HTML, CSS의 명세에 따라 HTML파일을 해석해서 표시하는데, 이명세는 웹표준화 기준인 W3C에서 정한다.<br/>



#### 3-2-1. URI(Uniform Resource Identifier)이란?



### 3-3. 브라우저의 기본구조

<img src="/assets/images/browser_work.png" /><br/>
> 출처 : https://d2.naver.com/helloworld/59361<br/>


- 1) **`사용자 인터페이스`**
  - 주소표시줄, 검색창, 새로고침, 뒤로가기/앞으로가기 버튼 등
  - **요청한 페이지를 보여주는 창을 제외한 나머지 부분**인 사용자가 접근할 수 있는 영역

- 2) **`브라우저 엔진`**
  - `사용자 인터페이스`와 `렌더링 엔진` 사이의 동작을 제어한다.

- 3) **`렌더링 엔진`**
  - 요청한 콘텐츠를 화면에 표시하는 브라우저의 핵심
  - HTML을 요청하면 HTML과 CSS를 해석(파싱)해서 화면에 표시하는 엔진

- 4) **`통신`**
  - ***HTTP 요청*** 같은 네트워크 호출에 사용
  - 플랫폼마다 독립적인 인터페이스이고 각 플랫폼 하단에서 실행

- 5) **`UI 백엔드`**
  - 콤보박스, 창과 같은 기본적인 위젯을 그린다
  - 플랫폼에서 명시하지 않은 일반적인 인터페이스로, OS 사용자 인터페이스 체계를 사용한다

- 6) **`자바스크립트 해석기`**
  - 자바스크립트 코드를 해석하고 실행한다

- 7) **`자료 저장소`**
  - 이름 그대로 자료를 저장하는 계층이다. 모든 종류의 자원을 하드디스크에 저장할 필요가 있다.
  - Local Storage, Indexed DB, 쿠키 등 브라우저 메모리를 활용하여 저장하는 영역이다.



### 3-4. 렌더링 엔진

렌더링 엔진의 역할<br/>
: 요청받은 내용을 브라우저 화면에 표시하는 것. HTML 및 XML 문서와 이미지를 표시할 수 있다<br/>
(플러그인이나 브라우저 확장 기능을 이용해 PDF와 같은 다른 유형도 표시할 수 있다.)<br/>


파이어폭스는 모질라에서 직접 만든 `게코(Gecko)` 엔진을 사용하고 사파리와 크롬은 `웹킷(Webkit)` 엔진을 사용한다.<br/>
웹킷은 최초 리눅스 플랫폼에서 동작하기 위해 제작된 오픈소스 엔진인데 애플이 맥과 윈도우즈에서 사파리 브라우저를 지원하기 위해 수정을 했다.<br/>


#### 3-4-1. 렌더링 엔진의 동작과정

렌더링 엔진은 통신으로부터 요청한 문서의 내용을 얻는 것으로 시작하는데,<br/>
문서의 내용은 보통 8KB 단위로 전송된다<br/>

<img src="/assets/images/browser_rendering_engine.png" /><br/>

we
- 1) DOM(Document Object Model) 트리 구축을 위한 HTML 파싱
  - 브라우저는 서버로부터 HTML 문서를 모두 전달받음
  - 전달받은 HTML 문서를 파싱, 콘텐츠 트리 내부에서 태그를 DOM 노드로 변환(DOM 트리 구축)
  - 외부 CSS 파일과 스타일 요소도 파싱
  - 스타일 정보와 HTML 표시 규칙은 렌더 트리를 구축한다
- 2) 렌더 트리 구축
  - DOM(Document Object Model) 트리와 스타일 정보를 합쳐서 렌더 트리를 만든다
- 3) 렌더 트리 배치
  - 렌더 트리의 각 노드에 대해서 화면 상에 어디에 배치할지 결정
- 4) 렌더 트리 그리기
  - UI 백엔드가 렌더 트리의 각 노드를 가로지르며 형상을 만들어내 렌더 트리를 그리고, 우리가 보는 화면에 출력된다

이러한 과정들은 점진적으로 진행된다. <br/>
렌더링 엔진은 좀 더 나은 나용자 경험을 위해 가능하면 빠르게 내용을 표시하는데, 모든 HTML을 파싱할 때까지 <strong style="color:black;background-color:yellow">기다리지 않고 배치와 그리기를 시작</strong>한다.<br/>

모든 내용을 한번에 파싱된 후 보여주기엔 속도가 느리기 때문에 기다리지 않고 파싱과 배치가 이뤄지는 것이다.<br/>
네트워크로부터 나머지 내용이 전송되기를 기다림과 동시에 받은 내용 일부를 화면에 먼저 표시한다.<br/>


- Webkit 엔진의 동작과정 예시

<img src="/assets/images/webkit-engine.png" /><br/>


#### 3-4-2. 파싱과 렌더 트리 구축

- 파싱
  - : 문서 파싱을 **브라우저가 코드를 `이해하고 사용`할 수 있는 구조로 `변환`하는 것**을 의미

  파싱 결과는 보통 문서 구조를 나타내는 `노드 트리` 파싱 트리(parse tree), 문법 트리(syntax tree) 라고 한다.<br/>

파서를 생성해 줄 수 있는 도구를 `파서 생성기`라고 한다. 위 사진에서 예로 든 웹킷은 두 개의 파서 생성기를 사용한다.<br/>

어휘 생성을 위한 `Flex`, 파서 생성을 위한 `Bison`이다.<br/>

- `Flex`
  - 토큰의 정규 표현식 정의를 포함하는 파일을 입력받음
- `Bison`
  - BNF 형식의 언어 구문 규칙을 입력받는다

이렇게 생성된 파서로 CSS와 자바스크립트를 파싱한다<br/>

HTML의 경우, 아래와 같은 이유로 일반적인 상향식/하향식 파서로는 파싱이 안되기 때문에 브라우저는 별도의 파서를 만들어야한다.<br/>

- 1) 언어의 너그러운 속성
- 2) HTML 오류에 대한 브라우저의 관용
- 3) 변경에 의한 재파싱

브라우저는 HTML을 받아서 **어휘와 구문을 분석**해서 파싱해 `파싱 트리`를 만든다.<br/>
`파싱 트리`를 기반으로 DOM 요소와 속성 노드를 가지는 `DOM 트리`를 생성한다. 그리고 DOM을 생성할 때 거쳤던 과정을 CSS에 반복해서 `CSSOM(CSS Object Model)`을 생성한다.<br/>
**DOM 트리가 구축되는 동안** 브라우저는 **DOM 트리를 기반으로 `렌더 트리를 생성`**한다. <br/>
렌더 트리는 아직 위치와 크기를 가지고 있지 않기 때문에 객체들에게 위치와 크기를 결정해주고,<br/>
렌더 트리의 각 노드를 화면에 그리면 화면에 콘텐츠가 표현된다.


#### 3-4-4. 렌더링 엔진과 자바스크립트 엔진 비교

렌더링 엔진의 역할<br/>
: 요청받은 내용을 브라우저 화면에 표시하는 것

자바스크립트 엔진의 역할<br/>
=> 자바스크립트 코드를 실행하는 것

- `렌더링 엔진`
  - 웹 렌더링 엔진(Web Rendering Engine), 웹 브라우저 엔진(Web Browser Engine), 웹 레이아웃 엔진(Web Layout Engine)
  - 웹 페이지에 대한 ***컨텐츠 및 데이터를 위해 동작***하는 엔진
  - 렌더링 역할을 하는 엔진이 ***브라우저마다 달라서*** 같은 페이지가 다르게 보인다
  - 엔진의 종류
    - Gecko - 모질라, 파이어폭스
    - Blink - 구글, 오페라
    - Webkit - 사파리
    - Trident - 익스플로러
    - EdgeHTML - 마이크로소프트 엣지

- `자바스크립트 엔진`
  - ***자바스크립트 코드를 실행***하는 인터프리터 또는 프로그램
  - 주로 웹 브라우저를 위해 사용된다
  - 대중적으로 알려진 자바스크립트 엔진은 구글의 V8 엔진
  - 자바스크립트 엔진이 반드시 V8 엔진이 아니고 엔진은 많이 존재한다. V8이 구글의 엔진이자 Node.js의 엔진일 뿐
  - 엔진의 종류
    - Rhino - 모질라
    - SpiderMonkey - 파이어폭스
    - V8 - 구글, 오페라
    - JavascriptCore - 사파리
    - Chakra - 익스플로러, 마이크로소프트 엣지

### 3-5. 인터프리터와 컴파일러

프로그램 언어를 해석하고 실행시키는 대표적인 방법으로는 `컴파일(Compile)`과 `인터 프릿(Interpret)` 방식이 있다. <br/>

#### 3-5-1. 실행 방식 비교

  - 컴파일
    - 프로그래밍 언어를 기계어로 해석하는 작업 방식
    - 실행은 인터프리터를 이용해 실행시키는 것 보다 빠르게 실행된다
    - 만약 원시 프로그램의 크기가 크다면 상당한 시간이 걸린다
  - 인터프릿
    - 한번에 한줄씩 읽어서 해석하며 프로그램을 구동시킴
    - 직접 코드를 구동시키는 특징이 있어 실제 실행시간은 느린 대신 실시간으로 디버깅이나 코드수정이 가능
    - 고급 프로그램을 즉시 실행시킬 수 있다


#### 3-5-2. 실행 과정 비교

| -- | -- |
| **`컴파일`** | **`인터프릿`** |
| 1. 어휘 분석 | 1. 명령어를 메모리에서 가져옴 |
| 2. 구문 분석 | 2. 가져온 명령어 해석 |
| 3. 중간 코드 생성 | 3. 필요한 데이터 가져옴 |
| 4. 최적화 | 4. 명령을 실행 |
| 5. 코드 생성 | -- |



## 4. 웹 접근성

### 4-1. 웹 접근성이란?

웹 접근성(Web Accessibility) 이란 장애인, 고령자 등이 웹 사이트에서 제공하는 정보에 비장애인과 동등하게 접근하고 이해할 수 있도록 보장하는 것이다. 법으로는 2017년 7월 26일부터 `장애인차별금지법`으로 시행되었다.<br/>

<img src="/assets/images/web_accessibility.png" /><br/>

웹 접근성은 정보와 사용자의 `디지털정보격차`를 줄인다는 개념으로도 볼 수 있다.

> #### 4-1-1. 디지털정보격차(Digital Divide)란?<br/>
정보통신기술에서의 접근, 역량, 활용에 있어서의 불평등<br/>
사회자원에서의 접근, 역량, 활용에 있어서의 불평등<br/>

### 4-2. 웹 접근성 접근성 지침(WCAG)

웹의 표준화 관련 국제 기구인 W3C(World Wide Web Consortium)에서는 웹 서비스에서 장애인의 접근성에 관련된 문제가 발생하자, 1997년에 WAI(Web Accessibility Initiative)라는 산하 단체를 설립하였다.

<br/>

<img src="/assets/images/accessibility_wcag.png" /><br/>

- WAI의 웹 콘텐츠 접근성 지침
  - 인지성(Perceivable)
  - 운용성(Operable)
  - 이해성(Understandable)
  - 견고성(Robust)



### 4-3. 대표 웹 접근성 기술

- 1) 시멘틱 마크업
  - W3C는 텍스트를 시각적으로 표현하는 태그보다 프로그램적으로 **`의미를 전달`**할 수 있는 시멘틱 마크업 사용을 권장한다.
  - 예시)
    - 의미가 없는 태그는 가상선택자(:after, :before)를 이용하며, 의미가 있는 태그는 span 태그 등에 대체 텍스트를 활용한다
    - b 태그는 강조보단 두껍게를 의미하는 태그이다. 강조의 의미인 <strong> 및 <em> 태그를 활용한다
    - 쇼핑몰 사이트의 <del>10,000원</del> 이런 형태의 가격표에는 del 태그를 사용하면 스크린리더기가 10,000원 뒤에 '삭제' 라고 읽는다
  -  **`의미론적인 태그를 사용`하여 마크업을 작성**할 것


- 2) 텍스트를 포함한 이미지
  - image 태그에는 꼭 스크린리더기가 읽을 수 있는 alt 속성을 추가해 이미지를 설명한다

- 3) 텍스트 명도대비
  - W3C는 기본적으로 텍스트와 배경과의 명도대비는 최소한 4.5 : 1 을 제공하도록 권장

- 4) 비텍스트 명도대비
  - W3C는 UI요소 및 그래픽 콘텐츠에 한에서 명도대비를 3:1을 제공하도록 권장

- 5) WAI-ARIA
 - 정적인 HTML과 단순한 JavaScript 환경이 아닌 동적인 JavaScript 및 Ajax와 같은 기술을 사용한 환경에서 스크린리더 및 보조기기등이 접근성 및 상호 운용성을 향상시키기 위하여 탄생

- 6) 반응형 웹
  - 콘텐츠는 정보 또는 기능 손실 없이, 2차원 스크롤 없이 제공해야 한다
  - **2차원 스크롤** 예시
    - 가로 320px 넓이에서 가로 스크롤이 없이 수직으로 스크롤
    - 세로 256px 높이에서 세로 스크롤이 없이 수평으로 스크롤

- 7) 동영상 실시간 자막
 - 동영상 제공 시 W3C는 특별한 경우를 제외하고 동기화된 자막을 제공하도록 권장

- 8) 자동완성기능
  - 사용자들로부터 어떤 값들이 입력되길 기대하는지, 혹은 입력된 정보의 의미가 무엇인지를 나타내는 코드가 필요



https://accessibility.naver.com/accessibility  등에서 기준을 찾을 수 있다.



> 참조
<br/>
https://velog.io/@surim014/AJAX%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
<br/>
https://webplatform.github.io/docs/apis/xhr/XMLHttpRequest/
<br/>
https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F#thankYou
<br/>
https://evan-moon.github.io/2020/05/21/about-cors/
<br/>
https://mygumi.tistory.com/173
<br/>
https://d2.naver.com/helloworld/59361
<br/>
https://seulbinim.github.io/WSA/accessibility.html#%EC%9B%B9%EC%A0%91%EA%B7%BC%EC%84%B1%EC%9D%98-%EA%B0%9C%EC%9A%94
<br/>
https://velog.io/@recordboy/%EC%9B%B9-%EC%A0%91%EA%B7%BC%EC%84%B1-%EC%A0%95%EC%9D%98-%EB%B0%8F-%EB%8C%80%EB%B9%84-%EB%B0%A9%EB%B2%95IATC