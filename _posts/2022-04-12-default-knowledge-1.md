---
published: true
title: "👩🏻‍💻 배경지식 쌓기 Step (1) - Git, JS동작원리, DOM, ECMAScript"
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

# 1. Git / GitHub

"깃과 깃허브의 차이를 아시나요?"<br/>
모른다. 회사에서 집에서 밥먹듯이 쓰면서도 모른다.<br/>
버전관리를 해주기 때문에 git 없이는 일할 수 없다는 것 뿐. <br/>

> `버전관리`란? <br/>
작업에 실수가 있어 이전 버전으로 돌아가고 싶을 때, 협업을 하다 서로 작업이 꼬였을 때.<br/>
이러한 일을 관리해주는 프로그램을 **버전관리 프로그램**이라고 한다.<br/>
작업 내역을 버전관리 툴에 올리고 기록한다. <br/>
이렇게 작업을 하다가 만약 코드가 꼬이거나 개발 방향을 바꿔야할 경우 특정 버전을 지정하여 되돌아 갈 수 있다.



## 1-1. Git

📌 **Git** <br/>

**오픈 소스 버전 관리 시스템(VCS: Version Control System)**<br/>
로컬에서 변경된 사항을 추적하고 원격 리소스와 대조해서 변경사항을 푸시하거나 가져올 수 있다.


- **`로컬`**에서 버전 관리
- 소프트웨어 개발 및 소스 코드 관리에 사용

본인의 코드와 그 수정내역을 기록하고 관리하도록 돕는 버전 관리 프로그램이며, 로컬에서 프로젝트의 기록을 스스로 관리할 수 있도록 해준다.<br/>
**브랜치를 생성**하고 이전 브랜치로 **복구, 삭제, 병합이 가능**하다.<br/>
하지만 로컬 저장소를 사용하기 때문에 다른 개발자와 **실시간으로 작업을 공유할 수 `없다`**.



## 1-2. Github

📌 **Github** <br/>

- Git Repository를 위한 ***웹 기반 호스팅 서비스***
- **`클라우드 서버`**를 사용해서 로컬에서 버전 관리한 소스코드를 업로드하여 공유 가능
- 분산 버전 제어, 액세스 제어, 소스 코드 관리,  버그 추적, 기능 요청 및 작업 관리를 제공

git 저장소를 관리하는 **클라우드 기반 호스팅 서비스**. <br/>
git 저장소 호스팅 서비스는 클라우드 기반으로 다른 사람과 소스코드 공유가 가능하며 git의 기본적인 기능을 확장하여 제공한다.<br/>
또한 클라우드 서버에 소스를 올리기 때문에 한 프로젝트에 여러 명의 사람이 참여하여 버전 제어 및 **공동 작업이 가능**.



## 1-3. GitLab

📌 **GitLab** <br/>

간단히 요약하자면 비공개된 Github. <br/>

개인 또는 조직이 Git repository 내부관리에 사용하는 Github라고 볼 수 있다. <br/>

중앙 서버에서 Git 저장소를 관리하기 위해서 사용하고,<br/>
repository 완벽하게 제어 할 수 있으며, 공개 또는 비공개 여부를 결정할 수 있다.<br/>






# 2. Javascript 동작원리


매일 자바스크립트를 쓰면서도, 자바스크립트의 동작 원리를 어렴풋하게만 알고 있었을 뿐 제대로 정리해본 적이 없다. <br/>
그래서 작업을 하는 도중 일처리 순서에 의문을 가질 때가 매우 많았다. <br/>

가장 의문을 가졌던 부분부터 차근차근 정리해보겠다.<br/>

"자바스크립트는 **싱글쓰레드** 기반이고, **콜백 큐**를 사용한다" <br/>

이제 알쏭달쏭한 이 말을 천천히 이해해보자.

## 2-1.자바스크립트의 엔진

google에서 만든 V8엔진은 자바스크립트를 실행할 수 있게 해준다.<br/>
아래는 V8 엔진을 간략히 그린 그림이다.

<img src="/assets/images/js_engine.png" /><br/>
이미지 출처 https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf
<br/>

엔진에는 두가지 구성요소가 있다.

- **`Memory Heap`** : 메모리 할당이 일어나는 곳
- **`Call Stack`** : 코드 실행에 따라 호출 스택이 쌓이는 곳

## 2-2. 자바스크립트가 싱글 쓰레드인 이유

바로 V8 엔진에 콜 스택이 하나밖에 없기 때문이다. <br/>
코드를 읽으며 **호출된 함수를 콜 스택에 추가**하고, **실행이 완료**된 함수는 콜 스택에서 **제거**한다. <br/>
이 콜 스택이 단 한개이기 때문에 두개 이상의 코드를 동시에 읽지 못한다. <br/>



자바스크립트를 사용하다보면, setTimeOut() 같은 수많은 API를 사용한다.<br/>
이런 API들은 자바스크립트 엔진에서 제공해주는 요소가 아닌 `Web API`이다. <br/>
`Web API`란 웹 브라우저 혹은 node js 같은 자바스크립트 런타임에서 지원해주는 API를 말한다. <br/>
(그래서 어떤 브라우저에서는 지원을 해줄 수도 있고, 안 해 줄 수도 있다)<br/>
Web API와 더불어 **웹 브라우저나 런타임**에서는 `Event loop`와 `Callback Queue`라는 것을 지원한다. <br/>



<img src="/assets/images/js_engine_work.png" /><br/>




## 2-3. 스택 프레임(Stack Frame)과 후입 선출(LIFO, Last-In-First-Out)


자바스크립트 엔진 이외에도 자바스크립트에 관여하는 다른 요소들이 많습니다. DOM, Ajax, setTimeout 과같이 브라우저에서 제공하는 API 들을 Web API라고 합니다. 그리고 아래쪽에 이벤트 루프와 콜백 큐도 있네요.

- V8 엔진의 **`Memory heap`**, **`Call Stack`**
- Web API에서 제공하는 API들 **`DOM`**, **`AJAX`**, **`TimeOut`**
- 







## 2-4. 중요! ⭐️  싱글쓰레드가 비동기 처리를 어떻게 하는거지?


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








# 3. DOM API
# 4. ECMAScript2015(ES6)







































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