---
title: "두번째노드테스트"
permalink: /cs/node2Second
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-02-09
last_modified_at: 2022-02-09
---

![]()

Node.js
나오기전까지는 JS를 브라우저에서만 쓸 수 있었다.
노드가 나와서 이제는 브라우저만이 아닌, 서버사이드에서도 쓸 수 있게 되었다.

=> Node는? JS를 서버사이드에서 쓸 수 있는 언어


Express.js
Node.js가 자동차의 엔진이라면,
그 엔진을 가지고 자동차(웹사이트, 어플리케이션)를 쉽게 만들 수 있게 도와주는 것

Node.js를 쉽게 이용할 수 있게 해주는 프레임워크 개념


http://expressjs.com/en/starter/installing.html

$ npm install express --save
뒤에 --save를 붙이는 이유는,
dependency에 추가해서

이 어플리케이션에서는 express 라는 라이브러리를 쓰고 있따라는 것을 알려주기 위해서.




## 4.

모델이란?

스키마를 감싸주는 역할을 하는 것

스키마란?

데이터의 타입과 최대길이 등을 하나하나 지정할 수 있는 것을 스키마라고 함
(하나하나의 정보를 지정해줄 수 있는 것)


## 6.

git이란?

툴. 소스코드를 관리할 수 있는 툴. 

github?
클라우드 서비스


깃으로, 소스코드를 깃허브에 올린 다음에 깃허브에서 사람들과 공유하고 수정할 수 있게 해주는 클라우드 서비스

=> 결론
깃? 툴
깃허브? 깃을 사용하는 서비스





## 7.

body parser를 이용해서
클라이언트에서 입력하는
아이디, 비번을 받을 수 있다


## 8. nodemon

노드 서버를 킨 다음에 무언가를 바꾸면,
원래는 서버를 껐다가 다시 켜야 바꾼 소스가 반영이 된다.
이걸 이용하면 굳이 껐다가 키지 않아도 자동으로 소스의 변화를 감지해서 업데이트를 해줌

npm install nodemon --save-dev

-dev를 붙이는 이유?
로컬에서 하는 development mode,
배포 후 production mode
두가지 모드가 있는데, -dev를 붙이면
로컬에서 할 때만 사용을 하겠다는 뜻


## 9. 비밀정보 보호하기

몽고DB에 연결하는 URI에는 아이디와 비번이 들어있으니,
이걸 gitIgnore에 추가해서 못보게해야함.
로컬환경일 경우 URI를 가져오는 곳은 
배포환경을 경우엔 HEROKU라는 웹사이트(이런 걸 관리해주는 사이트)에서

분기처리를 해줘야한다.

## 10. Bcrypt 라이브러리로 비밀번호를 암호화하기

Bcrypt를 사용하는 이유?

사용자가 입력한 비밀번호가 데이터베이스 상에 그대로 노출되어있음.
관리자도 비밀번호를 알 수 없게 암호화가 필요하다.






# client


npx create-react-app .

.를 붙이는 이유는 이 디렉토리 안에 create-react-app 을 실행하겠다


## npm과 npx의 차이

### npm(Node Package Manager)

npm install에는 local download와 global download가 있다

npm install
로컬에 다운로드. node_modules/.bin에 다운받아진다

npm install -g
글로벌로 다운로드. 프로그램 안에서만 다운받아지는 것이 아니라, 컴퓨터 안에 bin/ 폴더 안에 다운로드가 됨

기존에는 npm install -g create-react-app 을 이용해서 글로벌로 설치했다

그런데 이제는 npx create-react-app을 하면,
npx가 npm registry에서 create-react-app를 찿아서 다운로드 없이 실행시켜준다

1. 디스크 공간 낭비하지 않음
2. 항상 최신 버전 사용 가능

npm install create-react-app 하면 create-react-app 패키지를 해당 디렉토리 루트에 node_modules폴더를 생성하고 거기에 다운로드가 됩니다.  

npx는  그 패키지를 로컬에 다운로드 받지 않고 바로 실행해서 리액트앱을 생성하게 됩니다.


웹팩이 관리하는 부분은 src폴더 안에 있는 것들만!
그 외에 public은 웹팩이 관리 안해준다
그래서 이미지 파일 등을 넣고싶을 때는 웹팩이 모아줄 수 있도록 src폴더 안에 넣어야한다



# 20. React Router Dom

React에서는 페이지 간 이동을 할 때 Router를 사용


<Route path="/users" component={Users} />
<Route path="/users/create" component={CreateUser} />

여기 두개의 라우트가 보이시죠 



exact이  없다면     

http://app.com/users   여기로 갔을때   Users 컴포넌트로 가는데 

http://app.com/users/create  여기로 갔을때도   Users 컴포넌트로 갑니다  원래는  CreateUser 로 가야되는데 말이죠... !

그 이유는 Router가  부분적으로만 닮아도  같은거라고 인식해버려서  처음 보는 Route의 컴포넌트로 이동시켜버려서 입니다.

그래서 부분적인것만 닮아도 같은거라고 인식하는 부분을 없애기 위해서 

exact를 넣어주는것입니다 !  





## 22 port 번호만 맞추면 되는 거 아니었어?

Access to XMLHttpRequest at 'http://localhost:5001/api/hello' from origin 'http://localhost:3000' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.

서버의 포트는 5001, 클라이언트의 포트는 3000

클라이언트에서 포트넘버만 5001으로 요청을 보낸다고 그냥 보내지지 않는다.
두개의 다른 포트를 가지고 있는 서버는 아무 설정없이 Request를 보낼 수 없다!

Cors 정책 때문에.

Cross-Origin Resourse Sharing (CORS)

각 Origin (서버와 클라이언트)을 Sharing할 때 적용되는 보안 정책.



## 26 Redux

Redux란?

상태(state) 관리 라이브러리

그럼 상태란?

props VS state

### 1. props

부모가 내려주는 properties.

- 1. 위에서 아래로 (부모에서 자식으로)
- 2. 변경불가( 부모가 바꿔서 다시 내려줘야 함)

### 2. state

컴포넌트 내부에서 데이터전달 / 교환 가능

- 1. 부모가 내려준 것 X
- 2. 변경가능 (변경되면 re-render된다)


이런 state를 관리해주는 것이 바로 Redux

Action / Reducer

### 1. Action
무엇이 일어났는지 설명하는 객체

### 2. Reducer






## 27. Redux SetUP하기

1. Dependency 설치

npm install redux react-redux redux-promise redux-thunk --save


- redux
- react-redux
- redux-promise
- redux-thunk

설치

### redux와 redux hook의 차이

redux-promise, redux-thunk가 왜 필요하지?

이 둘은 리덕스 미들웨어. 리덕스를 잘 쓸 수 있게 도와줌

redux 안의 모든 state는 store가 들고있다.
이 state를 변경하고 싶으면 반드시 dispatch를 이용해서 action으로 변경하는 방법 뿐이다.
이 action은 반드시 객체의 형식이어야함. 그래야 store가 받을 수 있다
하지만 store에는 매번 객체만 들어오는 것이 아님! Promise 형태일 수도 있고, function 형태일 수도 있다.
그러면 객체만 받을 수 있는 store는 당연히 받지 못한다.
그래서 받은 것이 바로 redux-promise와 redux-thunk.
redux-thunk는 function을 받는 방법을 알려주고
redux-promise는 promise를 받는 방법을 알려준다



## 28. React Hooks

React Component
- Class Component
- Functional Component

1. Class Component
- 많은 기능 사용 가능
- 코드가 길다
- 복잡하다
- 느린 성능

2. Functional Component
- 적은 기능 사용 가능
- 코드가 짧다
- 간단하다
- 빠른 성능


## 33 Authentication

인증체크는 HOC(High Order Component)로.

다른 컴포넌트를 받아서 새로운 컴포넌트를 return하는 function.

const EnhancedComponent = higherOrderComponent(WrappedComponent)

