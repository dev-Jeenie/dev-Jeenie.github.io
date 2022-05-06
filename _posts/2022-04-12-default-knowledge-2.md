---
published: true
title: "npm, Webpack, Babel, HTML/CSS, CSS Media Query"
permalink: /cs/defaultKnowledge2
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-04-14
last_modified_at: 2022-04-14
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

## 1. npm 이란?

### 1-1. 미리 알아야할 Node.js


> Node.js®는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임입니다. Node.js는 이벤트 기반, Non 블로킹 I/O 모델을 사용해 가볍고 효율적입니다. Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 합니다.<br/>
출처 : Node.js 공식 사이트<br/>

공식 사이트에 따르면 node는 **`JavaScript 런타임`**이다. <br/>
JavaScript 기반으로 구성된 서버 사이드 서비스를 JavaScript로 구현할 수 있게 만든 런타임!<br/>


#### 1-1-1. 자바스크립트 런타임이란?

자바스크립트 런타임이란 **자바스크립트가 `구동되는 환경`**을 말한다.<br/>
이러한 자바스크립트 런타임의 종류로는 웹 브라우저(크롬, 파이어폭스, 익스플로러 등)프로그램과 Node.js가 있다. <br/>
이러한 프로그램들에서 자바스크립트가 구동되기 때문에 ***자바스크립트 런타임***이라고 한다<br/>

### 1-2. 그럼 npm은?

**Node.js로 만들어진 pakage(module)을 관리해주는 툴.** <br/>

node.js 기반의 모듈을 모아둔 집합 저장소이다. <br/>
Node Package Manager 또는 Node Package Modules라고도 한다.<br/>
자바스크립트 런타임 환경 Node.js의 기본 패키지 관리자이다.<br/>
Node.js 개발자들이 패키지(모듈)의 설치 및 관리를 쉽게 하기 위해 도와주는 매니저(관리 도구) <br/>
명령 줄 클라이언트, 그리고 공개 패키지와 지불 방식의 개인 패키지의 온라인 데이터베이스로 이루어져 있다.<br/>
간단히 말해 `자바스크립트 패키지 매니저`이다.<br/>


Node.js에서 사용할 수 있는 모듈들을 ***패키지화***하여 모아둔 `저장소` 역할과 패키지 설치 및 관리를 위한 `CLI(Command line interface)`를 제공한다.<br/>
자신이 작성한 패키지를 공개할 수도 있고 필요한 패키지를 검색하여 재사용할 수도 있다.<br/>


### 1-3. 패키지 매니저를 사용하는 이유?

- 코드의 재사용성 우수, 유지 보수가 쉽고 형상관리가 용이
- 내가 원하는 기능을 직접 구현하지 않아도 됨

### 1-4. npm 패키지 설치 방법
Node.js에서 사용할 수 있는 모듈인 패키지를 설치할 때에는 npm install 명령어 뒤에 설치할 패키지 이름을 지정한다.


```js
$ npm install <package>
```




-npm
-Webpack, Babel
-HTML/CSS
-CSS Media Query


https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/
<br/>
https://poiemaweb.com/nodejs-npm


> npm run eject<br/>
  react 프로젝트에서 해당 명령어를 입력하면 webpack 설정이 열린다.<br/>
  하지만 한번 열린 것을 다시 되돌릴 수는 없으니 조심하자.(깃으로 되돌리는 방법 뿐)<br/>


## 2. Webpack, Babel

자바스크립트 es5 버전에서는 모듈을 지원하지 않아서, `CommonJS` 모듈과 `AMD(Asynchronous Module Definition)`를 사용했다.<br/>
es5 자체적으로 모듈 개념이 없었기 때문에 es6 버전에서, 두 스탠다드 (CommonJS와 AMD)의 장점들을 가져와 새로운 포맷을 만들어냈다.<br/>

- CommonJs처럼 간결한 문법으로 싱글 export와 순환 의존성을 지원
- AMD처럼 비동기 로딩과 모듈 로딩을 지원

그리고 자바스크립트라는 언어 자체가 모듈을 지원하기 때문에<br/>
간결한 문법, 구조가 static 하게 분석이 가능해졌으며 최적화가 가능해졌다.<br/>

🤷🏻‍♀️ : 그럼 잘된 거 아니야? 웹팩을 왜 써?<br/>

=> 브라우저는 여전히 파일 단위 모듈을 모르기 때문에!<br/>

es6 버전은 일부 브라우저에서만 지원한다.<br/>
웹은 하나의 소스로 모든 브라우저에 보여주기 때문에, 모듈을 **하나의 파일로 묶어서** ***네트워크 비용을 최소화***해야한다.<br/>
이 하나로 묶는 과정을 바로 `번들링`이라고 한다.


### 2-1. Webpack

***`모듈 번들러`***! <br/>

> 모듈 번들링이란? <br/>
html 파일에 들어가는 자바스크립트 파일들을 하나로 만들어주는 방식 <br/>

따라서 웹팩은, 필요한 다수의 자바스크립트 파일을 하나의 자바 스크립트 파일로 만들어 주는 것을 말함. <br/>
리액트 프로젝트에는 이미 웹팩이 설정이 되어 있어 처음부터 커스텀 세팅할 일이 많지는 않지만<br/>
기능 추가를 위해 웹팩 설정이 있다<br/>

🤷🏻‍♀️ ?? : 이렇게 중요한 웹팩을 왜 설정해 본 적이 없을까??? <br/>
***=> react가 알아서 척척 다 해줬기 때문이지!***<br/>

create-react-app으로 프로젝트를 생성하면,<br/>
react가 웹팩 세팅을 다 해주니까 기본적인건 다 완료 되어있는 상태로 개발을 시작한다.<br/>
그래서 create-react-app 이 편하다는 거야!<br/>




entry파일을 지정해서, entry 파일이 **의존성을 띄고 있는 모듈들을 모두 `하나로`** 묶어내는 라이브러리.<br/>

이 모듈 번들러에는 네가지 개념이 있다.

- 엔트리
- 아웃풋
- 로더
- 플러그인

#### 2-1-1. 엔트리

엔트리는 <strong style="color:black;background-color:yellow">의존성 그래프의 시작점</strong>을 의미한다.<br/>
엔트리 파일을 의존하는 파일은 없고, 엔트리 > A를 의존 > A가 B를 의존 > B가 C를 의존하는 식으로 모듈이 연결된다. <br/>
이때 웹팩은 이미지, 폰트, 스타일시트 역시 모듈로 관리한다. 설정파일에서 엔트리 파일을 지정할 수 있다.

```js
// webpack.config.js
module.exports = {
    entry: {
        main: './src/main.js',
    }
}
```
src/main.js가 시작점. 이렇게 entry 키에 시작점 경로를 지정한다. <br/>


#### 2-1-2. 아웃풋

엔트리에 설정한 자바스크립트 파일을 시작으로, 의존되어 있는 모듈을 하나로 묶어서 내보낸다 = 번들링해서 내보낸다. <br/>
번들된 결과물이 나오는 위치는 output 키에 기록한다. <br/>

```js
// webpack.config.js
module.exports = {
    output: {
        filename: 'bundle.js', 
        path: '.dist'
    }
}
```
dist 폴더에 bundle.js 파일에 결과가 나오게 된다. <br/>


아래처럼 html 파일에는 번들링된 이 하나의 파일만 나오면 된다.

```html
<body>
    <script src="./dist/bundle.js"></script>
</body>
```


#### 2-1-3. 로더

웹팩은 자바스크립트 파일 뿐 아니라 이미지, 폰트, 스타일시트까지 전부 모듈로 관리한다. <br/>
하지만 웹팩은 자바스크립트 밖에 알지 못한다. 이미지, 폰트, 스타일 시트 등 자바스크립트가 아닌 파일들은 웹팩이 이해하도록 바꿔야한다. <br/>
바꾸는 역할을 `로더`가 한다. <br/>

##### 2-1-3-1. css-loader

css를 자바스크립트 파일로 변환해서 로딩할 때 사용하는 로더이다. <br/>

test에 로딩할 파일을 지정해주고, user에 사용할 로더를 정해주면 된다.

```js
//webpack.config.js 
module.exports = {
    module: {
        rules: [{
            test: /\.css$/,
            use: ['style-loader', 'css-loader']
        }]
    }
}
```

#### 2-1-4. 플러그인

- 로더
  - 번들되기 전에 파일단위를 처리
- 플러그인
  - 번들된 결과물을 추가로 처리
  
번들된 자바스크립트를 난독화, 특정 텍스트를 추출하는 용도로 사용할 수 있다.

##### 2-1-4-1. UglifyJsPlugin

자바스크립트 결과물을 **난독화 처리**하는 플러그인이다.<br/>

플러그인을 사용할 때는 웹팩 객체의 plugins 배열에 추가한다.




### 2-2. Babel

최신 문법을 모르는 브라우저를 위해 es6, es7 문법의 자바스크립트를 es5로 바꿔주는 컴파일러.<br/>

자바스크립트 언어의 환경을 전반적으로 바꿔주는 역할을 한다.<br/>
간단히 말해 자바스크립트 es6 문법을 이해하지 못하는 구 브라우저들을 위한 `번역기`!<br/>


브라우저가 ES6를 지원하든 지원하지 않든 ES6를 사용하고 싶다? <br/>
=> ***babel 설치!***

단, babel 을 사용한다고 최신 함수를 사용할 수 있는 건 아니다.<br/>
babel 은 문법을 변환하여 javascript 로 변환하는 transpiler 역할만 할 뿐, <br/>
브라우저에서 지원하지 않는 함수를 검사하는 작업을 거쳐야하는데, 이 역할을 `babel-polyfill`이 담당한다.

> polyfill이란? <br/>
  개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인 <br/>
  브라우저에서 지원하지 않는 기능들에 대한 호환성 작업을 채워 넣는다고 해서 polyfill 이라고 칭한다

> 그럼 babel-polyfill이란? <br/>
  개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인


즉, `babel`은 **컴파일시에 실행**되고 `babel-polyfill` 은 **런타임에 실행**되는 것.<br/>

```java
$npm i @babel/preset-env
``` 

로 초기설정을 마치면 따로 polyfill을 설정할 필요 없이 세팅이 완료된다.<br/>
(현재 polyfill은 deprecated 상태)



https://velog.io/@pop8682/%EB%B2%88%EC%97%AD-%EC%99%9C-babel-preset%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%98%EA%B3%A0-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%9C%EA%B0%80-yhk03drm7q

https://velog.io/@kwonh/Babel-%ED%8F%B4%EB%A6%AC%ED%95%84polyfill-babelpreset-env




- 바벨 프리셋(초기 설정)이 완료된 경우
  - 절대경로 설정 되어있음
  <img src="/assets/images/babel_alias.png" /><br/>
  
  - 절대경로 설정은 안되어있음
  <img src="/assets/images/babel_no_alias.png" /><br/>

alias는 따로 npm으로 설치할 필요 없이 내가 원하는 절대경로를 입력하면 된다.


#### 2-2-1. 바벨 설치

- 바벨의 기본 모듈 설치

```java
$npm i -D @babel/core @babel/cli @babel/preset-env
``` 

```java
$npm i @babel/preset-env
``` 
바벨의 초기설정을 마치면 babel.config.js 파일이 생성된다.


- 각 모듈의 역할

@babel/core: 바벨의 핵심 기능들을 포함.
@babel/cli: 터미널에서 바벨 명령어를 사용할 수 있게 도와준다
@babel/preset-env: 코드 구문 변환 설정을 도와줌 (지원 브라우저 점유율, 호환성 설정 등)
 
 
```java
$npm i -D @babel/plugin-proposal-optional-chaining
```


옵셔널 체이닝과 같은 플러그인 또한 설치 가능.







<!-- 
```js
module.exports = {
  presets: ['module:metro-react-native-babel-preset'],
  plugins: [
    [
      'module-resolver',
      {
        alias: {
          '#apis': './src/apis',
          '#commons': './src/commons',
          '#components': './src/components',
          '#contexts': './src/contexts',
          '#hooks': './src/hooks',
          '#nav': './src/nav',
          '#pages': './src/pages',
          '#stores': './src/stores',
          '#utils': './src/utils',
        },
      },
    ],
    'react-native-reanimated/plugin',
  ],
};

``` -->


> 참조 <br/>

https://juneyr.dev/2019-02-20/webpack-babel
<br/>

https://bravenamme.github.io/2020/02/12/what-is-babel/
<br/>

https://velog.io/@code-bebop/babel%EA%B3%BC-webpack
<br/>


## 3. HTML과 CSS


아주 간단하게 말하자면 문서의 뼈대와 화장이라고 할 수 있다.<br/>

HTML로 문서의 뼈대를 만들고, CSS로 글꼴, 배경색, 너비 높이, 위치 등을 지정하거나<br/>
브라우저 크기에 따라 다르게 화면을 표시할 수 있도록 지정한다.<br/>


CSS가 도입되기 전에는 HTML 하나로 문서의 뼈대와 화장을 같이 했다.<br/>
그래서 같은 스타일을 가지는 다른 문서임에도, 하나가 바뀌면 모든 문서를 다 바꿔야하는 번거로움이 있었다.<br/>

<img src="/assets/images/html_css.png" /><br/>


### 3-1. 스타일을 꾸미는 방법

- html 태그 안에 속성처럼 style을 적용 (In-line)
- style 태그를 사용(Internal)
- css 파일을 만들어서 html 문서에 연결(External)

여러가지의 문서를 수정하기에는 2,3 번이 좋고 그 중에서도 css파일을 만드는 3번이 가장 좋다.



## 4. CSS media query

미디어 쿼리는 CSS의 문법 중 하나이며, 반응형 디자인을 사용할 수 있도록 해준다. <br/>


> 미디어 쿼리는 단말기의 유형(출력물 vs. 화면)과, 어떤 특성이나 수치(화면 해상도, 뷰포트 너비 등)에 따라 웹 사이트나 앱의 스타일을 수정할 때 유용합니다.<br/>
미디어 쿼리는 다음과 같은 상황에 사용할 수 있습니다.<br/>
CSS @media와 @import @규칙을 사용해 특정 조건에 따라 스타일을 적용할 때.<br/>
style, link, source (en-US), 기타 다른 HTML 요소에 media 특성을 사용해 특정 매체만 가리키게 할 때.<br/>
Window.matchMedia()와 MediaQueryList.addListener() (en-US) JavaScript 메서드를 사용해 미디어 상태를 판별하고 관측 (en-US)할 때.<br/>

```css
@media <media type> and (media feature) {
  /* ... */
}
```




> 참조 <br/>
https://developer.mozilla.org/ko/docs/Web/CSS/Media_Queries/Using_media_queries