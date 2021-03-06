---
published: true
title: "Git, JS동작원리, DOM, ECMAScript"
permalink: /cs/defaultKnowledge1
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-04-12
last_modified_at: 2022-04-12
---

![]()

> 들어가기 전 <br/>

https://joshua1988.github.io/web-development/interview/frontend-questions/
<br/>
https://github.com/JaeYeopHan/Interview_Question_for_Beginner
<br/>
https://jbee.io/essay/for_junior_frontend_developer/
<br/>

위의 글들을 참조하여 배경지식을 찬찬히 쌓아보자.<br/>

## 1. Git / GitHub

"깃과 깃허브의 차이를 아시나요?"<br/>
모른다. 회사에서 집에서 밥먹듯이 쓰면서도 모른다.<br/>
버전관리를 해주기 때문에 git 없이는 일할 수 없다는 것 뿐. <br/>

> `버전관리`란? <br/>
작업에 실수가 있어 이전 버전으로 돌아가고 싶을 때, 협업을 하다 서로 작업이 꼬였을 때.<br/>
이러한 일을 관리해주는 프로그램을 **버전관리 프로그램**이라고 한다.<br/>
작업 내역을 버전관리 툴에 올리고 기록한다. <br/>
이렇게 작업을 하다가 만약 코드가 꼬이거나 개발 방향을 바꿔야할 경우 특정 버전을 지정하여 되돌아 갈 수 있다.



### 1-1. Git

📌 **Git** <br/>

**오픈 소스 버전 관리 시스템(VCS: Version Control System)**<br/>
로컬에서 변경된 사항을 추적하고 원격 리소스와 대조해서 변경사항을 푸시하거나 가져올 수 있다.


- **`로컬`**에서 버전 관리
- 소프트웨어 개발 및 소스 코드 관리에 사용

본인의 코드와 그 수정내역을 기록하고 관리하도록 돕는 버전 관리 프로그램이며, 로컬에서 프로젝트의 기록을 스스로 관리할 수 있도록 해준다.<br/>
**브랜치를 생성**하고 이전 브랜치로 **복구, 삭제, 병합이 가능**하다.<br/>
하지만 로컬 저장소를 사용하기 때문에 다른 개발자와 **실시간으로 작업을 공유할 수 `없다`**.



### 1-2. Github

📌 **Github** <br/>

- Git Repository를 위한 ***웹 기반 호스팅 서비스***
- **`클라우드 서버`**를 사용해서 로컬에서 버전 관리한 소스코드를 업로드하여 공유 가능
- 분산 버전 제어, 액세스 제어, 소스 코드 관리,  버그 추적, 기능 요청 및 작업 관리를 제공

git 저장소를 관리하는 **클라우드 기반 호스팅 서비스**. <br/>
git 저장소 호스팅 서비스는 클라우드 기반으로 다른 사람과 소스코드 공유가 가능하며 git의 기본적인 기능을 확장하여 제공한다.<br/>
또한 클라우드 서버에 소스를 올리기 때문에 한 프로젝트에 여러 명의 사람이 참여하여 버전 제어 및 **공동 작업이 가능**.



### 1-3. GitLab

📌 **GitLab** <br/>

간단히 요약하자면 비공개된 Github. <br/>

개인 또는 조직이 Git repository 내부관리에 사용하는 Github라고 볼 수 있다. <br/>

중앙 서버에서 Git 저장소를 관리하기 위해서 사용하고,<br/>
repository 완벽하게 제어 할 수 있으며, 공개 또는 비공개 여부를 결정할 수 있다.<br/>






## 2. Javascript 동작원리


매일 자바스크립트를 쓰면서도, 자바스크립트의 동작 원리를 어렴풋하게만 알고 있었을 뿐 제대로 정리해본 적이 없다. <br/>
그래서 작업을 하는 도중 일처리 순서에 의문을 가질 때가 매우 많았다. <br/>

가장 의문을 가졌던 부분부터 차근차근 정리해보겠다.<br/>

"자바스크립트는 **싱글쓰레드** 기반이고, **콜백 큐**를 사용한다" <br/>

이제 알쏭달쏭한 이 말을 천천히 이해해보자.

### 2-1.자바스크립트의 엔진

google에서 만든 V8엔진은 자바스크립트를 실행할 수 있게 해준다.<br/>
아래는 V8 엔진을 간략히 그린 그림이다.

<img src="/assets/images/js_engine.png" /><br/>
이미지 출처 https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf
<br/>

엔진에는 두가지 구성요소가 있다.

- **`Memory Heap`** : 메모리 할당이 일어나는 곳
- **`Call Stack`** : 코드 실행에 따라 호출 스택이 쌓이는 곳

### 2-2. 자바스크립트가 싱글 쓰레드인 이유

바로 V8 엔진에 콜 스택이 하나밖에 없기 때문이다. <br/>
코드를 읽으며 **호출된 함수를 콜 스택에 추가**하고, **실행이 완료**된 함수는 콜 스택에서 **제거**한다. <br/>
이 콜 스택이 단 한개이기 때문에 두개 이상의 코드를 동시에 읽지 못한다. <br/>



자바스크립트를 사용하다보면, setTimeOut() 같은 수많은 API를 사용한다.<br/>
이런 API들은 자바스크립트 엔진에서 제공해주는 요소가 아닌 `Web API`이다. <br/>
`Web API`란 웹 브라우저 혹은 node js 같은 자바스크립트 런타임에서 지원해주는 API를 말한다. <br/>
(그래서 어떤 브라우저에서는 지원을 해줄 수도 있고, 안 해 줄 수도 있다)<br/>
Web API와 더불어 **웹 브라우저나 런타임**에서는 `Event loop`와 `Callback Queue`라는 것을 지원한다. <br/>



<img src="/assets/images/js_engine_work.png" /><br/>
이미지 출처 https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf



- V8 엔진의 **`Memory heap`**, **`Call Stack`**
- Web API에서 제공하는 API들 **`DOM`**, **`AJAX`**, **`TimeOut`**
- 브라우저나 런타임이 제공하는 **`Event Loop`**, **`Callback Queue`**



### 2-3. 스택 프레임(Stack Frame)과 후입 선출(LIFO, Last-In-First-Out)

자바스크립트의 **Call Stack(호출 스택)**은,<br/>
한 줄씩 읽어가며 코드가 순서대로 돌아갈 수 있도록 보장해주는 데이터 구조 <br/>

Stack을 사용하기 때문에, 나중에 들어온 것이 먼저 나가는 **`후입 선출`**의 구조를 가진다.<br/>

이렇게 call stack에 쌓이는 하나의 사각형을 **`스택 프레임(stack frame)`**이라고 한다.<br/>

호출 스택은 기본적으로 프로그램 상에서 **`어디 있는지`** 기록하는 자료구조이다.<br/>

- 함수가 실행이 된다면(실행 커서가 함수 안에 있으면)<br/>
  - 해당 함수 스택 프레임은 호출 스택의 가장 상단에 위치한다<br/>
  - 따라서 스택의 맨 위에 있는 스택 프레임을 가리키고 있게 됨.<br/>
- 함수의 실행이 끝날 때(리턴 값을 돌려줄 떄)<br/>
  - 해당 함수 스택 프레임을 호출 스택에서 제거<br/>

=> 이게 ***스택의 역할***!


* 예제 (사각형의 넓이 구하기)

```js
function multiply(x, y) {
    return x * y;
}
function printSquare(x) {
    var s = multiply(x, x);
    console.log(s);
}
printSquare(5);
```

처음 엔진이 이 코드를 실행하는 시점에서는 호출스택이 비어있다. <br/>

하지만 코드가 실행되면 아래와 같이 변한다<br/>
<img src="/assets/images/js_stack_frame.png" /><br/>

코드가 실행되면 가장 먼저 printSqure가 호출됨<br/>
- 1. printSqure를 Push해서 스택에 쌓고 읽음
- 2. multiply를 Push해서 스택에 쌓고 읽음
- 3. console.log(s)를 스택에 쌓고 읽음
- 4. 더이상 읽어서 쌓을 함수가 존재하지 않으면, 맨 위에 있는 스택프레임부터 처리하며 출력

중요! ⭐️ <br/>
더이상 쌓을 함수가 존재하지 않으면, **맨 위에 있는** 스택 프레임부터 하나씩 처리하며 출력한다. <br/>





### 2-4. 중요! ⭐️  싱글쓰레드가 비동기 처리를 어떻게 하는거지?


그런데 이상한 점이 있다.<br/>
비동기처리는 보통 멀티스레드가 동작해서 멀티테스킹 작업을 해야할텐데, 싱글스레드인 JS는 어떻게 비동기처리를 하는 걸까?<br/>


> **`동기`**(Syncronous)<br/>
: 요청을 보내고 해당 요청에 대한 응답을 받기 전 까지 다음 동작을 실행하지 않는다.<br/>
> **`비동기`**(Ansyncoronous) <br/>
: 요청을 보내고 해당 요청에 대한 **응답 여부에 상관없이** 다음 동작을 실행한다.


=> `Web API` & `Event loop` & `Callback Queue`와의 협업 덕분에! <br/>


자바스크립트는 웹 브라우저나 node js의 자바스크립트 엔진에서 실행된다.<br/>
이 엔진에는 자바스크립트를 돌리는 하나의 쓰레드가 있다. <br/>
이 엔진과 **비동기식 처리 모델인 `Web API`**가 함께 동작하면서 <br/>

- 자바스크립트 엔진의 `call Stack`에서는 코드 실행에 따라 쌓인 **`호출 스택`**을 처리
- `Web API`에서는 setTimeout이나, AJAX로 http 데이터를 가져오는 작업 등의 **`시간이 소요되는 일`**을 처리


<img src="/assets/images/js_async_work_1.jpeg" /><br/>
<img src="/assets/images/js_async_work_2.jpeg" /><br/>





> 첨언
자스의 엔진의 싱글쓰레드로써의 노력 + Web API의 오래걸리는 일 처리능력 + 이벤트 루프의 콜스택이 비었는지 검사하고 비었으면 큐에서 스택으로 올려보내는 노력

setTimeout이나 AJAX나 DOM 변경하는건 오래걸리자나여 그래서 자스 자체로는 처리능력이 없고

그걸 쓰는 것 자체가 Web API가 주는 걸 가져다 ㄱ쓰는거라서

씀과 동시에 자기꺼니까 저기 멀리 가서 처리한 뒤에 콜백큐에 넣어버리는거져


- 콜백 함수는 말 그대로 나중에 실행되는 함수를 말하고
- 콜백 큐는 비동기 처리를 위해 동작하고 있는 함수들이
- 대기시간이 종료되면 (예: setTimeout의 3초지남 ) 콜백 큐로 차근차근 들어오고
- 이벤트 루프는 그 콜백 큐와 호출스택을 보고있다가
- 호출스택이 비었을 경우에만 콜백 큐에서 하나씩 빼서 올립니다
- 그래서 콜백큐는 선입선출
결론 => Web API가 콜백함수를 콜백큐로 밀어넣는다



setTImeout DOM AJAX를 사용하는 것
= Web API를 사용하는 것
= 콜백함수이고 대기시간이 종료되면 콜백큐로 넘어가서 콜스택이 비어있으면 올라감

- 비동기 함수가 실행된다면, Web API가 호출된다.

- Web API는 비동기함수의 콜백함수를 Callback Queue에 밀어넣는다.
## 3. DOM API



<!-- 
DOM API (Web API) and Concept
-https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction

-DOM은 문서의 구조화된 표현(structured representation)을 제공하며 프로그래밍 언어가 DOM 구조에 
접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다.

-javascript 를 통해 웹 콘텐츠를 동적으로 제어할 수 있는 이유는 DOM 이 
중간에서 interface 역할을 해주기 때문입니다. -->


### 3-1. DOM(The Document Object Model)이란?

문서 객체 모델(The Document Object Model, 이하 DOM) 은 **HTML, XML 문서의 `프로그래밍 interface`** 이다.<br/>
DOM은 문서의 **구조화된 표현**(structured representation)을 제공하며 <br/>
프로그래밍 언어가 
<strong style="color:black;background-color:yellow"> DOM 구조에 접근할 수 있는 방법을 제공</strong>하여
<br/>

그들이 **문서 구조, 스타일, 내용 등을 `변경할 수 있게`** 돕는다.

<br/>

DOM 은 구조화된 **`nodes`**와 **`property`** 와 **`method`** 를 갖고 있는 **`objects`**로 문서를 표현한다.<br/>
이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게
<strong style="color:black;background-color:yellow"> 연결시켜주는 역할</strong>을 담당한다.<br/>

웹을 아주 기본적으로 나누자면<br/>
**HTML(구조)**, **CSS(스타일링)**, **JS(기능)** 으로 나눌 수 있다.<br/>

이 중 HTML을 바꾸는 것이 JS의 역할이라고 할 수 있는데, <br/>
이 역할을 DOM과 연관지을 수 있다.<br/>

javascript 를 통해 웹 콘텐츠를 동적으로 제어할 수 있는 이유는<br/>
DOM 이 중간에서 interface 역할을 해주기 때문.

### 3-2. DOM 구조, DOM 트리

DOM은 트리 구조로 HTML 문서를 표현한다

<img src="/assets/images/js_dom.png" /><br/>

기본적으로 HTML 구조를 따라가고, 이를 tree 형태로 표현한다.<br/>

최상위 태그인 html이 DOM Tree의 가장 상위 요소인 것 처럼 보이지만,<br/>
html태그와 더불어 최상단의 선언문인 !doctype html까지 포함하는

**`document 객체`**가 그 위에 있다.<br/>
모든 html의 위에는 document가 있는 것이다.<br/>

div, input 과 같은 태그들로 쌓여있는 마크업 한 구조들이 나무처럼 보여서 돔트리라고 한다.

### 3-3. 그럼 DOM API가 뭐야?

**`DOM API`**(Document Object Model Application Programming Interface)<br/>

> 다시한번 요약 정리

- DOM(Document Object Model)
  - HTML에서 제어하는 div, span, input 등의 요소들
- API(Application Programming Interface)
  - 프로그램을 사용하기 위한 명령들의 집합

=> 결론!<br/>
DOM API는, HTML의 요소들을 JS에서 제어하기 위한 **`명령들의 집합`**을 뜻한다.

## 4. ECMAScript2015(ES6)


JavaScript 언어의 **표준**이며 ES6라고도 칭한다. <br/>

ECMA라는 국제 기구에서 만든 표준문서인 ECMAScript(=ES)의 6번째 개정판 문서에 있는 표준 스펙을 말한다.<br/>

<!-- -2015년 자바스크립트가 새롭게 개편되어 const let 화살표 함수와 같은 ES5까지 그동안 문제가 
많았던 문법들을 해결하는 새로운 문법들이 등장하게된 문법
문제 예: this가 특정 객체 안의 메소드 함수 안에서 함수를 호출하면 자신을 감싸고 있는
 객체가 아닌 전역객체의 메소드가 되어 window나 global을 this로 불러오는 오류를 화살표
 함수로 바꾸면 따로 바인딩 하지 않아도 해결됨 -->



TypeScript의 기반이 되는, 클래스 문법과 모듈 기능 추가, IE9 부터 지원 <br/>

다음과 같은 문제점들이 사라짐 <br/>

- 호이스팅이 사라진 것 같은 효과
- 함수 단위 스코프에서 블록 단위 스코프로 변경
- this를 동적으로 바인딩하지 않는 화살표 함수
- 모듈화 지원
- 콜백 지옥에서 구원해줄 Promise
- Default, Rest 파라미터
- 해체 할당, Spread 연산자
- 템플릿 리터럴

브라우저(특히 MS 계열)에서 지원해주지 않는 경우가 많아, **`바벨(Babel)`**이라는 트랜스파일러를 써야한다. <br/>

































> 참조

https://needjarvis.tistory.com/656
<br/>
https://cocoon1787.tistory.com/723
<br/>
https://velog.io/@leyuri/Github-%EA%B3%BC-Gitlab-%EC%9D%98-%EC%B0%A8%EC%9D%B4
<br/>
https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf
<br/>
https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/
<br/>
https://tristy.tistory.com/51
<br/>
https://velog.io/@code-bebop/JS-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-%EC%BD%9C%EB%B0%B1-%ED%81%90
<br/>
https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction
<br/>
https://from2020.tistory.com/23

<br/>

https://velog.io/@gil0127/JS-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%95%B5%EC%8B%AC-Event-Loop