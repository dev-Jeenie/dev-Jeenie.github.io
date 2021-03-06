---
title: "브라우저 저장소! Browser storage 🌏"
permalink: /cs/browserStorage
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-20
last_modified_at: 2022-01-20
---

![]()



# 브라우저 저장소


## 1. local storage

- 단순히 `key value` 저장소의 기능을 한다.<br/>
- string 으로만 지원<br/>
- 최대 저장용량 제한이 5MB ~ 10MB으로 간단한 텍스트 이상 담기 힘들다<br/>
- 데이터 만료 기한 `없음`

```js
setItem("key", "value")
getItem("key")
removeItem("key")
clear()
```

## 2. session storage

- **브라우저 종료** 또는 **새 탭**을 열면 `데이터 초기화`

- 하지만 같은 탭에서 **새로고침**할 때는 `그대로 유지됨`

> ex) 텍스트 에디터에서 자동 임시저장<br/>

- 데이터 만료 기한 있음

- API 사용방법은 local storage와 동일

```js
setItem("key", "value")
getItem("key")
removeItem("key")
clear()
```


## 3. Indexed DB
- 대용량 데이터의 저장이 가능하다.
기능이 많고 저장할 수 있는 데이터 타입이 다양하다
- 상대적으로 저수준 API 제공해서 가벼운 사용에는 까다롭기 때문에,
  본격적으로 데이터를 저장해야할 때 사용한다


## 4. Cookie 🍪

쿠키란?<br/>
브라우저에 저장되는 작은 크기의 문자열<br/>
웹에서 가장 기본적이고 오랫동안 함께해온 저장소!<br/>

- 저장가능 용량 `매우 적음`
  - 저장가능 용량 약 4KB
    - 서버 데이터를 공유하는 용도로 사용되어서,
      서버에게 **요청을 할때마다 `같이`** 실려서 따라가는 Cookie가 MB단위라면 문제가 되기 때문<br/>

- Cookie는 로컬스토리지와는 다르게 데이터 유효기간을 지정할 수 있음
  - 한시간 뒤, 하루 뒤에 만료되게끔 설정가능

### 4-1. 서버사이드 랜더링에서의 Cookie와 Local storage

서버사이드 랜더링을 한다면 Cookie는 더욱 중요함<br/>

**로컬 스토리지의 경우**<br/>

- 서버사이드 랜더링 시점에 로컬 스토리지의 값을 `알 수 없음`

**쿠키의 경우**<br/>

- 서버사이드 랜더링 시점에 쿠키 데이터의 값을 `알 수 있음`

- 필요한 데이터들을 미리 쿠키에 넣어두면, <br/> 서버에서 HTML을 랜더링할 때 **더 많은 정보를 `미리` 담을 수 있다**

**=> 로딩시간 단축**


## 5. 결론!

### 5-1. 요약

- 로컬 스토리지 (local storage)

- 세션 스토리지 (session storage)

- 쿠키 (cookie)

### 5-2. 차이점

| -- | -- | -- |
| 로컬 스토리지 | 세션 스토리지 | 쿠키 |
| 로컬 스토리지 | 세션 스토리지 | 쿠키 |


⭐️ **로컬 스토리지와 쿠키의 차이점** ⭐️<br/>
