---
title: "Java script ES6💫 중급🔥 ✍️ (4) Class"
permalink: /cs/newJavascript4
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-02-22
last_modified_at: 2022-02-22
---

![]()



# 1. Class


## 1-1. Class 소개


```js
function Person1 (name) {
  this.name = name
}
```

Person1 함수는 생성자 함수.<br/>
1) 대문자이고 2) this를 사용했다는 특징이 있음<br/>

하지만 생성자 함수는 생성자 함수로도 쓸 수 있고, 그냥 함수로도 쓸 수 있다.<br/>

***잠깐 짚고 넘어가는 `prototype method`와 `static method`***

```js
function Person1 (name) {
  this.name = name
}
Person1.prototype.getName = function () { // prototype method
  return this.name
}

Person1.isPerson = function (obj) {  // static method
  return obj instanceof this
}

const jn1 = new Person1('재남')
console.log(jn1.getName())
console.log(Person1.isPerson(jn1))

// jn1은 

person.getName();
// O. Person1로 만든 인스턴스는 getName을 호출가능
Person1.getName();
// X. 생성자함수 자체는 getName을 호출할 수 없다.

Person1.isPerson();
// O. 생성자함수 자체는 isPerson 호출가능
person.isPerson();
// X. Person1로 만든 인스턴스에서 isPerson를 호출할 수 없다 

```
- getName
> Person1.prototype.getName<br/>

  - prototype이 붙었으니 이건 prototype method.
  - 생성자함수는 prototype method를 바로 호출할 수 없다.

- isPerson
> Person1.isPerson<br/>

  - prototype이 없으니 이건 static method.
  - 생성자함수 본인이 직접 가지고 있으니 호출가능.
  - 하지만 생성자 함수로 생성한 instance는 호출 불가능!


> static method란?<br/>
생성자 함수 본인이 직접 가지고 있는 method.(정적 메소드)


- es5의 방식
```js
function Person1 (name) {
  this.name = name
}
Person1.prototype.getName = function () {
  return this.name
}
Person1.isPerson = function (obj) {
  return obj instanceof this
}
const jn1 = new Person1('재남')
console.log(jn1.getName())
console.log(Person1.isPerson(jn1))
```

- es6의 방식
```js
class Person2 {
  constructor (name) { this.name = name }
  getName () { return this.name }
  static isPerson (obj) { return obj instanceof this }
}
const jn2 = new Person2('재남2')
console.log(jn2.getName())
console.log(Person2.isPerson(jn2))
```

생성자 함수의 내용이 constructor로 들어왔따<br/>
getName: function () { return this.name }<br/>
이렇게 객체에서 선언하듯이는 쓸 수 없음.<br/>

` , `로 구분하지도 않았다. ` : `, `function`도 **사용 불가**<br/>
class 내부영역은 method들만 정의해둘 수 있는 영역<br/>

> method이름 (인자) { 내용 }<br/>
class 내부에서는 오직 이렇게만 쓸 수 있다.<br/>





```js
Slide.prototype.triggerClick = function () {}
```
너는 내가 허락한 이것 이외에는 scope로 감싸져있는 내부변수들을 건드리지 못할거야.<br/>
(외부와의 소통수단 하나를 열어준 것)<br/>

너는 오직 triggerClick으로만 나와 소통할 수 있어.<br/>

이것이 객체지향 프로그래밍의 기본원칙







## 1-2. 상세

#### 1) 선언방식

```js
// 클래스 리터럴
class Person1 { }
console.log(Person1.name)
// 결과 : Person1
// Person1이 바로 할당됨

// 기명 클래스 표현식
const Person2 = class Person22 { }
console.log(Person2.name)
// a.name => "aa"
// Person2.name => "Person22"

// 익명 클래스 표현식
let Person3 = class { }
console.log(Person3.name)
```
클래스도 보기에는 스코프때문에 새로운 문이 등장한 것 같지만, <br/>
문이 아닌 식이면서 값이다.

> 함수의 이용 목적에 따른 정의<br/>

함수선언문이라고 부르지만, 목적에 따라 식, 값, 문이 될 수 있다.

```js
function a () { }
a() // 호출 목적 : 함수 a는 식이다

const a = function () { }
// 할당 목적 : 함수 a는 값이다
```

어딘가에 **`할당할 수 있다`는 목적**이라면 `값`이자 `식`! **문이 X**



#### 2) 기존 방식과의 차이점

- let, const와 마찬가지로 `TDZ`가 존재하며, `블록스코프`에 갇힌다.

```js
if(true) {
  class A { }
  const a = new A()
  if(true) {
    // A라는 변수만 호이스팅 되고 Class 값 할당되지않음
    const b = new A() // TDZ
    class A { }
  }
}
const c = new A() // referenceError
```

호이스팅을 하지만, **함수선언문과는 달리** TDZ에 걸려 변수만 호이스팅한다.

- class 내부는 strict mode가 강제된다.

- 모든 메소드를 열거할 수 없다. (콘솔에서 색상이 흐리게 표기됨)

```js
class A {
  a () { }
  b () { }
  static c () { }
}

for (let p in A.prototype) {
  console.log(p)
}

A.prototype.a = function () { }
A.prototype.d = function () { }

for (let p in A.prototype) {
  console.log(p)
}

// d: ƒ () d만 색이 진하고 나머지는 흐림
// a: ƒ ()
// b: ƒ b()
// constructor: class A
// [[Prototype]]: Object
```

- constructor를 제외한 모든 메소드는`new` 명령어로 호출할 수 없다.

```js
class A {
  constructor () { }
  a () { }
  static b () { }
}

A.prototype.constructor === A // true

const a = new A.prototype.constructor()
// 가능
const b = new A.prototype.a()
// TypeError: A.prototype.a() is not a constructor
const c = new A.prototype.b()
// TypeError: A.prototype.b() is not a constructor

const d = new A()
const e = new d.constructor()
```

  class A의 메소드 `a`와 `b`는 `prototype이 없다`.<br/>
  A라는 Class 자체에는 prototype 이 있다.(`constructor`가 자기 자신과 같으니까)<br/>
  그래서 const a = **new A()**는 `가능`한 것이고<br/>
  그래서 const a = **new A.prototype.a()**는 `불가능`한 것.<br/>

```js
function A () {}
A.prototype.a = function () {}
const aa = new A.prototype.a();
```
함수 자체를 a라는 property에 할당하는 거니까,<br/>
이 함수 선언문이 가지고 있는 특성을 고스란히 가지고있음<br/>
그래서 **원래는 이렇게 `함수를 생성자함수로도 사용이 가능`**했다.<br/>
(함수로도 쓸 수 있고 생성자 함수로도 쓸 수 있던 기존 방식)


- 생성자로서만 동작한다.

```js
class A { }
A()
// Class construction A cannot be invoked without 'new'
```
함수로도 쓸 수 있고 생성자 함수로도 쓸 수 있던 기존 방식과 달리,<br/>
class는 반드시 생성자로써만 동작한다.



- 클래스 내부에서 클래스명 수정

```js
let A = class {
  constructor () { A = 'A' }
}
const a = new A()
console.log(A)

const B = class {
  constructor () { B = 'B' }
}
const b = new B()

class C {
  constructor () { C = 'C' }
}
const c = new C()
```



- 클래스 외부에서 클래스명 수정

```js
let A = class { }
A = 10;             // ok

const B = class { }
B = 10;             // Uncaught Type Error: Assignment to constant variable

class C { }
C = 10;             // ok  
```

- 외부에서 prototype을 다른 객체로 덮어씌울 수 없다 (읽기전용)

```js
class A {
  a () { }
}
A.prototype = {
  a () { console.log(1) }
}
const a = new A()
a.a()
```
