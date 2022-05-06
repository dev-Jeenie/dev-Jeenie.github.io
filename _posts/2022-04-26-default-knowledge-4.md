---
published: true
title: "CSS 방법론, SSR/CSR, 함수형과 객체지향, 데이터를 저장하는 방법"
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

css 방법론이란? <br/>
CSS를 보다 **효율적으로 작성하는 아이디어** <br/>

CSS의 역할이 커지게 되면서 CSS 클래스 이름을 어떻게 작성할지, 어떤 식으로 스타일을 작성할지 등의 방법을 정해둔 것이 방법론이다.<br/>

### 1-1. CSS 방법론들의 공통적인 목표​

- 1) **코드의 재사용성**

- 2) **직관적인 클래스 네이밍**

- 3) **원활한 유지 보수**

- 4) **확장성**

- CSS 선택자로 아이디나 타입 또는 html 태그를 사용하는 것을 지양할 것
  - 아이디는 클래스와는 다르게 재사용이 불가능
  - 마크업을 수정할 경우 스타일 또한 다시 수정해야함
​


### 1-2. SMACSS(calable and Modular Architecture for CSS)

CSS에 대한 확장형 모듈식 구조 (by Jonathan Snook)으로, <br/>
​CSS를 범주화로 패턴화하고자 하는 방법론 <br/>
CSS의 프레임워크가 아닌 하나의 스타일 가이드 <br/>


다섯 가지 범주를 제시하고 있으며 기본(base), 레이아웃(layout), 모듈(module), 상태(state), 테마(theme)로 나뉜다.​


- **사용목적**
  - Class명을 통한 예측
  - 재 사용
  - 쉬운 유지보수
  - 확장 가능
 
- **유의사항**
  - 파생된 CSS 셀렉터 사용금지
  - ID 셀렉터 사용금지
  - !important 사용 금지
  - Class 이름은 의미있게, 다른 개발자가 이해할 수 있도록 선언



#### 1-2-1. Base - 기초 스타일

기본 스타일 (Reset, Default, Variables, Mixins)
기본 스타일에는 !important를 쓸 필요가 없다.
선택자: 주로 요소 선택자 (ex. input[type=text] 같은 것)

```css

body {
    font-size: 14px;
    line-height:1.5;
}

img, fieldset, legend, button {
    border: 0;
}

hr, button img{
    display:none;
}

```
전체 웹 사이트와 모든 요소에 사용되는 기본값을 정의합니다.

​

 

#### 1-2-2. Layout - 레이아웃 관련된 스타일
Class명에 suffix “l-”를 붙인다
선택자: 아이디(#)나 클래스(.)
기능: 페이지를 구획하는 스타일(예: 헤더, 푸터, 그리드 …)
 


```css
#header {
    width: 80px;
}
#lnb {
    width: 120px;
}

.l-width #header {
    width: 300px;
    padding: 5px;
}
.l-width #lnb {
    width: 50px;
}
```
주요 요소(ID)와 하위 요소(class)로 구분하고 접두사를 사용

​



 

#### 1-2-3. Module(Components) -  모듈 관련 스타일
기능 : 레이아웃 요소 안에 들어가는 더 작은 부분들 (네비게이션 바, 말풍선, 대화상자, 위젯 등)
스타일 재사용을 위한 요소
Block, Element, Module
재사용을 위해 id 셀렉터와 element를 사용하지 않는다.
만약, element 셀렉터를 사용해야 한다면, .box > span 처럼 child 셀렉터를 사용
사용 예시) nav bar, 이미지 슬라이더, dialogs, widgets, tables, icons




​
```css
.nav-prev { ... }
.nav-next { ... }
```

재사용이 가능한 구성요소들을 정의

​


 

#### 1-2-4. State - 상태를 나타내는 스타일
기능: 다른 스타일에 덧붙이거나 덮어 씌워서 상태를 나타냄 ( 펼침과 접힘, 성공과 실패 등 )
선택자: 클래스 선택자 한개, 같은 모듈에 두 상태를 적용하지 말 것.
!important를 쓸 수 있다 (최소화 할 것)
Hidden, expend, active, hover 등의 상태에서 사용
Class명에 suffix “is-” 또는 “s-”를 붙여서 사용 (특정 모듈은 모듈 이름도 뒤에 붙인다. ex) is-tab-active )

 

#header는 레이아웃 요소임을 알 수 있다.

.is-collapsed로 접힌 상태임을 알 수 있다.

 

.msg는 모듈이다.

.is-error로 오류 상태임을 알 수 있다.

 

#searchbox 연관 된 라벨은 숨겨져 있다. ( .is-hidden )

라벨이 마크업 된 이유는 스크린 리더기를 위한 것

 
```css
.is-xl-hide { display: none; }
.is-md-hide { display: none; }
.is-sm-show { display: block; }
.is-xs-show { display: block; }

```

요소의 상태 변화를 표현하며 접두사를 사용

 

 

 

#### 1-2-5. Theme
사이트 전반적 look and feel 제어
색상이나 이미지를 불변하는 스타일과 분리하는 것. 기존 스타일을 재선언하여 사용할 수 있다.
적용범위가 넓은 테마는 “theme-”를 suffix를 붙여 사용한다.

 
```css
// base.css 선언 값
.aside {
    background: #efefef;
}

// theme.css 에서 재선언
.aside {
    background: #bebebe;
}
```


사용자가 선택할 수 있게 스타일을 제 선언하여 사용

​

​

​




​

### 1-2. BEM(Block Element Modifier)
​

블록(block), 요소(element), 상태(modifier)로 구분하는 클래스 이름을 작성하는 방법


BEM은 Block Element Modifier의 약자이다<br/>
OOP(Object Oriented Programming)와 유사하다<br/>
ID는 사용할 수 없고, 오직 class명만 사용할 수 있다.<br/>
.header __navigation ‐‐secondary과 같은 class를 사용한다<br/>
 

 

 

#### 1-2-1. Block
block은 문단 전체에 적용된 element 또는 element를 담고 있는 컨테이너를 말한다.<br/>
ex) logo / login form / menu / search from / content / footer<br/>

 


 

재사용 할 수있는 기능적으로 독립적인 페이지 구성 요소. HTML에서 블록은 class 속성으로 표시된다.<br/>
형태(red, big)가 아닌 목적(menu, button)에 맞게 결정해야 한다.<br/>
블록은 환경에 영향을 받지 않아야 한다. 즉, 여백이나 위치를 설정하면 안된다.<br/>
태그, id 선택자를 사용하면 안된다.<br/>
블록은 서로 중첩해서 작성 할 수 있다.<br/>
> ex) header, menu, search-form ….

 
우선 화면의 보이는 블록을 기준으로 첫 번째 네이밍을 작성

```css
.header {
    width: 100%;
    height: 60px;
}

.aside {
    width: 300px;
    height: 100%;
}

```



 

 
#### 1-2-2. Element
element는 block 안에서 특정 기능을 수행하는 컴포넌트이다. element는 상황에 따라 달라진다.<br/>
각 element는 두 개의 밑줄표시로 연결하여 block 다음에 작성한다.<br/>


block 이름이나 element 이름이 길 경우 ' – ' 하이픈으로 연결한다. (강제성은 없음, 프로젝트의 규칙을 적용하면 됨)<br/>


 

블록안에서 특정 기능을 담당하는 부분.<br/>
block__element 형태로 사용 (더블 언더바)
형태(red, big)가 아닌 목적(item, text, title)에 맞게 결정해야 한다.<br/>
요소는 중첩해서 작성 할 수 있다.<br/>
요소는 블록의 부분으로만 사용 할 수 있고 다른 요소의 부분으로 사용할 수 없다.<br/>
모든 블록에서 요소는 필수가 아닌 선택적으로 사용한다. 즉, 블록안에 요소가 없을 수도 있다.<br/>
> ex)  menu__item, header__title …<br/>


 

그 후 다음 블록 안의 요소들을 __로 연결하여 네이밍을 작성<br/>

```css
.header__logo {
    width: 100px;
    height: 40px;
}

.aside__list {
    display: flex;
    height: 100px;
}
```

​
 

#### 1-2-3. Modifiers
Modifier은 block 또는 element의 속성이다<br/>
이 속성은 block 또는 element의 외관이나 상태를 변화시킨다<br/>
Class명은 “–“를 추가하여 modifier 추가

 

블록이나 요소의 모양(color, size) / 상태(disabled, checked)를 정의한다.<br/>
block__element--modifier, block--modifier 형태로 사용(더블 하이픈)
수식어의 블리언 타입과 키-벨류 타입이 있다.<br/>
블리언 타입	키-벨류 타입<br/>
수식어가 있으면 값이 true 라고 가정한다.<br/>

> (form__button — disabled)<br/>

 

키, 벨류를 하이픈으로 연결하여 표시한다.<br/>

> (color-red, theme-ocean)<br/>

 

 

수식어는 단독으로 사용할 수 없다. 즉 기본 블록과 요소에 추가하여 사용해야 한다.<br/>
> ( class=”block__element block__element — modifier”)<br/>



탭 메뉴가 다른 영역에서 다른 스타일로 사용된다면 메인 속성을 복사하여 추가 하거나, 전 처리 장치인 sass의  @extend를 활용하여 속성을 상속 받을 수 있다<br/>


하이픈 두 개(--)를 추가하여 사용

```css
.pagination__item {
    width: 50x;
    height: 50px;
}
.pagination__item--active {
    color: #fff;
}
.pagination__item--disabled {
    background-color: #bebebe;
}
```

클래스 명을 구체적이고 명료하게 작성하여 'html' 안에서도 읽기 쉬워야 하지만,<br />
클래스 명이 길어지는 경우가 많기 때문에 CSS 전처리기(Sass, Less, Stylus)를 활용하는 게 좋다.


 

#### 1-2-4. class명이 길다?
BEM의 class명은 구체적이고 명료하여 HTML안에서도 읽기 쉬워야 한다.
class명이 무엇을 나타내는지 분명하게 전달돼야 한다
 

#### 1-2-5. 그 외 +

파일 시스템
Class명의 정의 말고도 BEM은 파일 분리 시스템을 정의 하고 있다
https://en.bem.info/method/filesystem/
툴(Tool)
BEM 방법에 따라 파일 작업을 위한 툴
https://en.bem.info/tools/
 

 



​

​

### 1-3. OOCSS(Object Oriented CSS)

​
CSS를 **모듈 방식으로 작성**하여 `중복을 최소화`하며 `캡슐화`를 원칙으로 하는 방법론

```css
.header {
    background: #eb7b67;
}

.aside {
    background: #8888ee;
}

.default-width {
    width: 800px;
    padding: 10px;
    margin: 0;
}
```

.default-width 클래스와 같이 스타일을 정의해 두고

```html
<div class="header default-width"></div>
<div class="aside default-width"></div>
```

html 태그에 공통된 부분을 찾아 재활용하는 식으로 사용 <br/>

​

utility class 생성

​
```css
.white {color:#fff !important;}
.red {color:#fd454d !important;}
.blue {color:#2c8ff0 !important;}
.orange {color:#ff8000 !important;}
.green {color:#40a040 !important;}
.gray {color:#999 !important;}
.black {color:#000 !important;}
.tahoma {font-family:'tahoma' !important;}
.fb-like {width:100px;}

.mg0 {margin:0px !important}
.mg5 {margin:5px !important}
.mg10 {margin:10px !important}
.mg15 {margin:15px !important}
.mg20 {margin:20px !important}
.mg25 {margin:25px !important}
.mg30 {margin:30px !important}
.mg40 {margin:40px !important}
.mg50 {margin:50px !important}

.pd0 {padding:0px !important}
.pd5 {padding:5px !important}
.pd7 {padding:7px !important}
.pd10 {padding:10px !important}
.pd15 {padding:15px !important}
.pd20 {padding:20px !important}
.pd30 {padding:30px !important}
.pd40 {padding:40px !important}
.pd50 {padding:50px !important}
```

SMACSS의 base와 같은 느낌으로 공통 스타일을 작성하면 타이핑하는 코드 양을 줄임과 동시에 스타일을 쉽게 재사용 할 수 있다

​

​

CSS Pre-Processor 활용

```css

@each $color, $value in $colors {
	@include bg-variant(".bg-#{$color}", $value, $ignore-warning: true);
}

@each $color, $value in $theme-colors {
	@include bg-gradient-variant(".bg-gradient-#{$color}", $value, $ignore-warning: true);
}

@each $color, $value in $colors {
	@include bg-gradient-variant(".bg-gradient-#{$color}", $value, $ignore-warning: true);
}


// Background colors with transparency

@each $color, $value in $theme-colors {
    @include bg-translucent-variant(".bg-translucent-#{$color}", $value, $ignore-warning: true);
}

```

CSS Pre-Processor의 함수, 연산 등의 기능들을 활용하면 작성되는 코드량도 훨씬 줄어들게 되고, 여러 가지 효과들도 편하게 활용할 수 있다

​




## 2. 서버사이드 렌더링과 클라이언트 사이드 렌더링

> 이전에 정리한 내용 (https://dev-jeenie.github.io/cs/serversideRendering)

## 3. 함수형 프로그래밍과 객체지향 프로그래밍




<!-- ## 4. 추상 메서드, 추상 클래스, 인터페이스 -->

## 5. 데이터를 저장하는 방법

앱에서 나오는 데이터를 어디에 저장해야할까?

### 5-1. Redux

- 엄청 간단한 중앙 저장소
- RAM 같은 존재
- 앱 꺼지면 날아간다 (따라서 안전함)
- 데이터를 불러올 때 성능이 가장 좋다




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



<!-- 


리액트에서 페이지를 이동할 때는 <a> 태그의 href 대신 Link를 사용해야 한다.

<a> 태그의 href로 이동하면 상태 값을 잃고 속도가 저하된다.

리액트는 단일 url을 가지고 SPA(Single Page Application)으로 사이트를 표현하는 프레임워크로

하나의 HTML 페이지와 애플리케이션 실행에 필요한 JavaScript와 CSS 같은 모든 자산을 로드하는 애플리케이션이다.

해당 이유로 페이지를 새로 불러오게 되면 앱이 지니고 있는 상태가 초기화되고, 렌더링 된 컴포넌트도 모두 사라지고

새로 렌더링을 해야 한다.

상태 유지와 속도의 효율성을 위해 새로운 페이지를 불러오는 대신 업데이트하는 방식으로 구현해야 한다.

<a> 태그의 href는 페이지를 이동시킬 때 페이지를 새로 불러오게 된다. 따라서 상태 값이 유지되지 못하고 속도도 저하

된다.

반면에, Link 컴포넌트는 HTML5 History API를 사용하여 브라우저의 주소만 바꿀 뿐, 페이지를 새로 불러오지는 않는다.

따라서 리엑트에서는 Link 컴포넌트 사용을 권장한다.
출처: https://gomgomkim.tistory.com/9 [곰의 끄덕끄덕]
 -->


<!-- 
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
// 구글은 이런 refreshToken을 DB화해놓고 있어서, 그 중 하나에서 강제로 로그아웃시키기를 누르면 refreshToken을 없애버리는 방식인 것. -->




> 참고

https://velog.io/@huurray/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EA%B3%BC-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D

https://chlolisher.tistory.com/11