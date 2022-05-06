---
published: true
title: "✨ 자바스크립트 핵심 개념(ES5 Core Concept)"
permalink: /cs/defaultKnowledge5
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-05-06
last_modified_at: 2022-05-06
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

# 자바스크립트 핵심 개념

이전에도 정리한 글이 있지만, 다시 한번 정리해본다.<br/>
> 이전에 정리해둔 글 (https://dev-jeenie.github.io/tags/#js1)

## 1. 데이터 타입(data-type)

> 이전에 정리해둔 글 참고 (https://dev-jeenie.github.io/js1/JavascriptDataTypes)


기본형은 값을 그대로 할당하고, 참조형은 값이 저장된 주소값을 할당(참조)한다.




### 1-1. 기본형

기본형(Primitive Type)
Number
String
Boolean
null
undefined
(es6에선 symbol 추가)

### 1-2. 참조형

참조형(Reference Type)
Object
Array
Function
RegExp
(es6에선 map, set 등 추가)


## 2. function
> 이전에 정리해둔 글 참고 (https://dev-jeenie.github.io/es6/javascriptEs69)



### 2-1. 호이스팅

1. 호이스팅 (hoisting)
 - 사전적의미는 '끌어올리다' 라는 뜻. 변수 선언과 함수 선언을 끌어올린다.
 - 자바스크립트 엔진은 프로그램 실행 전 코드 전반에 걸쳐 선언만을 끌어올린다.

### 2-2. 함수선언문과 표현식

2. 함수선언문과 함수표현식 (function declaration & function expression)
 - 함수 선언문(function declaration)
 - 기명 함수 표현식(named function expression)
 - (익명) 함수 표현식((unnamed/annonymous)function expression)
     
 - 호이스팅에서 함수 선언문과 함수 표현식의 차이: 선언문은 함수 전체가 호이스팅되고, 표현식은 함수가 할당된 변수만이 호이스팅된다.
 - 협업에선 호이스팅이 어떻게 되는지 여부가 굉장히 중요하다. (작업사항 충돌 우려)
 - 더글라스 크락포드는 함수 선언식이 아닌 '함수 표현식'을 사용할 것을 강력히 권장한다.
### 2-3. 스코프와 실행 컨텍스트
3. 함수 스코프, 실행 컨텍스트 (function scope, execution context)
 - 스코프(scope) : 변수의 유효범위
 - 실행 컨텍스트(execution context) : 실행되는 코드덩어리 (추상적 개념)
      
 - 둘의 가장 큰 차이는 발생 시점
 - >> 스코프는 함수가 '정의' 될 때 결정된다.
 - >> 실행 컨텍스트는 함수가 '실행' 될 때 생성된다.

 - 실행 컨텍스트에는 호이스팅 후의 함수 본문 내용과 this가 무엇인지에 대한 정보가 담긴다.
 - 즉, 실행 컨텍스트는 사용자가 함수를 호출했을 때에 내부적으로 해당 함수를 실행하기 위해 불러 모은 집합체.

### 2-4. 메소드
4. 메소드 (method)
 - 객체 안에 선언된 함수.
 - 함수와 메소드의 차이점은, 간단히 생각하면 앞에 '.' 이 있느냐 없느냐의 차이이다.
 - '.'이 있냐 없냐로 this가 달라진다.
### 2-5. 콜백

콜백함수 (Callback Function)
 - Something will call this function back
 - 제어권을 넘겨주는 것(맡기는 것)
 - A가 콜백 함수를 받는 함수, B가 콜백 함수라고 할 때,
    - 다른 함수의 매개변수로 콜백함수를 전달하면, A가 B의 제어권을 갖게 된다.
    - 특별한 요청(bind)이 없는 한 A에 미리 정해진 방식에 따라 B를 호출한다.
    - 미리 정해진 방식이란 this에 무엇을 바인딩할지, 매개변수에는 어떤 값들을 지정할지, 어떤 타이밍에 콜백을 호출할지 등이다.
 - 주의할 점은, 콜백함수는 '메소드'가 아니고 '함수'라는 것.


## 3. this
> 이전에 정리해둔 글 참고 (https://dev-jeenie.github.io/es6/javascriptEs61#4-this)

### 3-1. 호출 위치와 방식에 따른 this

전역공간에서
 - 전역객체를 가리킴
    - 브라우저 콘솔에선 'Window 객체'
    - node.js 에선 'grobal 객체'
 - Window, global 둘 모두 ECMA Script 에서 정의한 구현체
함수 내부에서
 - 전역객체를 가리킴
메소드 호출시
 - 메소드 호출 주체 (메소드 바로 앞)
 - 즉, 메소드명 바로 앞에 있는 마지막 점 '.' 까지가 주체.
       
 - 여기서, '함수는 (전역 객체의) 메소드다' 라고 생각하는게 편한데, 
 - 옳지는 않지만 이렇게 생각한다면 앞에 뭐가 있다면 걔가 this고 없다면 전역객체가 this다.
callback에서
 - 기본적으로는 함수 내부의 this와 동일
 - 제어권을 가진 함수가 callback의 this를 명시한 경우에 그에 따르게 된다. (addEventListener()의 this는 dom)
 - 개발자가 this를 바인딩한 채로 callback을 넘기면 그에 따른다.(thisArg)
생성자함수에서
 - 인스턴스를 가리킨다.



## 4. 클로저(closer)


### 4-1. 클로저란?

### 4-2. 클로저 사용 예제







## 5. 프로토타입 (prototype)
> 이전에 정리해둔 글 참고 (https://dev-jeenie.github.io/es62/newJavascript4) <br/>
(https://dev-jeenie.github.io/es6/javascriptEs67#1-2-concise-methods-%EA%B0%84%EA%B2%B0%ED%95%9C-%EB%A9%94%EC%86%8C%EB%93%9C)

### 5-1. 프로토타입이란?



- 정의
 1. 생성자 함수(constructor)가 있을때,
 2. new 연산자를 써서 instance 를 만들면,
 3. 생성자 함수의 prototype 이라고 하는 프로퍼티가
 4. instance 의 __proto__ 라고 하는 프로퍼티에 전달된다. => 생성자 함수의 prototype과 instance 의 __proto__ 라고 하는 프로퍼티는 같은 객체를 참조하게 된다.****
 5. __proto__ 는 내부 프로퍼티에 접근할 때 이 단어를 생략할 수 있다.


객체는 프로퍼티를 가질 수 있는데 prototype이라는 프로퍼티는 그 용도가 약속되어 있는 특수한 프로퍼티다. prototype에 저장된 속성들은 생성자를 통해서 객체가 만들어질 때 그 객체에 연결된다.


- 생성자의 프로토타입에 접근하는 법
 - [CONSTRUCTOR].prototype
 - [instance].__proto__
 - [instance]
 - (Object.getPrototypeOf([instance]))

- 생성자 함수에 접근하는 법
 - [CONSTRUCTOR]
 - [CONSTRUCTOR].prototype.constructor
 - (Object.getPrototypeOf([instance])).constructor
 - [instance].__proto__.constructor
 - [instance].constructor

### 5-2. 프로토타입 체이닝


프로토타입 체이닝
 - 모든 데이터 타입의 생성자 함수의 프로토타입에 연결된 Object.prototype에는, 자바스크립트 전체를 통괄하는 공통된 프로퍼티들이 정의되어 있고 이는 모든 데이터 타입이 프로토타입 체이닝에 의해서 접근할 수 있다.
 - 하지만 그렇기 때문에 객체의 프로토타입에는 객체에만 적용되는 프로토타입을 정의해둘 수 없다. 객체의 프로토타입에 특정 프로퍼티를 추가하면 바로 위 항목과 같은 이유로 모든 데이터 타입에 적용되어버리기 때문이다.
 - 그래서 어쩔 수 없이, 객체에만 적용되는 프로퍼티는 객체 생성자 함수에 직접 메서드를 정의할 수 밖에 없었다. 유독 객체 리터럴에서 대문자 Object로 시작하는 매서드가 많이 보이는 이유이다. (ex - assign(), keys(), create() 등등)



<img src="/assets/images/prototype.png" /><br/>


<img src="/assets/images/prototype_1.png" /><br/>



## 6. 클래스 (Class)
> 이전에 정리해둔 글 참고 (https://dev-jeenie.github.io/es62/newJavascript4)


### 6-1. 클래스란?
 - 사전적 의미로는 계급, 집단, 집합
 - 동일한 속성을 가진 요소들을 한데 묶은 명세

### 6-2. 클래스 사용목적
 - 접근 권한 제어
 - 지역변수 보호
 - 데이터 보존 및 활용

### 6-3. 클래스 사용법
 - 1. 함수에서 지역변수 및 내부함수 등을 생성한다.
 - 2. 외부에 노출시키고자 하는 멤버들로 구성된 객체를 return 한다.
 - >> return한 객체에 포함되지 않은 멤버들은 private하다. 
 - >> return한 객체에 포함된 멤버들은 public하다.

### 6-4. 인스턴스란?
 - 해당 클래스의 속성을 가진 구체적인 객체


### 6-5. 클래스의 static 메소드와 static 프로퍼티, prototype 메소드

 - static 메소드: 생성자 함수 안에 정의된 메소드 (Array.from(), Array.isArray() 등)
 - static 프로퍼티: 생성자 함수 안에 정의된 프로퍼티 (Array.length, Array.name 등)

 - 😤 static 요소들은 Array 생성자를 new 연산자 없이 일급객체로서 생성할 때에만 의미가 있다!!
### 6-6. 클래스의 prototype 메소드
 - (prototype) 메소드: prototype 안에 정의된 메소드들. 일반적으로 prototype을 떼고 그냥 메소드라고 부르는 경우가 많다.
 
 - 😤 인스턴스와 (prototype) 메소드는 __proto__ 로 연결되어 있고,      
    이 __proto는 생략 가능하기 때문에 instance에서 다이렉트로 (prototype) 메소드 안에 접근할 수 있는데,<br/>
    생성자 함수 내부에 있는 프로퍼티나 메소드는 다이렉트로 접근이 불가능하다.    <br/>
    (방법이 없는 건 아니지만 정상적인 동작을 기대하긴 힘들다.)






