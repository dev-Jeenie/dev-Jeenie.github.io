---
title: "서드파티 쿠키지원을 중단한다고? 그게뭔데! Third Party 💥"
permalink: /cs/ThirdParty
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-24
last_modified_at: 2021-11-24
---

![]()

"자사 쿠키🍪, 타사 쿠키🍪, 💵!"


## 그전에, 쿠키란?
브라우저에서 정보를 저장해야하는 경우가 있다.
로그인 됐다는 **`응답결과`를 브라우저에서 쿠키라는 형식으로 저장**하고 있는 것. <br/>
(장바구니 또한 쿠키로 장바구니 정보를 저장한 것) <br/>

웹서비스를 이용하며 서버에게 응답을 받게되는 경우가 많은데, <br/>
그 중 `특정 값들을`,  `각 사이트마다` 쿠키로 가지고 있는 것임!


이때의 쿠키는, **쿠키로 저장할 값들이 `어디에서 왔느냐`에 따라서** 두가지 종류로 나뉜다


- 1. First party Cookie 퍼스트 파티 쿠키
  - : 우리가 `이용하는 사이트의 도메인`과 관련된 쿠키
  - 웹사이트를 이용시 도메인을 접속해서 이용한다.(e.g. naver.com) <br/>
  - 이 `도메인 범위 내에서 송신하는 정보를 저장`하는 것이 바로 퍼스트 파티 쿠키!
  > 로그인 정보나, 서비스 이용에 필요한 정보들을 쿠키로 저장함.

- 2. Third Party Cookie 서드 파티 쿠키
  - : 접속한 도메인이 **아니라!**, `다른 도메인과의 통신 결과`를 담는 쿠키!
  - (e.g. 광고 서비스의 경우, 광고 서비스 자체 도메인이 있다)

<br/>

> 사이트 이용 예제<br/>

A라는 사이트를 이용한다면, 
- 1. A 사이트에서 운영하는 서버들과의 통신
  - `퍼스트 파티 쿠키`로 저장!
- 2. A 사이트에서 광고 서비스를 이용하고 있다면?
  - B라는 광고 서비스 도메인과 통신.
  - `서드파티 쿠키`로 따로 저장!
<br/>
<img src="/assets/images/Third-party-cookie.jpeg" /><br/>
이 유저가, 수익을 위해 광고를 붙여둔 B사이트에 접속하면<br/>
<img src="/assets/images/Third-party-cookie_2.jpeg" /><br/>

> `각 통신 도메인에 따라` 퍼스트파티, 서드파티 쿠키로 저장이 된다<br/>

## 그럼 서드파티 쿠키지원이 중단되면?

타겟팅 광고를 할 수 없기 때문에, 리타겟팅 광고 서비스들이 피해를 받는다!<br/>
타겟팅 광고를 할 수 없기 때문에, 리타겟팅 광고 서비스들이 피해를 받는다!<br/>
타겟팅 광고를 할 수 없기 때문에, 리타겟팅 광고 서비스들이 피해를 받는다!<br/>
타겟팅 광고를 할 수 없기 때문에, 리타겟팅 광고 서비스들이 피해를 받는다!<br/>