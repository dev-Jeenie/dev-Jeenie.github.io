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

AJAX란 비동기식 자바스크립트와 XML을 뜻한다.

- 자바스크립트를 이용해 서버와 브라우저가 **비동기 방식으로 데이터를 교환**할 수 있는 통신 기능
- 브라우저가 가지고 있는 `XMLHttpRequest` 객체를 이용해 전체 페이지를 새로 고침하지 않고 일부 데이터만 로드하는 방법

자바스크립트로 서버에 데이터를 <strong style="color:black;background-color:yellow">**비동기 방식으로 요청**</strong>하는 것!

> 여기서 XMLHttpRequest 란? <br/>

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

동기방식과 비동기방식
  <img src="/assets/images/default_3_async_2.jpeg" /><br/>
예제 )
  <img src="/assets/images/default_3_async_1.jpeg" /><br/>














## 2. CORS(Cross Origin Resource Sharing)


  <img src="/assets/images/cors.jpeg" /><br/>
  <img src="/assets/images/cors_1.png" /><br/>





> 참조
<br/>
https://velog.io/@surim014/AJAX%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80