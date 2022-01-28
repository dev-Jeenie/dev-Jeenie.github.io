---
title: "Java script ES6💫 중급🔥 ✍️ (1) Symbol"
permalink: /cs/javascriptEs610
tags:
  - [CS]

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


### 1-2-1. 암묵적 형변황

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
  }
}

```
변수 a를 접근하는 곳에서만 해당 값을 정확히 쓸 수 있음.<br/>
a에 접근하지 못하는 곳에서는 symbol a라는 값을 **알아낼 수 없다.**

 

