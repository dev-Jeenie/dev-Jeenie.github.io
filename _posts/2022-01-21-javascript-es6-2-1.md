---
title: "Java script ES6💫 중급🔥 ✍️ (1) Symbol"
permalink: /es62/javascriptEs621
tags:
  - [es62]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-21
last_modified_at: 2022-01-21
---

![]()


# 1. Symbol

## 1-1. 들어가기 전에 다시한번 정리하는 데이터 Type 분류

-- `Primitive` Value --<br/>
**값 `기본형`임**

- number
- string
- boolean
- null
- undefined
- Symbol

-- `Reference` Value --<br/>
**값 `참조형`임**

- object
- array
- function
- Map
- Set
- WeakMap
- WeakSet

`기본형` 값과 `참조형` 값의 가장 큰 차이는?<br/>

- 주소값을 가진다 (X)
  둘 다 주소값을 가짐
- 각자 가지는 그 주소값에
  - **`값이 그대로`** 들어오느냐, **`값이 별개의 데이터로`** 따로 있느냐의 차이


Es6에서 새로 등장한 type

## 1-2. Symbol

**탄생 목적 :**<br/>
`비공개 멤버`에 대한 요구를 충족시키기 위해!

- primitive value
  - 유일무이하고 고유한 존재
- 비공개 멤버에 대한 needs에서 탄생
  - Js에는 private member가 없어서
- 기본적인 열거대상에서 제외
  - for in 문처럼 **값을 순회**하면서 출력하려고 할 때 **`접근불가`**
- 암묵적 형변환 불가


### 1-2-1. 암묵적 형변환

**다른 타입의 경우**

```js

'a' + 1
// "a1"

true + 1
// 2
```
문자열 + 숫자<br/>
숫자가 문자열로 암묵적 형변환 됨<br/>

boolean + 숫자<br/>
boolean이 숫자로 암묵적 형변환 됨<br/>


**Symbol의 경우**

```js

Symbol() + 1
// error! can not convert a Symbol value to a number
Symbol() + 'a'
// error! can not convert a Symbol value to a string

```

형변환 불가능<br/>


```js
const a = Symbol()
const b = Symbol()

a === b
// false

a == b
// false
```

타입+값 일치 비교도 X<br/>
값 일치 비교도 X<br/>

완전히 다른 값이라서 비교가 불가능<br/>

```js
const a = Symbol('a')
const b = Symbol('a')

a === b
// false

a == b
// false
```
Symbol로 값을 똑같이 써넣어도 다름.<br/>
Symbol은 `생성 시마다` 완전히 다른 값!<br/>

```js

const a = Symbol('a')
const b = Symbol('a')
const c = b

b === c
// true

```

위치를 참조시키는 건 같다.



```js
const x = () => {
  const a = Symbol('a')
  return {
    [a]: 10
    // 변수에 접근하기 위한 대괄호 표기법,
    // 객체의 literal 생성시에도 사용 가능하다
  }

const y = x();

y
// { Symbol(a): 10 }

y.a
//undefined

y['a']
//undefined

y[Symbol('a')]
//undefined

}

```
y.a<br/>
y['a']<br/>
y[Symbol('a')]<br/>

이렇게는 a의 값에 접근할 수 없음!<br/>

가능한 유일한 방법은?<br/>
변수 a를 접근하는 곳에서만 해당 값을 정확히 쓸 수 있음.<br/>
a에 접근하지 못하는 곳에서는 symbol a라는 값을 **알아낼 수 없다.**

<br/>


```js
const x = () => {
  const a = Symbol('a')
  return {
    [a]: 10,
    a: a
  }

const y = x();

y
// { a:Symbol(a), Symbol(a): 10 }

y.a
// Symbol(a): 10

y['a']
// 10
}
```
변수 a에 접근하기 위해서,<br/>
**함수 x를 return**할 때, a라는 property를 다시 내려받음<br/>

그럼 a라는 property에 심볼이 있으니 값 자체를 알 수 있다.
<br/>이제 a로 접근할 수 있음!<br/>

이때의 x함수는 은닉화에 성공한 함수.<br/>
값은 쓸 수 있고 노출은 되어있지만<br/>
퍼블릭한 상태로 접근할 수 있는 권한을
주느냐, 주지 않느냐에 따라 다르다!<br/>

- 퍼블릭한 상태로 `접근 권한 O`

```js
const x = () => {
  const a = Symbol('a')
  return {
    [a]: 10,
    a: a
  }
```
a라는 property를 밖으로 빼줌<br/>

=> 값에 `접근할 수 있다`

- 퍼블릭한 상태로 `접근 권한 X`

```js
const x = () => {
  const a = Symbol('a')
  return {
    [a]: 10
  }
```
a라는 property를 밖으로 빼주지 않음<br/>
=> 보이기만 하고 값에 `접근할 수 없다`<br/>

y를 통해 객체에 접근할 수 있지만,<br/>
객체에 있는 Symbol(a)라는 Property엔 `접근불가`<br/>

> Reflect.ownKeys(y)<br/>
접근할 수 있는 방법 있긴 함

```js
const x = () => {
  const a = Symbol('a')
  return {
    [a]: 10
  }
  Reflect.ownKeys(y)
  // [Symbol(a)]

  const b = Reflect.ownKeys(y)
  b// [Symbol(a)]

  y[b[0]]
  // 10
```
하지만 이 방법은 0번째 값이 바뀔 수 있어서 좋지 않음.<br/>

### 1-2-2. new 연산자 사용 불가능
```js
new Symbol()
// error! Symbol is not a constructor
```

new연산자 사용 불가, 무조건 static한 형식으로 써야함

### 1-2-3. 문자열 아닌 타입은 toString처리

```js
const sb1 = Symbol('symbol')
const sb2 = Symbol('symbol')
console.log(sb1, sb2)
console.log(sb1 === sb2) // false
```

같은 문자열인 값을 넣어도 다름

```js
const obj = { a: 1 }
const sb1 = Symbol(obj)
const sb2 = Symbol(obj)
console.log(sb1)
// Symbol([object object])
obj.toString()
// "[Object Object]"
```

Symbol([toString]) 처리되어서 Object로 들어감 

```js
const sb = Symbol(null)
sb
// Symbol(null)
console.log(typeof sb)
// symbol
```
null도 문자열로 들어감<br/>
typeof로는 symbol이라고 출력됨<br/>


### 1-2-4. 객체의 property의 key로 활용



```js
const NAME = Symbol('이름')
const GENDER = Symbol('성별')
const iu = {
  [NAME]: '아이유',
  [GENDER]: 'female',
  age: 26
}
const suzi = {
  [NAME]: '수지',
  [GENDER]: 'female',
  age: 26
}
const jn = {
  [NAME]: '재남',
  [GENDER]: 'male',
  age: 30
}

console.log(iu, suzi, jn)
```

Symbol로 선언한 property는 열거되지 않음 <br/>
그러니 이 객체의 식별자 이상으로써의 의미는 지니지 않음.<br/>
그래서 주로 상수로 오는 경우가 많음<br/>


```js

const obj = {
  [Symbol('a')]: 1
}

obj
// { Symbol(a): 1 }
```
Symbol(a)의 값을 알고있는 변수가 없음.<br/>
그래서 이 값을 알아낼 수 있는 방법이 Reflect.ownKeys(y) 말고는 없다!<br/>
은닉화를 떠나서 나도 못쓰는 값이 되어버림


### 1-2-5. 프로퍼티 키로 할당한 심볼 탐색 (접근)

```js
console.log(iu[NAME], suzi[NAME], jn[NAME])

for (const prop in iu) {
  console.log(prop, iu[prop])
}
// age 26

Object.keys(iu).forEach(k => {
  console.log(k, iu[k])
})
// age 26

Object.getOwnPropertyNames(iu).forEach(k => {
  console.log(k, iu[k])
})
// age 26
```

for in 문으로는 Symbol을 제외한 age만 출력됨.<br/>`keys`, `getOwnPropertyNames`도 마찬가지

```js
Object.getOwnPropertySymbols(iu).forEach(k => {
  console.log(k, iu[k])
})
// Symbol(이름) "아이유"
// Symbol(성별) "female"

Reflect.ownKeys(iu).forEach(k => {
  console.log(k, iu[k])
})
// age 26
// Symbol(이름) "아이유"
// Symbol(성별) "female"
```

**getOwnPropertySymbols**<br/>
새로 등장한 메소드. 객체 안에있는 symbol들만 반환해준다.<br/>
대신 이건 Symbol만 나오고 age값이 안나옴!<br/>

**Reflect.ownKeys()**<br/>
이걸 사용하면 모두 출력이 가능.



### 1-2-6. private member 만들기


```js

const obj = (() => {
  const _privateMember1 = Symbol('private1')
  const _privateMember2 = Symbol('private1')
  return {
    [_privateMember1]: '외부에서 보이긴 하는데 접근할 방법이 마땅찮네',
    [_privateMember2]: 10,
    publicMember1: 20,
    publicMember2: 30
  }
})() // 즉시실행함수

console.log(obj)
console.log(obj[Symbol('private1')])
// 이건 아예 새로운 심볼생성
console.log(obj[_privateMember1])
// 이건 _privateMember1를 모르고

for (const prop in obj) {
  console.log(prop, obj[prop])
}

Object.keys(obj).forEach(k => {
  console.log(k, obj[k])
})

Object.getOwnPropertyNames(obj).forEach(k => {
  console.log(k, obj[k])
})

// 물론 아래 방법들로는 접근 가능하나 정상적이지 않음
Object.getOwnPropertySymbols(obj).forEach(k => {
  console.log(k, obj[k])
})

Reflect.ownKeys(obj).forEach(k => {
  console.log(k, obj[k])
})
```

그냥 객체를 만들지 않고 즉시실행 함수로 만들어서 함수 스코프를 생성. <br/>
그럼 _privateMember1, _privateMember2는 함수 스코프 밖을 **벗어날 수 없음** <br/>

이렇게 Symbol을 활용하면 private member를 흉내낼 수 있다. <br/>


🤷🏻‍♀️ 근데 private member를 왜 하려고 해??<br/>


`캡슐화`, 바꾸는 실수를 방지하기 위해서.<br/>

외부에서 접근 못하게 한다 === 다른사람이, 혹은 내가 바꾸지 못하게 한다<br/>

obj는 `캡슐화`가 된 것!<br/>

이것과는 완전히 정반대인 `Symbol.for`가 있다.


### 1-2-7. `Symbol.for` - 공유심볼

- public member! 전역공간에서 공유되는 심볼.

```js
const a = Symbol.for('abc')
const b = Symbol.for('abc')

a === b
// true!
```
식별하는 방법이, 문자열만 가지고 식별을 한다.<br/>
그리고 Symbol.for라고 하는 퍼블릭한 심볼들이 가지는 값을 모아둔 전역공간에 있는 공간이 있음<br/>

그 공간에 Symbol.for로 선언한 것들이 다 모여있음!<br/>
Symbol.for 를 **처음 사용**하면 그 값을 **`공용공간에 저장`**을 하고,<br/>
이미 사용했으면 그걸 **`그대로 가져다가 쓴다`**.<br/>

=> `a는 처음 선언`한 거니까 공간에 `저장`하고<br/>
`b는 이미 있는지` 찾아보고 있으니까 `그대로 가져다가 쓴 것`<br/>


```js
const COMMON1 = Symbol.for('공유심볼')
const obj = {
  [COMMON1]: '공유할 프로퍼티 키값이에요. 어디서든 접근 가능하답니다.'
}
console.log(obj[COMMON1])
// 공유할 프로퍼티 키값이에요. 어디서든 접근 가능하답니다.

const COMMON2 = Symbol.for('공유심볼')
console.log(obj[COMMON2])
// 공유할 프로퍼티 키값이에요. 어디서든 접근 가능하답니다.

console.log(COMMON1 === COMMON2)
// true
```

> Symbol.keyFor
```js
const UNCOMMON = Symbol('비공유심볼')
const commonSymbolKey1 = Symbol.keyFor(COMMON1)
// 공유심볼
const commonSymbolKey2 = Symbol.keyFor(COMMON2)
// 공유심볼
const commonSymbolKey2 = Symbol.keyFor(UNCOMMON)
// undefined
```
Symbol.for에서만 쓸 수 있는 메소드.<br/>
변수에 있는 키, 문자열 값을 출력해준다.
