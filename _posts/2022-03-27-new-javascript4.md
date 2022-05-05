---
title: "Java script ES6💫 중급🔥 ✍️ (4) Class"
permalink: /es62/newJavascript4
tags:
  - [es62]

navigation: true
toc: true
toc_sticky: true

date: 2022-02-22
last_modified_at: 2022-03-27
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
console.log(jn1.getName()) // 재남
console.log(Person1.isPerson(jn1)) // true

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

  - `prototype`이 붙었으니 이건 prototype method.
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



아이패드 설명



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


- Class는 `생성자로서만` 동작한다.

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
클래스 선언문에 의해서 만든 변수는 `상수`이다.<br/>

클래스 C 내부에서 comstructor로 해당 클래스명을 다른 것으로 바꾸려는 시도는 constant variable 막히지만, <br/>
외부에서는 C라는 변수가 const가 아닌 let으로 선언된 것으로 보임.


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

function A { }
A.prototype.~

class A {
  a () { }
}

const a = new A()
a.a()
// undefined 실행해봤자 아무것도 없음


```

function으로 만든건 나중에 prototype.메소드로 할당할 수 있었지만,<br/>
class로 만들면 선언과 동시에 읽기전용으로 만들어버린다.<br/>


```js
A.prototype.a = {
  function () { console.log(1) }
}

a.a() // 1
```

class A 안에 있는 a 메소드는 A.prototype.a()와 같다.<br/>


```js
A.prototype = {}
// X
```

prototype을 통째로 바꿔치기하는 건 불가능하지만,<br/>
메소드 하나하나는 바꿔치기가 가능하다.





#### 3) '문'이 아닌 '값'이자 '식'이다.

그렇기 때문에 class 자체를 다른 함수의 인자로 넘길 수 있다.

```js
const jn = new class {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}('재님')
jn.sayName()
```

```js
const instanceGenerator = (className, ...params) => new className(...params)
class Person {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}

const jn = instanceGenerator(Person, '재나')
// === new Person('재나') 와 동일하다
const sh = instanceGenerator(class {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}, '성후')

jn.sayName()
// Person {name: '재나'}
sh.sayName()
// {name: '성후'}
// 익명클래스이기 때문에 앞에 클래스 네임이 붙지않음
```
className이라는 인자로 클래스를 전달받아서 새로운 인스턴스를 생성하는 방식이 가능함.




#### 4) 접근자

```js
class CustomHTMLElement {
  constructor (element) {
    this._element = element
  }
  get html () {
    return this._element.innerHTML
  }
  set html (value) {
    this._element.innerHTML = value
  }
}
console.log(Object.entries(CustomHTMLElement.prototype))
//  [] 열거대상에서 재외
console.log(Object.getOwnPropertyDescriptor(CustomHTMLElement.prototype, 'html'))
// {get: f, set: f,enumerable: false, configuarable: false}

```



#### 5) computed property names

```js
const method1 = 'sayName'
const fullNameGetter = 'fullname'
class Person {
  constructor (name) { this.name = name }
  [method1] () { console.log(this.name) }
  // 메소드를 대괄호 표기법으로 호출할 수 있다. 이름이 바뀌어도 호출이 가능하게끔
  get [fullNameGetter] () { return this.name + ' 정' }
}
const jn = new Person('재나')
jn.sayName()
// 재나
console.log(jn.fullname)
// 재나 정
```

#### 6) 제너레이터

```js

const obj = {
  *gene () {}
}

class A {
  *generator () {
    yield 1
    yield 2
  }
}
const a = new A() 
const iter = a.generator()
console.log(...iter)
```

객체에서 generator를 할당할 때와 동일하게 class에서도 할당 가능.



#### 7) Symbol.iterator

```js
class Products {
  constructor () {
    this.items = new Set()
  }
  addItem (name) {
    this.items.add(name)
  }
  [Symbol.iterator] () {
    // 방식은 객체에서와 동일. 대괄호 표기법으로 접근해서 Symbol.iterator를 만들어줌.
    let count = 0
	  const items = [...this.items]
    return {
      next () {
        return {
          done: count >= items.length,
          value: items[count++]
        }
      }
    }
  }
}
const a = new Products()
a.addItem('밥')
a.addItem('밥밥')
a.addItem('밥밥밥')

[...a]
// (3) ['밥','밥밥','밥밥밥']

const iter = a[Symbol.iterator()];

iter.next()
// { done: false, vale: '밥' }

iter.next()
// { done: false, vale: '밥밥' }

iter.next()
// { done: false, vale: '밥밥밥' }

iter.next()
// { done: true, vale: undefined }

```

```js
class Products {
  constructor () {
    this.items = new Set()
  }
  addItem (name) {
    this.items.add(name)
  }
  *[Symbol.iterator] () {
    // generator로 iterator를 만들면 간단.
    yield* this.items
  }
}
const prods = new Products()
prods.addItem('사과')
prods.addItem('배')
prods.addItem('포도')
for (let x of prods) {
  console.log(x)
}
```


### 8) 정적 메소드 (static method)

```js
class Person {
  static create (name) {
    return new this(name)
  }
  constructor (name) {
    this.name = name
  }
}
const jn = Person.create('재난')
console.log(jn)
```

class 본인을 위해서만 create 메소드를 호출할 수 있다.<br/>
따라서 인스턴스에서 접근이 불가능하다.<br/>


> 사실 접근은 가능하다. 하지만 의미가 없다<br/>

jn.__proto__.constructor.create()<br/>
이렇게 접근할 수는 있지만, 이때의 this는 `jn.__proto__.constructor`<br/>

jn.create()이렇게 접근이 되어야 this가 변경이 되면서 인스턴스가 호출을 할 수 있는데,<br/>

접근해봤자 this가 Person이 아니기때문에<br/>
class만이 접근이 가능하다.


## 15-3. 클래스 상속


사각형  =>  직사각형  =>  정사각형<br/>
(변4개)   (+각이90도)   (+변길이모두같음)<br/>

이 집단 구성의 원칙은 프로그래밍에서도 동일함.<br/>

하지만 사각형이 최상위일지, 정사각형이 최상위일지는 정하기 나름.


```js
class 사각형 {
  constructor (a, b, c, d) {}
}

class 직사각형 {
  constructor (가로, 세로) {}
}

class 정사각형 {
  constructor (가로) {}
}

```



### 15-3-1. 소개

```js
function Square (width) {
  this.width = width
}

Square.prototype.getArea = function () {
  return this.width * (this.height || this.width)
}

function Rectangle (width, height) {
  Square.call(this, width)
  this.height = height
}

function F() { }

F.prototype = Square.prototype
Rectangle.prototype = new F()
Rectangle.prototype.constructor = Rectangle

const square = Square(3)
const rect = new Rectangle(3, 4)

console.log(rect.getArea())
console.log(rect instanceof Rectangle)
console.log(rect instanceof Square)
```


이런 빈 함수를 만들어서 힘들게 처리했어야 했는데, <br/>

이제는 아래처럼 extends 만 쓰면 된다.


```js
class Square {
  constructor (width) {
    this.width = width
  }
  getArea () {
    return this.width * (this.height || this.width)
  }
}
class Rectangle extends Square {
  constructor (width, height) {
    super(width)
    //  prototype 체이닝 상에 다시 접근할 수 있는 접근자
    this.height = height
  }
}

const rect = new Rectangle(10, 20)
console.log(rect.getArea())
// 200
console.log(rect instanceof Rectangle)
console.log(rect instanceof Square)
```

> super <br/>
prototype 체이닝 상에 다시 접근할 수 있는 접근자. <br/>

super.gerArea(width) 이렇게 접근할 수 있지만, 지금은 그냥 함수로써 쓰였다. <br/>
함수로 쓰일때는 , `상위에 있는 class의 constructor를 직접 접근`함. <br/>
오직 constructor(생성자함수)안에서만 호출이 가능 <br/>

그래서 상위의 클래스의  constructor가 호출됨.

width가 넘어가고, 이때의 this는 Rectangle의 this <br/>
그래서 this.width = width가 되는 것. <br/>


```js
console.log(rect.getArea())
```
200이 나오는 이유? <br/>
넘겨준 값들에 의해서 Rectangle 클래스의 construtor가 호출이 된다. <br/>
그럼 10, 20 이 넘어간채로 super에 10을 넘김 <br/>

Squre의 constructor에 의해서 this.width가 10이 됨. <br/>
그 다음 height는 20. <br/>


Rectangle에는 메소드가 없다. 


rect.(__proto__) // Rectangle.prototype <br/>
rect.(__proto__).(__proto__) // Squre.prototype <br/>
rect.(__proto__).(__proto__).getArea() <br/>

(__proto__)는 생략가능! <br/>
그래서 결국 rect.getArea() 이렇게 사용이 가능한 것 <br/>




## 15-2. 상세

#### 1) 선언방식

```js
// 클래스 리터럴
class Person1 { }
console.log(Person1.name)

// 기명 클래스 표현식
const Person2 = class Person22 { }
console.log(Person2.name)

// 익명 클래스 표현식
let Person3 = class { }
console.log(Person3.name)
```

#### 2) 기존 방식과의 차이점

- let, const와 마찬가지로 TDZ가 존재하며, 블록스코프에 갇힌다.

```js
if(true) {
  class A { }
  const a = new A()
  if(true) {
    const b = new A()
    class A { }
  }
}
const c = new A()
```

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
```

- constructor를 제외한 모든 메소드는`new` 명령어로 호출할 수 없다.

```js
class A {
  constructor () { }
  a () { }
  static b () { }
}
const a = new A.prototype.constructor()
const b = new A.prototype.a()
const c = new A.prototype.b()

const d = new A()
const e = new d.constructor()
```

- 생성자로서만 동작한다.

```js
class A { }
A()
```

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

#### 3) '문'이 아닌 '식'이다.

```js
const jn = new class {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}('재님')
jn.sayName()
```

```js
const instanceGenerator = (className, ...params) => new className(...params)
class Person {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}

const jn = instanceGenerator(Person, '재나')
const sh = instanceGenerator(class {
  constructor (name) { this.name = name }
  sayName () { console.log(this.name) }
}, '성후')

jn.sayName()
sh.sayName()
```

#### 4) 접근자

```js
class CustomHTMLElement {
  constructor (element) {
    this._element = element
  }
  get html () {
    return this._element.innerHTML
  }
  set html (value) {
    this._element.innerHTML = value
  }
}
console.log(Object.entries(CustomHTMLElement.prototype))
console.log(Object.getOwnPropertyDescriptor(CustomHTMLElement.prototype, 'html'))
```

#### 5) computed property names

```js
const method1 = 'sayName'
const fullNameGetter = 'fullname'
class Person {
  constructor (name) { this.name = name }
  [method1] () { console.log(this.name) }
  get [fullNameGetter] () { return this.name + ' 정' }
}
const jn = new Person('재나')
jn.sayName()
console.log(jn.fullname)
```

#### 6) 제너레이터

```js
class A {
  *generator () {
    yield 1
    yield 2
  }
}
const a = new A()
const iter = a.generator()
console.log(...iter)
```

#### 7) Symbol.iterator

```js
class Products {
  constructor () {
    this.items = new Set()
  }
  addItem (name) {
    this.items.add(name)
  }
  [Symbol.iterator] () {
    let count = 0
	  const items = [...this.items]
    return {
      next () {
        return {
          done: count >= items.length,
          value: items[count++]
        }
      }
    }
  }
}
const prods = new Products()
prods.addItem('사과')
prods.addItem('배')
prods.addItem('포도')
for (let x of prods) {
  console.log(x)
}
```

```js
class Products {
  constructor () {
    this.items = new Set()
  }
  addItem (name) {
    this.items.add(name)
  }
  *[Symbol.iterator] () {
    yield* this.items
  }
}
const prods = new Products()
prods.addItem('사과')
prods.addItem('배')
prods.addItem('포도')
for (let x of prods) {
  console.log(x)
}
```

### 8) 정적 메소드 (static method)

```js
class Person {
  static create (name) {
    return new this(name)
  }
  constructor (name) {
    this.name = name
  }
}
const jn = Person.create('재난')
console.log(jn)
```

## 15-3. 클래스 상속

### 15-3-1. 소개

```js
function Square (width) {
  this.width = width
}

Square.prototype.getArea = function () {
  return this.width * (this.height || this.width)
}

function Rectangle (width, height) {
  Square.call(this, width)
  this.height = height
}

function F() { }

F.prototype = Square.prototype
Rectangle.prototype = new F()
Rectangle.prototype.constructor = Rectangle

const square = Square(3)
const rect = new Rectangle(3, 4)

console.log(rect.getArea())
console.log(rect instanceof Rectangle)
console.log(rect instanceof Square)
```

```js
class Square {
  constructor (width) {
    this.width = width
  }
  getArea () {
    return this.width * (this.height || this.width)
  }
}
class Rectangle extends Square {
  constructor (width, height) {
    super(width)
    this.height = height
  }
}

const rect = new Rectangle(3, 4)
console.log(rect.getArea())
console.log(rect instanceof Rectangle)
console.log(rect instanceof Square)
```

### 15-3-2. 상세

1. `class [서브클래스명] extends [수퍼클래스명] { [서브클래스 본문] }`

- 반드시 변수만 와야 하는 것이 아니라, 클래스 식이 와도 된다.
```js
class Employee extends class Person {
  constructor (name) { this.name = name }
} {
  constructor (name, position) {
    super(name)
    this.position = position
  }
}
const jn = new Employee('잰남', 'worker')
```

```js
class Employee extends class {
  constructor (name) { this.name = name }
} {
  constructor (name, position) {
     (name)
    this.position = position
  }
}
const jn = new Employee('잰남', 'worker')
console.log(jn.__proto__.__proto__.constructor.name)
```

- 함수도 상속 가능.

```js
function Person (name) { this.name = name }
class Employee extends Person {
  constructor (name, position) {
    super(name)
    this.position = position
  }
}
const jn = new Employee('잰남', 'worker')
```

```js
class Employee extends function (name) { this.name = name } {
  constructor (name, position) {
    super(name)
    this.position = position
  }
}
const jn = new Employee('잰남', 'worker')
```

- 내장 타입 상속 가능

```js
class NewArray extends Array {
  toString () {
    return `[${super.toString()}]`
  }
}
const arr = new NewArray(1, 2, 3)
console.log(arr)
console.log(arr.toString())
```

2. super (내부키워드로써, 허용된 동작 외엔 활용 불가)

- (1) constructor 내부에서
  - 수퍼클래스의 constructor를 호출하는 함수 개념.
  - 서브클래스의 constructor 내부에서 `this`에 접근하려 할 때는 **가장 먼저** super함수를 호출해야만 한다.
  - 서브클래스에서 constructor를 사용하지 않는다면 무관. (이 경우 상위클래스의 constructor만 실행된다.)거나, 내부에서 `this`에 접근하지 않는다면 무관.

- (2) - 메소드 내부에서
  - 수퍼클래스의 프로토타입 객체 개념.
  - 메소드 오버라이드 또는 상위 메소드 호출 목적으로 활용.

```js
class Rectangle {
  constructor (width, height) {
    this.width = width
    this.height = height
  }
  getArea () {
    return this.width * this.height
  }
}
class Square extends Rectangle {
  constructor (width) {
    console.log(super)
    super(width, width)
  }
  getArea () {
    console.log('get area of square.')
    console.dir(super)
    return super.getArea()
  }
}
const square = new Square(3)
console.log(square.getArea())
```

3. `new.target`을 활용한 abstract class 흉내

```js
class Shape {
  constructor () {
    if(new.target === Shape) {
      throw new Error('이 클래스는 직접 인스턴스화할 수 없는 추상클래스입니다.')
    }
  }
  getSize () {}
}
class Rectangle extends Shape {
  constructor (width, height) {
    super()
    this.width = width
    this.height = height
  }
  getSize () {
    return this.width * this.height
  }
}
const s = new Shape()
const r = new Rectangle(4, 5)
```
