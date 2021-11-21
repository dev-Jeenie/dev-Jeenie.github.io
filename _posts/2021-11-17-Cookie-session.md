---
title: "cookie, session, token 🍪 "
permalink: /cs/CookieSession
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-18
last_modified_at: 2021-11-18
---

![]()
"세션 ID를 전달하는 매개체"

## cookie 

서버는 쿠키를 이용 브라우저에 `내 정보를 기억`하기 위한 데이터를 넣을 수 있다.

<img src="/assets/images/Cookie_what_is_cookie.jpeg" /><br/>

1. 사이트에 방문하면 브라우저는 서버에 request를 보냄
2. 서버는 모든 데이터와 내가 찾던 페이지 정보를 가지고 response함<br/>
(이 response 안에 브라우저가 저장하고자 하는 쿠키가 있다)

쿠키는?

- 쿠키는 `도메인에 따라 제한`된다
  - 유튜브가 준 쿠키는 유튜브에만 전달됨
- 쿠키는 `유효기간`이 있다
  - 서버기 정한 기간마다 다름
- 쿠키는 인증 뿐만 아니라 `여러가지 정보를 저장`할 수 있다
  - 웹사이트 언어설정 변경으로 예시<br/><br/>
<img src="/assets/images/Cookie_cookie.jpeg" /><br/>

<br/>

## session / JWT
### 1. session

> HTTP 프로토콜은 `stateless`!

- 서버로 가는 모든 요청이, 이전 request와는 독립적으로 다뤄진다
- 요청끼리 연결이 없음. 메모리가 없음.

요청이 끝나면 서버는 잊어버리기 때문에, 요청시마다 우리가 누군지 알려줘야한다

알려주는 방법 중 하나가 바로 session!

> login 예제

<img src="/assets/images/Cookie_login.jpeg" /><br/>


- Nico라는 유저가 로그인을 하고싶다면,

1. 유저명과 비밀번호를 서버에 보낸다
2. 비번이 맞다면 서버는 세션DB에 Nico라는 유저를 생성함(해당 세션에는 별도의 ID 존재)
3. 해당 세션ID는 쿠키를 통해 서버를 거쳐 브라우저로 돌아오고 저장된다

따라서, 같은 웹사이트의 다른 페이지로 이동하면?

1. 브라우저가 `세션ID`를 가지고있는 쿠키를 서버에 보낸다
2. 서버는 `세션ID`와 함께 오는 쿠키를 확인한다
  - 서버는 아직까지도 내가 누구인지 모름
  - `세션ID`가 있는 쿠키를 가진 요청이 있다는 것만 알고있다!
3. 서버는 해당 `세션ID`를 가지고 **세션 DB**를 확인하고
4. **세션DB**는 이 `세션ID`가 유저명 Nico의 것이라는 걸 알려줌
5. 서버는 이제야 누구인지 알고, 환영Nico 메시지를 띄운다


> => 해당 요청이 끝나고 다른 페이지로 이동하면?

<img src="/assets/images/Cookie_login_2.jpeg" /><br/>


**유저는 오직 `세션ID`만** 가지고 있다!<br/>
**서버가 유저에 대한 모든 정보**를 가지고 있음

쿠키는 이 `세션ID`를 전달하기 위한 `매개체`일 뿐!

> `token`이란?<br/>
  : `쿠키 대신 사용하는 매개체`! <br/>
    세션을 이용해 android, ios 앱을 만들 수 있지만 **쿠키는 native 앱에 없기 때문에** 사용할 수 없다. 쿠키는 오직 브라우저에만 있음<br/>
  => 세션ID를 전달해주는 매개체로 쿠키 대신 <strong>**토큰**<strong>을 사용!<br/>
  토큰은 그냥 이상하게 생긴 `string`이다.<br/>



**기억해야할 부분!**
- 현재 로그인한 유저들의 모든 세션 ID를 DB에 저장해아한다.
  - request가 들어올 때마다
  1. 서버는 쿠키를 받아서 세션ID를 보고,
  2. 세션ID와 일치하는 유저를 찾아야하고,
  3. 그제서야 다음 작업을 수행할 수 있다.
  
> => 요청이 있을 때마다 DB를 뒤져야한다.<br/>
유저가 `늘어남에 따라 DB 리소스가 더 필요한 것`!<br/>
이때 사용하는 것이 **JWT**

### 2.JWT



JWT는 쿠키가 아닌 토큰형식이다 <br/>
JWT로 유저 인증을 처리하면, 세션 DB를 가질 필요가 없음.
서버는 유저 인증을 위해서 많은 일을 하지 않아도 된다

토큰은 서버로부터 받아서, request할 때마다 보내야하는 것. 서버는 받은 요청안에 있는 토큰으로 세션DB에서 일치하는 것을 찾아야함.(일이 너무 많아서 DB 리소스가 더 필요한 것)

이러한 세션 방식 대신 JWT


> 로그인 예제
<img src="/assets/images/Cookie_JWT.jpeg" /><br/>


1. 유저가 로그인을 하려고 ID password를 서버에 전송
2. ID password가 맞다면,  세션 방식처럼 세션DB에 해당 유저정보를 `생성하지 않는다`.
대신 유저의 ID 등을 가져다가 signature algolythm을 이용해 사인함.
3. 해당 사인된 정보를 string 형태로 보내줌.

쿠키보다 훨씬 길다. 쿠키는 공간 제약이 있지만, JWT는 제약이 없기 때문에!


## session과 JWT의 `차이점` 정리! ✨

### session
<img src="/assets/images/Cookie_session_vs_JWT.jpeg" /><br/>

session 방식은,<br/>
`session ID`를 가진 request가 오면 **`세션 DB`**에서 `세션 ID`를 찾는 것!


### JWT
<img src="/assets/images/Cookie_session_vs_JWT_2.jpeg" /><br/>

JWT 방식은,<br/>
`token`를 가진 request가 오면 그 `token`의 **`유효성 검사`**를 하는 것!
