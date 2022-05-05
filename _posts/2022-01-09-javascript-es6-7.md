---
title: "Java script ES6💫 제대로 알아보기! ✍️ (7) enhanced object functionallities"
permalink: /js2/javascriptEs67
tags:
  - [es6]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-15
last_modified_at: 2022-01-15
---

![]()

## 1. enhanced object functionalities(객체의 향상된 기능들)



## 1-1. shorthand properties (프로퍼티 축약)

```js
var x = 10
var y = 20
var obj = {
  x: x,
  y: y
}
```

```js
const x = 10
const y = 20
const obj = {
  x,
  y
}
```
똑같은 property key와, 거기에 미리 선언한 변수명을 할당하고자 할 때<br/>

property `key`와 **value에 할당**하고자 하는 `변수명`이 **동일**할 경우에 `value 생략 가능`하다<br/>

### 1-1-1. 활용

- 1)

```js
const convertExtension = function (fullFileName) {
  const fullFileNameArr = fullFileName.split('.')
  const filename = fullFileNameArr[0]
  const ext = fullFileNameArr[1] && fullFileNameArr[1] === 'png' ? 'jpg' : 'gif'
  return {
    filename,
    ext
  }
}
convertExtension('abc.png')
```
이렇게 애초에 **변수명**을 `해당 키값으로` 만든다.

- 2)

```js
const {
  name,
  age
} = {
  name: '재남',
  age: 30
}
console.log(name, age)
```

객체의 형태를 뒤와 매칭시켜서 동일하게 매칭된 애들마다 해당 변수를 할당한다.

```js
const {
  name: name,
  age: age
} = {
  name: '재남', // name에 재남 할당
  age: 30 /// age에 30 할당
}
console.log(name, age)
```


## 1-2. concise methods (간결한 메소드)

### 1-2-1. 메소드를 축약 가능

```js
var obj = {
  name: 'foo',
  getNameEs6 () { return this.name }
  getNameEs5: function () { return this.name }
}
```
- 차이점
  - getNameEs5
    - 기존에는 **실행이 종료된 이후**에 접근하려고 해도 `반환값이 null`인 채로 `접근이 가능`했다.
    - **prototype** `있음`
  - getNameEs6
    - 기존에는 **실행이 종료된 이후**에 접근하려고 해도 `반환값이 null`인 채로 `접근이 가능`했다. 에러를 명시적으로 띄워줘서 디버깅을 용이하게 함
    - agruments에 접근할 수 없는 환경의 경우에는 에러를 띄워준다.
    - **prototype** `없음`

기존의 함수는 **함수**로써, **생성자 함수**로써 두 가지로 쓸 수 있었음.<br/>
이때 생성자 함수의 역할은, 얘가 들고있던 prototype property의 내용을 연결해주는 역할<br/>

새로운 `메소드 축약형`에서는 하려던 일, 본연의 일만 할 수 있게 됨! <br/>
=> 함수가 가벼워짐.<br/>

prototype 객체가 사라졌기 때문에 생성자 함수로 **쓸 수 없고**, <br/>
오로지 **함수 본연의 기능만** 할 수 있다<br/>
그래서 더 빨라짐.<br/>

=> **결론**<br/>

`method`로써 호출할 때는 **method** 본연의 기능<br/>
`콜백함수`로 넘겼을 때는 **함수** 본연의 기능<br/>

#### 1-2-1-1. 상세

- 1) super 명령어로 상위 클래스에 접근 가능

- **super** Class (상위클래스)
- **sub** Class (하위클래스)

```js
const Person = {
  greeting: function () { return 'hello' }
}
const friend = {
  greeting: function () {
    return 'hi, ' + super.greeting()
  }
}
Object.setPrototypeOf(friend, Person)
friend.greeting()
```
`setPrototypeOf(instance로, 생성자함수로)`

object friend의 **prototype**을 Person으로 지정해라.<br/>

=> 결과<br/>
friend의 prototype 상의 생성자함수가 person이 됨.<br/>
`super`를 사용하면,<br/>
자신의 prototype 체이닝 상에서 `상위에 있는 method를 호출`할 수 있다.

```js
friend.greeting();
// "hi,Hello"
friend._proto_.greeting();
// "hello"

```

- 2) prototype property가 없어서 생성자 함수로 사용 불가능

## 1-2. computed property name (계산된 프로퍼티명)

- 1) 대괄호 표기법
  - 객체 리터럴 `선언 시` 프로퍼티 키 값에 대괄호 표기로 접근 가능
  - 대괄호 내에서는 `값` 또는 `식`을 넣어 조합할 수 있음(문은 X)

```js
var className = ' Class'
var obj = {}

obj.'ab cd' = 'AB CD'
```

. 뒤엔 문자열이 올 수 없다.<br/>
**객체 밖**에서 `불가능`

```js

obj = {
  'ab cd': 'AB CD'
}

obj['ab cd'] = 'AB CD'
```
이렇게 **객체 안**에 바로 넣으면 `가능`

```js

obj['A' + className] = 'A급'

```

`가능`

```js

var obj = {
  'A' + className: 'A급'
}
```

`불가능`<br/>

```js
const obj2 = {
  'ab cd':
  ['A' + className]: 'A급'
}
```
되게 하려면 이렇게 `대괄호 표기법`을 사용.<br/>

기존의 대괄호 표기법은,<br/>

```js
const obj2 = {}
obj2['A' + className]: 'A급'
```

객체를 선언하는 순간 말고, 객체가 **이미 선언되어 있을 때**!<br/>
그 객체 안에 property **하나씩 추가**할 때는 가능했지만,
<br/>
내부에 변수명을 조합하는게 불가능했다.<br/>

그런데 이제는 선언하는 순간에 `변수명을 조합`하는 게 가능!<br/>


```js
let suffix = ' name'
let iu = {
  ['last' + suffix]: '이',
  ['first' + suffix]: '지은'
}
console.log(iu)
/// 결과 {last name: '이', first name: '지은'}

```
 
## 1-3. own property enumeration order (고정된 프로퍼티 열거 순서)

```js
const obj1 = {
  c: 1,
  2: 2,
  a: 3,
  0: 4,
  b: 5,
  1: 6
}
const keys1 = []
for (const key in obj1) {
  keys1.push(key)
}
console.log(keys1)
console.log(Object.keys(obj1))
console.log(Object.getOwnPropertyNames(obj1))

// 결과는 모두 ['0', '1', '2', 'c', 'a', 'b']
```
`숫자`는 **숫자 순서**, `문자`는 **입력된 순서**



```js

const obj2 = {
  [Symbol('2')]: true,
  '02': true,
  '10': true,
  '01': true,
  '2': true,
  [Symbol('1')]: true
}
const keys2= []
for(const key in obj2) {
  keys2.push(key)
}
console.log(keys2)

// 결과 ['2', '10', '02', '01']

```

숫자라면 숫자순서대로 나와야하고, 문자라면 입력순서대로 나와야하는데 왜?<br/>
- 숫자인데 첫글자가 0이 아닌 경우 => 숫자
- 숫자인데 첫글자가 0인 경우 => 문자

그래서 2,10은 숫자라서 순서대로 먼저 나오고,<br/>
01, 02는 문자라 입력순서대로 나온 것.<br/>






```js

const obj3 = Object.assign({}, obj1, obj2)
//아까의 obj1, obj2를 병합해서 obj3에 넣음

const keys3= []
for(const key in obj3) {
  keys3.push(key)
}
console.log(keys3)
console.log(Object.keys(obj3))
console.log(Object.getOwnPropertyNames(obj3))
// ['0', '1', '2', '10', 'c', 'a', 'b', '02', '01']
```
일반적으로 출력하면 Symbol은 무시됨.<br/>
Symbol은 **열거 대상에서 제외**됨

```js
console.log(obj3)

// 결과 {0: 4, 1: 6, 2: true, 10: true, c: 1, a: 3, b: 5, 02: true, 01: true, …}0: 401: true1: 602: true2: true10: truea: 3b: 5c: 1Symbol(1): trueSymbol(2): true[[Prototype]]: Object
```

그냥 콘솔창에서 보려고 할 때는 `순서를 보장하지 않는다`.<br/>
그런데 프로그래밍적으로 이 값을 쓰려고 할 때, 열거한 값을 가지고 처리하려고 할 때는 순서를 보장하겠다는 것.<br/>
이 때에는 열거 대상이 아니니 Symbol도 출력된다.<br/>

하지만 굳이 symbol도 열거를 해야겠다면?

```js

console.log(Reflect.ownKeys(obj3))
// ['0', '1', '2', '10', 'c', 'a', 'b', '02', '01', Symbol(2), Symbol(1)]

```

=> **결론**

| 객체의 열거 순서 |
| -- | -- | -- |
| 1. 숫자(asc) | 2. 문자(입력순서) | 3. Symbol |


- 1) 열거순서는 다음 규칙을 따른다.

- **number & string & symbol** 의 순서로 정렬된다.
- `number` key는 프로퍼티들 중 가장 앞에 위치하며, `오름차순`이다.
- `string` key는 객체에 `추가된 당시의 순서`를 유지하면서 숫자 뒤에 위치한다.
- `Symbol` key는 객체에 `추가된 당시의 순서`를 유지하면서 제일 마지막에 위치한다.

- 2) number(index)로 인식하는 key는 다음과 같다.

- 0 이상의, `첫째자리가 0이 아닌 숫자`는, 문자열로 입력해도 똑같이 `숫자`로 인식한다.
- `첫째자리가 0`인 두자리 이상의 숫자는 문자열로 입력해야 하고, `문자열`로 인식한다.
- `음수`는 **문자열**로 입력해야 하고, `문자열`로 인식한다.

**&there4; 'index'로 인식할 수 있는 경우에 한해서만 작은 수부터 나열한다.**

- 3) 열거순서를 엄격히 지키는 경우는 다음과 같다.

- `Object.getOwnPropertyNames()`
- `Reflect.ownKeys()`
- `Object.assign()`

- 4) ES5 하위문법인 다음의 경우에는 정합성을 보장하지 않는다.

- `for in`
- `Object.keys()`
- `JSON.stringify()`

순서가 보장되지 않기 때문에, **어떤 환경이냐**에 따라서 순서가 보장될 수 있고 아닐 수 있음.