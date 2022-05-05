---
title: "Java script ES6💫 제대로 알아보기! ✍️ (9) Function"
permalink: /js2/javascriptEs69
tags:
  - [es6]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-18
last_modified_at: 2022-01-18
---

![]()

## 1. name property of function




```js
function a () { }
console.log(a.name)

const b = function () { }
console.log(b.name)
```

익명함수로 name을 할당하면 변수명이 원래는 안들어갔고, 브라우저 편의상 변수명을 할당했었는데<br/>
이젠 규칙으로 변수명을 할당하게 됨!<br/>

```js

const c = function cc () { }
console.log(c.name)
```
그럼 기명함수 표현식의 name은?<br/>
기명된 그 이름이 들어간다 (c가 아닌 cc)

```js
const d = () => {}
console.log(d.name)
```
그럼 arrow function은?<br/>
익명함수와 동일하게 name property에 해당 변수의 이름이 들어간다<br/>

```js
const e = {
  om1: function () {},
  om2 () {},
  om3: () => {}
}
console.log(e.om1.name, e.om2.name, e.om3.name)
// om1, om2, om3
```


```js
class F {
  static method1 () {}
  method2 () {}
}

function G () { } // 생성자 함수로 사용
  G.method1 = function () {}
  G.prototype.method2 = function () {}
}

const f = new F()
console.log(F.method1.name, f.method2.name)
const g = new G()
console.log(G.method1.name, g.method2.name)
```

함수 G는 생성자 함수이지만,<br/>생성자 함수는 원래 함수.<br/>함수는 원래 1급 객체.<br/>
객체는 property를 할당할 수 있다.<br/>
=> 객체 자체한테 method1이라는 property를 할당한 것.<br/>

이것을 가지고 name을 출력하라고 한 것.<br/>

(이해못함)



```js

const f = function (a,b) {return a + b;}
// 해당 함수를 new function으로 바꾸려면
const g = new Function('a,b','return a + b')

g(1,2) // 3
f(1,2) // 3
```
new Function으로 만드는 애는 익명함수를 만든다.<br/>
단, 다른 익명함수들과는 달리 **해당 변수의 이름을 넣는게 아니라**, <br/>
`new Function`으로 만든 `인스턴스`를 **g에다 할당**하는 방식이기 때문에<br/>
그때에 익명함수인 것을 표시하기 위해서 name에 `annoymous`가 들어간다


```js
function a () { }
const b = function () { }

a.call({ }) // undefined
a.apply({ }) // undefined

const b = a.bind({a: 1})
console.log(h.name)
```

> call / apply<br/>
this 및 인자들을 넘김과 동시에 바로 실행하는 것.<br/>
a.call({ })<br/>
this를 {}로 해서 a를 호출하라는 뜻<br/>
apply와 마찬가지로 this를 첫번째 인자로 받음<br/>


> bind

내가 넘기고 싶은 인자를 바탕으로 `새로운 함수`를 만든다.<br/>
bind를 붙이면 바로 실행하지않고, 그 결과를 `해당 변수에 담아라`가 됨.<br/>
 
그래서 b를 실행하면, b의 this는 {a: 1}이 됨.<br/>


bind를 사용했을 경우에 name은 앞에 'bound'가 붙어서 들어감.

<!-- ```js
const person = {
  _name: '재남',
  get name () {
    return this._name
  },
  set name (v) {
    this._name = v
  }
}
const descriptor = Object.getOwnPropertyDescriptor(person, 'name')
console.log(descriptor.get.name)
console.log(descriptor.set.name)
```
 -->


## 2. new.target


[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target]()

```js
function Person (name) {
  if (this instanceof Person) {
    this.name = name
  } else {
    throw new Error('new 연산자를 사용하세요.')
  }
}
var p1 = new Person('재남')
console.log(p1)

var p2 = Person('성훈')
console.log(p2)

var p3 = Person.call({}, '곰')
console.log(p3)

var p4 = Person.call(p1, '곰')
console.log(p4)
```

```js
function Person (name) {
  console.dir(new.target)
  if (new.target !== undefined) {
    this.name = name
  } else {
    throw new Error('new 연산자를 사용하세요.')
  }
}

const p1 = new Person('재남')
console.log(p1)

const p2 = Person('성훈')
console.log(p2)

const p3 = Person.call({}, '곰')
console.log(p3)

const p4 = Person.call(p1, '곰')
console.log(p4)
```

```js
function Person (name) {
  const af = n => {
    this.name = n
    console.log(new.target)
  }
  af(name)
}
const p1 = new Person('재남')
const p2 = Person('성훈')
```

```js
function Person (name) {
  this.name = name
}
function Android (name) {
  Person.call(this, name)
}
const p1 = new Android('재남봇')
```

```js
function Person (name) {
  console.log(new.target)
  if (new.target === Person) {
    this.name = name
  } else {
    throw new Error('Person 생성자함수를 new로 호출해야 해요!')
  }
}
function Android (name) {
  Person.call(this, name)
}
const p2 = new Android('재남봇')
```









## 3. 블록 스코프 내부에서 함수 선언 / 호이스팅

```js
if (true) {
  a()
  function a () { console.log(true) }
}
a()
```

```js
a()
if (true) {
  a()
  function a () { console.log(true) }
}
```

```js
if (true) {
  a()
  function a () { console.log(true) }
  if (true) {
    a()
    function a () { console.log(false) }
  }
}
a()
```

```js
'use strict'
if (true) {
  a()
  function a () { console.log(true) }
  if (true) {
    a()
    function a () { console.log(false) }
  }
}
a()
```

```js
'use strict'
if (true) {
  function a () { console.log(true) }
  a()
}
a()
```

