---
published: true
title: "👩🏻‍💻 배경지식 쌓기 Step (4) - CSS 방법론, SSR/CSR, 함수형과 객체지향, 데이터를 저장하는 방법"
permalink: /cs/defaultKnowledge4
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-04-26
last_modified_at: 2022-04-26
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

## 1. CSS 방법론

## 2. 서버사이드 렌더링과 클라이언트 사이드 렌더링

## 3. 함수형 프로그래밍과 객체지향 프로그래밍

## 4. 추상 메서드, 추상 클래스, 인터페이스

## 5. 데이터를 저장하는 방법

앱에서 나오는 데이터를 어디에 저장해야할까?

### 5-1. Redux

엄청 간단한 중앙 저장소
RAM 같은 존재
앱 꺼지면 날아간다 (따라서 안전함)
데이터를 불러올 때 성능이 가장 좋다




### 5-2. AsyncStorage / EncryptStorage

껐다켜도 저장되어야하는 데이터를 넣는다

AsyncStorage
- 암호화되지 않음
- 누구나 열어볼 수 있어서 위험하다
- 따라서 보안에 민감하지 않은, 계속 유지되어야하는 데이터

EncryptStorage
- 암호화됨
- 보안에 민감한 데이터
- AsyncStorage와 사용방법 동일

### 5-3. react-native-config

개발 환경별로 달라지는 값은 react-native-config


### 5-4. 요약

- 보안에 민감하다면?
  - 앱을 꺼도 저장되어야한다면 encrypted-storage
  - 앱을 끄면 날아가도 된다면 redux
- 개발 환경별로 달라지는 값이라면?
  - react-native-config에 저장(암호화 안 됨)
- 그 외 유지만 되면 되는 데이터들
  - async-storage에 저장(npm install @react-native-async-storage/async-storage)








// 앱에서 서버로 요청을 보낼때는, 서버는 기본적으로 요청을 누가 보낸건지 모른다.
// 요청에는 아무런 상태가 없기 때문에.
// 그래서 요청을 보낼 때에 힌트! 토큰을 넣어서 보내면 서버가 토큰을 까보고 누군지 알아낸다.
// 요청한 사람이 누구인지 알려주는 것이 바로 토큰

// 서버에 요청을 보낼 땐 accessToken 안에 유저 정보가 담겨있다
// 그럼 refreshToken은 어디에 쓰지?
// 만약 accessToken이 탈취당해서 해커가 내 accessToken를 써서 서버에 요청을 보내면 정상적으로 응답해버려서 큰일남
// 그래서 accessToken에는 유효기간을 둔다. 짧은 것이 좋음
// 은행 어플을 사용하면 로그인 유지기간 30분, 연장하시겠습니까라는 알림이 뜨는데 이게 바로 accessToken 유효기간이 30분으로 정해져있는 것
// 그럼 이 유효기간 연장을 어떻게 하느냐?
// refresh 토큰을 서버로 보내고, 그럼 서버는 accessToken을 새로 발급해준다. 그럼 유효기간도 다시 갱신됨
// 그럼 refresh 토큰까지 같이 털려버리면 진짜 답이 없는 상황임. 그러니 refresh토큰은 반드시 암호화를 해야함
// 토큰 정보안에 유효기간까지 들어있음

// accessToken과 refreshToken은 저장소를 분리하는 것이 좋다
// 앱에서는 accessToken은 redux에, refreshToken은 EncryptedStorage에
// 웹에서는 accessToken은 메모리에, refreshToken은 LocalStorage에 넣는 식으로
// accessToken은 털려도 유효기간이 있는데, refreshToken은 유효기간이 훨씬 길어서 위험하기때문

// 그래야 혹시나 털렸을 때 한쪽만 훔쳐갈 수 있도록.

// 구글에 가보면 현재 로그인되어있는 기기들을 볼 수 있다.
// 구글은 이런 refreshToken을 DB화해놓고 있어서, 그 중 하나에서 강제로 로그아웃시키기를 누르면 refreshToken을 없애버리는 방식인 것.
