---
published: true
title: "REST API, TDD, MVC 패턴"
permalink: /cs/defaultKnowledge5
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-05-06
last_modified_at: 2022-05-06
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

<hr/>

## 1. REST(REpresentational State Transfer)


### 1-1. REST란?

<!-- Client와 Server 사이의 통신 방식 중 하나 -->
소프트웨어 프로그램 아키텍처의 한 형식 <br/>

REpresentational State Transfer의 약자로<br/>
자원을 이름으로 구분해 해당 자원의 상태를 주고받는 모든 것을 의미<br/>

즉, **자원의 표현에 의한 상태 전달**을 뜻함

- 자원 : 해당 소프트웨어가 관리하는 모든 것 ( 문서, 그림, 데이터, 해당 소프트웨어 자체 등 )
- 표현 : 그 자원을 표현하기 위한 이름 ( DB의 학생 정보가 자원이면, 'students'를 자원의 표현으로 정함 )
- 상태 전달 : 데이터가 요청되는 시점에 자원의 상태를 전달한다. ( JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적 )

웹의 기존 기술과 **HTTP 프로토콜을 그대로 활용**하기 때문에,<br/>
**웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일**이다<br/>



HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,<br/>
HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
CRUD Operation
Create : 생성(POST)
Read : 조회(GET)
Update : 수정(PUT)
Delete : 삭제(DELETE)
HEAD: header 정보 조회(HEAD)



### 1-2. REST API와 RESTful API



REST API는 URI로 접근가능하고 내용이 JSON,XML 등으로 표현된 자원에 대한 행위를 **`HTTP Method로 정의`**한다.

RESTful하다라는 것은 REST API의 **설계의도를 명확하게 지켜주는 것**이다.
(슬래시를 통해 계층관계를 표시한다던가 숫자는 id를 나타낸다든가 동사보단 명사를 위주로 쓴다든가 하는.)







## 2. TDD


### 2-1. TDD란?


### 2-2. 장단점



## 3. MVC 패턴

<img src="/assets/images/mvc.png" /><br/>

디자인 패턴 중 하나.

> 디자인 패턴이란? <br/>




> 참조

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
