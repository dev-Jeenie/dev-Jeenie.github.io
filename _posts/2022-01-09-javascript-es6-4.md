---
title: "Java script ES6💫 제대로 알아보기! ✍️ (4) Default parameter"
permalink: /cs/javascriptEs64
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-12
last_modified_at: 2022-01-12
---

![]()

## 1. Default parameter(매개변수 기본값)

### 1-1. Default parameter의 정의

`파라미터` = `매개변수` = `함수의 인자`<br/>

- 그럼 default parameter는?<br/>

함수의 인자로 넘어오는 것들을 `기본값`을 지정해줄 수 있음.<br/>


- 기존의 방법

```js
const f = function (x, y, z) {
  x = x ? x : 4
  y = y || 5
  if (!z) {
    z = 6
  }
  console.log(x, y, z)
}
f(1)
// 결과 1,5,6
```
인자를 받고 인자에 대한 판단을 함수 안에서 해왔다.<br/>
그런데 🚨 문제점 🚨

```js
const f = function (x, y, z) {
  x = x ? x : 4
  y = y || 5
  if (!z) {
    z = 6
  }
  console.log(x, y, z)
}

f(0, null)
// 결과 4,5,6

```

0과 null을 넘겨주면 false로 판단해버림.<br/>

이걸 고치려면 .....

```js
const f = function (x, y, z) {
  x = x !== undefined ? x : 4
  y = typeof y !== "undefined" || 5
  if(!z) {
    z = 6
  }
  console.log(x, y, z)
}
f(0, null)

// 결과 0, true 6
```
<img src="/assets/images/es6-default-parameter.png" /><br/>

이런 처리를 해줘야했음.<br/>
핵귀찮다.

- default parameter의 방법

```js
const f = function (x=4, y=5, z=6) {
  console.log(x, y, z)
}
f(0, null)

// 결과 0, true 6
```

<img src="/assets/images/es6-default-parameter-2.png" /><br/>


## 2. Default parameter 상세

### 2-1. undefined 또는 누락됐을 경우에만 할당

### 2-2. 식을 넣을 수 있다

default parameter로 함수를 넘길 수 있다.<br/>

**=> 에러 체크가 가능**

```js
const notValid = function () {
  console.error('notValid Called.')
  return 10
}
const sum = function (x = notValid(), y = notValid()) {
  console.log(x + y)
}
sum(1, 2)
sum(1) // error!notValid Called.
```
<img src="/assets/images/es6-default-parameter-3.png" /><br/>



### 2-3. let 선언과 동일한 효과!

- 원래 함수의 인자는,

```js
function a (a,b,c) {
  var a = 1;
  var b = 2;
  var c = 3;
}
a(1,2,3)
```
실행컨텍스트가 열린 순간에 인자 하나하나를 변수로 선언해서 변수의 값을 할당하는 것까지를 내부에서 처리함.
그래서 내부 변수로써만 존재함.

- 그런데 함수의 인자에 default parameter를 할당하면,

```js
function a (a=1,b=2,c=3) {
  let a = 1;
  let b = 2;
  let c = 3;
}
a(1,2,3)
```

let을 선언한 것과 동일하다!

**예제**

```js
function a (a = 1, b = a + 1, c = 3) {
  console.log(a, b, c);
}

a(1, undefined, 3)
```
b의 위치에 undefined가 들어갔기 때문에 default parameter가 나타남.<br/>

그런데, let선언한 것과 `동일하게 동작`하기 때문에 아래처럼은 **불가능**!
```js
function a (a = 1, b = c, c = 3) {
  console.log(a, b, c);
}

a(1, undefined, 3) // error! c is not defined
```

`a를 실행할 때에 c의 값이 넘어갔음`에도 불구하고 🚨 에러 🚨가 뜨는이유?
<br/>

변수를 선언하는 곳이 `(a=1, b=c, c=3)` 여기니까!

```js
function a (a = 1, b = c, c = 3) {
  let a;
  let b = c + 1;
  let c;

  console.log(a, b, c);
}

a(1, undefined, 3) // error! c is not defined
```
이것과 동일함.<br/>
`b`가 `c`를 참조하려고 하는 순간, `TDZ`에 걸려서 <strong style="color:black;background-color:yellow">reference error</strong>!


> 여기서 잠깐, 자꾸 나오는 reference error가 대체 뭐야?<br/>
reference란? 참조. **= 참조 에러라는 뜻**<br/>
**`변수를 선언한 순간`**에 변수에 **`값이 할당되어있지 않으면`** 생기는 오류<br/>


> 지난시간에 배웠던 `메모리 형태`<br/>

- 1) 변수명이 선언. 그럼 얘한테
- 2) 변수명과 별도로 값이 들어있는 공간의 `메모리 주소를 매칭` 시켜서 참조하라고 줘야함.
- 3) 매칭 작업을 하기 위해서 값을 찾는데 값이 없으니 참조 에러!


기존에 쓰던

```js
var = a;
```

는 참조 주소를 이미 들고있기 때문에 undefined가 나올 수 있는 것.<br/>

하지만 let과 const는 hoisting을 했을 때, <br/>
참조 주소를 매칭 시켜두지 않았으니까 TDZ에 걸려버림<br/>

🤷🏻‍♀️ `let`, `const` 변수 : "내가 **참조**할 수 있는 데이터가 **어딨는지 모르겠어**!! 나 `참조에러`야!!"



#### 2-3-1. 기본값이 변수일 경우 주의사항

default parameter의 값이 `변수`라면, `이름이 달라야한다`.

```js
let a = 10
let b = 20
function f (aa = a, b = b) {
  console.log(aa, b)
}
f(1, 2) //당연히 문제 없이 1,2 출력
f(undefined, 2) // aa의 기본값인 10, 2 출력
f(1) // error! b is not defined
```

왜 에러?<br/>
바로 TDZ에 걸렸기 때문.

> TDZ

```js
let a = 10;

```
를 읽는 방법.<br/>

- 10을 들고
- a에 넣어라

그런데
```js

let a = a;

```
라고하면? 아래와 같다.

```js

let a;
// 이때의 a는 아직 주소가 매칭되어있지 않음
a = a; // 그럼 들고오려고 하는 순간, TDZ에 걸림!

```

메모리공간에 **매칭하려는 작업**을 `값을 할당할 때`에 할건데,<br/>
**값이 매칭되지 않은 걸** 가져다가 매칭하려고 하니까 에러발생.<br/>

그래서 같은 변수명을 쓰려고 하면 안된다~

#### 2-3-2. argument에도 영향을 준다

- `유사배열객체`(array-like object)
  - : **객체**인데 각 propety `키가 인덱스`이고, `length`라는 property가 있는 객체

- 그럼 `arguments`란?
  - 불확실성이 높고, `유사배열 객체`이기 때문에 실제 배열의 메소드를 쓰려면 복잡함.
  - **array.prototype**에 있는 직접 적용하는 메소드(call 또는 apply등)을 써서 해야했음.

(이해못함.... 그냥 넘어가도 된다)

