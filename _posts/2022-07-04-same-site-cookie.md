---
published: true
title: "Cookie/Session, JWT, 그리고 SameSite"
permalink: /life/sameSiteCookie
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-07-04
last_modified_at: 2022-07-04
---
****
![]()

# Cookie와 Session

## 1. 등장배경

클라이언트가 정보를 유지하는 stateful한 성격의 서비스가 많아짐<br/>
> (로그인을 통해 볼 수 있는 서비스, 장바구니 등)<br/>

그런데 <a href="https://dev-jeenie.github.io/CS/whatIsHttp">HTTP의 특징 (링크)</a> 중 **`무상태(stateless)`**, **`비연결성(connectionless)`** 탓에 정보를 유지할 수 없다. <br/>

서버와 클라이언트가 통신을 할 때 마다 서버는 클라이언트가 누구인지 인증을 계속해야 한다. <br/>

🤷🏻‍♀️ : 아니 너무 번거롭잖아! 기억하게 하려면 어떻게 하지? <br/>

=> 그래서 나온 것이 바로 **`Cookie`**와 **`session`**! <br/>

클라이언트의 인증을 유지하기 위해 사용된다. <br/>

# 만약 쿠키와 세션을 사용하지 않는다면

- 쇼핑몰에 접속
- 너 누구야? 로그인 해
- 상품 클릭 -> 상세화면으로 이동
- 너 누구야? 로그인 해
- 주문
- 너 누구야? 로그인 해
- 유저 극대노 🔥🔥

=> 열받은 사용자는 사이트를 꺼버리고 말 것이다. </br>

# 쿠키와 세션을 사용했을 경우

**`최초 로그인`**을 하면, 서버가 그 사용자에 대한 **`인증을 유지`**한다. <br/>

즉, <strong style="color:black;background-color:yellow">쿠키와 세션을 통해 서버는 클라이언트를 기억하고 있는 것! </strong>


## 2. Cookie란?

클라이언트 측(브라우저)에서 관리되는 **`작은 기록 정보 파일`** <br/>

**쿠키의 특징**

- 사용자 인증이 **`유효한 시간을 명시`**할 수 있다
- 한 번 유효 시간이 정해지면 **`브라우저를 끄더라도 인증이 유지`**된다

### 2-1. 쿠키 구성 요소




### 2-2. 쿠키 동작 방식




### 2-3. 쿠키 사용 예




