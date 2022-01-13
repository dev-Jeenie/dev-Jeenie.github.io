---
title: "Java script ES6💫 제대로 알아보기! ✍️ (5) rest parameter"
permalink: /cs/javascriptEs65
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-13
last_modified_at: 2022-01-13
---

![]()

## 1. rest parameter(나머지 매개변수)
불확실하고 복잡한 `arguments`를 **대체하기 위해** 나온 것!

rest란?
- ~를 제외한 나머지

> 지난시간에 배운 `arguments`란?
  - 불확실성이 높고, `유사배열 객체`이기 때문에 실제 배열의 메소드를 쓰려면 복잡함.
  - **array.prototype**에 있는 직접 적용하는 메소드(call 또는 apply등)을 써서 해야했음.


### 1-1. arguments의 경우

```js
function f (x, y) {
  var rest = Array.prototype.slice.call(arguments, 2)
  console.log(rest)
}
f(1, 2, true, null, undefined, 10)
```
원래 받으려던 인자는 x,y두개 뿐인데 **`값을 더 많이 넘겨버린 경우`**.<br/>
이걸 제어하기 위해서는 기존에는 `arguments`를 사용했음.<br/>

근데 이 `arguments`를 배열로 쓰고 싶으면,<br/> `call`이나 `apply`같은 `prototype 메소드`를 써서 적용했어야함.<br/>

### 1-2. rest parameter의 경우



```js
const f = function (x, y, ...rest) {
  console.log(rest)
}
f(1, 2, true, null, undefined, 10)
// [true, null, undefined, 10]
```
x, y를 뺀 **나머지가 확실한 `배열`로** 들어옴.


**rest parameter의 기능**
- ...뒤에 변수명을 붙이면, 이 변수가 ...을 무시한 `나머지` 넘어온 인자들을 **모두 취합해서 `배열`로** 받아들인다.


```js
const f = function (...rest) {
  console.log(rest)
}
f(1, 2, true, null, undefined, 10)
// [1, 2, true, null, undefined, 10]
```

전부 나머지로 받아들이면, 완전히 argument를 대체할 수 있음!<br/>

단, rest parameter는 반드시 `마지막 parameter여야`함.

```js
function f (a,b,c, ...z) {
  console.log(z)
}
f(1,2)

// 결과 []
```

```js
function f (a, ...z) {
  console.log(z)
}
f(1,2)

// 결과 [2]
```


## 2. rest parameter 상세

### 2-1. 무조건 끝에서만!

```js
function f (_first, ...rest, _last) {
  console.log(_first, _last)
}
f(1,2,3,4,5,6,7,8,9)

// 불가능
```

처음과 끝 잘라내고 중간 것만 받는 것 불가능.


### 2-2. 객체의 setter에서

setter에는 나머지를 쓸 수 없다. 값을 여러개 넣어봐야 의미가 없기 때문에....

```js
let person = {
  name: 'name',
  age : 30,
  get personInfo(){
    return this.name + ' ' + this.age
  },
  set personInfo (...val) {
    this.name = val[0]
    this.age  = val[1]
  }
}
console.log(person.personInfo)
```

(이해못함)