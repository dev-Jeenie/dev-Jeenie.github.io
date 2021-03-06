---
published: true
title: "22.05.11. 첫번째 면접 회고 🥲"
permalink: /cs/developerJobInterview
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-05-12
last_modified_at: 2022-05-12
---
****
![]()

# 반성의 시간

오늘 개발자로서 처음으로!!! 면접이 있었다. <br/>
너무 긴장해서 아무것도 생각이 나질 않았다. 이렇게까지 긴장하다니! <br/>
준비했던 멘트도 다 날라가고, 아는 것도 어버버... 말그대로 아무 말을 했다. <br/>
(되짚어보니 긴장해서 말보다 휘적휘적 손짓을 많이 한 것 같다) <br/>

많은 질문을 받았지만, 제대로 대답한 게 한개도 없었다. <br/>
그런데도 계속 질문을 주셔서 정말 죄송하고 감사하기까지도 했다.....🥲 <br/>

다 한 번쯤은 들어본 내용인데도 설명할 수가 없었다. 그럼 모르는 거다.<br/>
제대로 설명할 수 없는 건 모른다는 것이다.<br/>

내가 얼마나 부족한지, 얼마나 준비가 안되어있었는지 다시 깨닫게 되었다. <br/>
나는 기본적인 흐름에 대한 이해 없이, 면접을 시험범위 안에서 출제되는 객관식 시험으로 생각했던 것 같다.... <br/>
면접 복기를 하며 다시 정리해야지. <br/>

# 받았던 면접 질문들

## CS
- MVC 패턴
  - 디자인 패턴 중 하나로, 프로젝트를 체계적으로 관리하기 위해 Model, View, Controller 세가지로 분류한 패턴
- CI/CD
  - 지속적 통합/지속적 배포라는 뜻으로, 어플리케이션 개발부터 배포까지를 자동화해서 빈번하게 배포할 수 있도록 하는 것
- HTTP Method
  - 클라이언트에서 서버로 요청하고, 서버에서 클라이언트로 응답을 줄 때 사용하는 프로토콜
- 대표적으로 GET, POST의 차이
  - GET은 CRUD 중 Read에 해당, HTTP HEADER에 요청을 적는다. URL에 데이터를 담기 때문에 길이 제한이 있다
  - POST는 CRUD 중 Create에 해당, HTTP BODY에 데이터를 담는다

- CS적인 스터디를 한다고 했는데, 어떤 부분을 공부하고 있나?


- Android와 IOS 개발에 대해서는 간접적으로라도 배운 적이 있는가?

- 디자인 구조?

## React

### React에서의 불변성을 지켜야하는 이유

React의 화면 업데이트와 관련이 있다. <br/>
React는 상태를 감시하고 있다가 변경된 상태에 따라 컴포넌트가 리렌더링 되는데, <br/>
변경된 상태가 만약 객체(배열,객체,함수) 타입 데이터일 경우 참조하는 위치가 동일하기 때문에 <br/>
React가 변화를 감지하지 못해 화면을 렌더링하지 않는다. <br/>

따라서 **`앝은 복사`**가 아닌 **`깊은 복사`**가 필요한데, <br/>
**`immer`** 라이브러리 등의 이용으로 새로운 레퍼런스 주소를 만들어 React에게 변화를 알려줘야한다. <br/>



### React를 배우면서 어려웠던 점?
- 웹 퍼블리싱과 React Native 퍼블리싱?
- React / React Native에 대한 공부를 하는가?


### Redux를 사용해본 적이 있나?
### lodash를 써본 적이 있나?
### 그럼 lodash 없이 배열의 요소에서 중복을 제거하는 방법은?
### 쿠키와 세션의 차이


- 공통점 : 웹 통신간 유지하려는 정보(ex:로그인 정보 등)를 저장하기 위해 사용하는 것
- 차이점 : 저장위치, 저장형식, 용량제한, 만료시점 등
  - 쿠키 : 개인 PC에 저장됨.
  - 세션 : 접속중인 웹 서버에 저장됨.


| -- | -- | -- |
| -- | 쿠키 | 세션 |
| 저장위치 | 클라이언트(=접속자 pc) | 웹 서버 |
| 저장형식 | text | Object |
| 만료시점 | 쿠키 저장시 설정(브라우저 종료해도 만료시점 전까지 자동삭제 안됨) | 브라우저 종료시 삭제(기간 지정 가능) |
| 사용자원(리소스) | 클라이언트 리소스 | 웹 서버 리소스 |
| 용량제한 | 총 300개, 하나의 도메인 당 20개, 하나의 쿠키 당 4KB | 서버가 허용하는 한 용량제한 없음 |
| 속도 | 세션보다 빠름 | 쿠키보다 느림 |
| 보안 | 세션보다 안좋음 | 쿠키보다 좋음 |





출처: https://hahahoho5915.tistory.com/32 [넌 잘하고 있어]



  - 그럼 세션 ID는 언제 사용하나?
### Promise all?
### Spread operator를 써본 적이 있나?
  > (이 질문을 불변성과 관련해서 답변해야 했다...🥲) <br/>

전개 연산자를 사용하여 객체나 배열 내부의 값을 복사할 땐 얕은 복사한다.<br/>
즉 **내부의 값이 완전히 새로 복사되는 것이 아니라, 가장 바깥쪽에 있는 값만 복사**된다.<br/>

=> 따라서 내부의 값이 객체라면, 내부의 값 또한 따로 복사를 해야한다!<br/>

내부 요소가 바뀌었을 때에도 state를 바꾸고, DOM을 다시 그리기 위해서는,<br/>
새로운 객체나 배열을 만들어 **새로운 참조값**을 만들고<br/>
React에게 **이 값은 이전과 다른 참조값**임을 알려야한다!<br/>

객체의 구조가 복잡해진다면, 불변성을 유지하면서 업데이트하는 것이 까다로워진다. <br/>
이런 복잡한 상황일 때 immer라는 라이브러리로 편하게 작업 가능 <br/>

- **React에서 immutable variable**을 만드는 방법

  - 1) ES6의 Object.assign() 또는 object-rest-spread
  - 2) JS 표준 라이브러리 immutable-js
  - 3) React 공식문서 추천 패키지 immmutabillity-helper


### 어떤 함수가 1번 페이지에서 2번 페이지로 가도 실행되어야하고, 3번 페이지에서 2번 페이지로 가도 실행되어야할 때 2번 페이지에 useEffect로 어떻게 처리?




## Java Script

### 깊은 복사와 얕은 복사의 차이
    -  예를 들면?
### Arrow function과 일반 function의 차이
### immutable과 mutable
### 호이스팅은?
### Java Script와 비교했을 때, Type Script를 사용하며 느낀 장점은?
### 자바스크립트로 정렬을 해본 적이 있는가?

## 기타
### M1칩과 기존 맥북칩의 차이를 아는가?
### 어떤 노력을 해서 프론트엔드 개발자가 되었는지?
### 스터디 등을 진행하고 있는지?
### 진취적이라고는 하는데, 주얼리 업계든 퍼블리셔이든 도전한 것들이 그다지 진취적이게 느껴지지 않는다.

### 개발 공부를 하며 느낀 점은?












## 면접후기

면접 막바지에 면접관님께서 해주신 말씀이 있다. <br/>
우리는 이미 잘하는 사람, 잘하진 못하지만 잠재력이 있는 사람, 다 아니어도 하드워킹으로 커버가 가능한 사람을 원한다. <br/>
누구에게 기대지 않고 스스로 성장할 수 있는 사람이야말로 발전하는 개발자다. <br/>

나는 당당하게 스스로 발전하고 있다고 말할 수 있었나? <br/>
아니! 너무 부끄러웠다! <br/>
