---
title: "React란? #1 리액트 프로젝트 시작하기 ⭐️"
permalink: /cs/ReactProgramming
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-02
last_modified_at: 2021-12-02
---

![]()

# 리액트란 무엇인가?


UI 기능만 제공

앵귤러와는 달리 개발환경 직접 구축해야함!


- 자동으로 업데이트 되는 UI
- UI = render(state)
- render함수는 `순수함수`로 작성(입력값이 같으면 출력값이 똑같아야 하는 것)
  - 랜덤함수사용 x
  - 외부상태변경 x
- state는 `불변변수`로 관리! (새로운 객체를 만들어서 값을 할당하는 것)
- 가상돔(virtual DOM) : 이전 UI상태를 메모리에 유지해서 변경된 부분만 업데이트하는 것!

=> 순수함수와 불변변수를 적극사용하면 버그발생 낮아지고 복잡도가 낮아짐
그리고 랜더링 속도도 빨라짐


(객체지향 프로그래밍과 반대되는 개념이 함수형 프로그래밍)

# 리액트 개발환경 직접 구축하기

React.useState는 이 파일이 실행될 때 전역변수로 실행이 된다!

createElement
- UI를 표현하는 가장 작은 단위가 리액트 요소이다
- 첫번째 인자로 선택한 태그, 두번째 인자로 함수 메소드 및 스타일 등


# 바벨 사용해보기

- 자바스트립트 코드를 변환해주는 컴파일러
- 최신 자스 문법을 지원하지 않는 환경에서도 
createElement로
- react 에서는 JSX 문법을 사용할 때 변환하기위해 사용

npm init -y (패키지 제이슨 파일이 설치됨)
npm install @Babel/core @babel/

npx babel

- 프리셋과 플러그인
  : 여러개의 플러그인을 특정 목적으로 모아둔 것이 프리셋인 것.



# 웹팩 사용해보기

- 다양한 기능 제공

  - 파일 내용을 기반으로 파일 이름에 해시값 추가 => 효율적 프라우저 캐싱
  (Vㅏ일 이름 자체가 해시의 키가 된다면 서버에게 ㅇ물어볼 필요가 없은 ㅣ효율적

  - 사용되지 않은 코드 제거
  - Java Script 압축
  - JS, CSS, JSON 텍스트 파일 등 일반 모듈처럼 불러오기
  - 환경 변수 주입

- 웹팩을 사용하는 가장 큰 이유 => 모듈 시스템을 사용하기 위해서!

export 

하나하나로 다 묶어두고, 빼다 쓰는 것을 모듈시스템이라고 한다.
export default 를 사용하지 않으면 중괄호로 담아서 import 해야한다!
as로 이름을 변경할 수도 있음.

웹팩을 사용하면 변수이름 충돌 등은 빌드단계에서 해결 가능
외브라이브러릴는 npm으로 관리 가능

- 요즘 브라우저는 ESM을 지원한다. 하지만
  - 오래된 브라우저
  - 많은 오픈소스가 commonJS로 작성됨








==========다른파일









# create-react-app(CRA)

리액트 개발환경을 직접 구축하려면 많은 지식과 노력이 필요함.

빌드 시스템 구축을 위해서 웹팩과 바벨 등을 써야하고,
제스트를 이용해서 테스트 환경 구축해야하고,
오래된 브라우저 지원을 위해 polyfill 도 추가를 해야하고,
HMR 코드 수정 시 화면에 바로 적용되는 기능과 css 후처리 등도 처리해야함

=> create-react-app이 자동으로 구축해서 제공해준다 !



서버사이드 랜더링의 지원여부

cra는 지원하지 않음!
깔끔한 방법이 아ㅓㅂㅅ다

필수인 프로젝트면 Next/js를 선택해야함.

백오피스처럼 서버사이드 랜더링이 필요없을 때 쓰는 것.

cra는 빌드시스템 변경이 불가능함.



npm start 는 개발모드에서만 써야함. 성능 최적화가 안되어있어서

배포할때는 반드시 build명령어를 써야한다

serviceWorker는 serviceWorker.unresister 되어있기 때문에 아직 동작하지 않음


strictMode는 리액트에서 잘못 사용하는 것을 잡아내기 위해 쓴다.

import logo from '~~.svg'이렇게
이미지 해시 값으로 사용하는게 좋다. 브라우저 캐싱을 효율적으로 활용이 가능!
이미지 뿐만 아니라 데이터도 마찬가지.
데이터가 특정 순간에만 필요하다고 할 때에도, 해시값으로 받아오는게 좋다.
- 1. 그냥 데이터를 받아오게 해두면, 버튼 클릭하기도 전에 데이터가 있는 상태로 번들이 구성이된다
- 2. import로 또 쓰면 파일이 받아와진다

```JS

import('./data.json')// 1번의 경우

function onClick() {
  import('./data.json').then({default: data}) => {
    console.log({ data })
  } // onClick 함수안에 담은 2번의 경우
}

```






npm start로 사용하게 되면 기본적으로http가 실행된다.

https로 실행하고싶다면 `HTTPS=true npm start`
윈도우는 https로 실행하고싶다면 `set HTTPS=true && npm start`

빌드하게 되면 정적파일이 생성이 됨.
build폴더 안에 있는 정적파일로 서비스만 하면 된는 것.
그러니까 서버사이드 랜더링으로 동작을 할 수 없는 것!

> react developer tools 크롬 익스텐션


bulid 명령어
빌드 시 큰이미지는 media폴더 안에 내장되는데,
HTTP요청 횟수를 줄이기 위해, 작은 image를 JS파일 내부에 포함한다. (2.0부터는 성능이 좋아져서 그럴 필요는 없긴함)
좀 더 빠르게 이미지를 보여줄 수 있는 장점이 있다.


text 명령어 
(test.js를 붙이면 test 파일이 된다.)

eject 명령어

react-scripts를 사용하지 않고 모든 설정파일을 `추출`하는 명령어
cra를 기반으로 직접 개발환경을 구축하고 싶을 때

추출하지 않으면 cra rㅣ능 추가됫을 때 단순히 버전만 올리는것만 하면 되는데,
추출을 하면 설정파일을 수정을 해버려야하니까 꼭 필요하지 ㅇ낳다면 관리측면에서 추출하지 않는 것이 좋다. 

polyfill

IE에서 지원안되는 것을 지원하고 싶을 ㅅ때 사용.

CRA는 기본적으로 core.js가 내장되어있어서 import 만하면 됨.
보통 core.js 를 사용한다.


`환경변수`란?
환경변수는 개발, 테스트 또는 배포 환경별로 다른 값을 적용할 때 유용하다.
전달된 환경 변수는 코드에서

```JS
process.env.{변수이름}
```
이렇게 사용할 수 있따

CRA는 기본적으로 NODE_ENV라는 값을 가지고 있음.
npm start 로 실행하면 .env.development
npm test는 .env.test
npm build는 .env.production






# CSS 작성방법 결정하기

- 일반적인 css파일 작성
 : 이름 충돌 문제

- css 모듈
 : module.css 형식으로 작성.
 객체 형식이기 때문에 객체로 들어옴
 해시값이 붙어서 들어가기때문에, 각 클래스명은 고유값을 가진다. 이름충돌문제 해결!
 classnames라는 걸 설치하면 좀 더 깔끔하게 작성할 수 있다
 cn(Style.button, Style.small)

- Sass
 : node sass를 설치해야함. modulecss와 함께 사용할 수 있음. 변수 사용가능

- css-in-js
 : 재사용가능한 구조로 사용할 수 있음! JS안에있는 css
  - styled-components
  