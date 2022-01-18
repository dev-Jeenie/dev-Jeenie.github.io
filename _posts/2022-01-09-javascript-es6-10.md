---
title: "Java script ES6💫 제대로 알아보기! ✍️ (10) Function"
permalink: /cs/javascriptEs610
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-18
last_modified_at: 2022-01-18
---

![]()
# 10. destructuring assignment (해체할당. 구조분해할당. 디스트럭쳐링)

## 10-1. 배열 해체할당

### 10-1-1. 사용법

#### 1) 기본

```js
var colors = ['red', 'white', 'orange']
var first = colors[0]
var second = colors[1]
var third = colors[2]
console.log(first, second, third)
```

```js
const colors = ['red', 'white', 'orange']
const [first, second, third] = colors
console.log(first, second, third)
```

#### 2) 발췌

```js
const colors = ['red', 'white', 'orange']
const [ , , third, fourth] = colors
console.log(third)
```

### 10-1-2. 활용

#### 1) rest parameter 와의 연동

```js
const arr = [1, 2, 3, 4, 5]
const [ a, ...b ] = arr
const [ , , ...c ] = arr
console.log(a, b, c)
```

#### 2) default parameter와의 연동

```js
const [a = 10, b = 20] = [undefined, 5]
const [c, d = c * 2] = [5]
const [e = f, f] = [undefined, 10]
```

#### 3) 다차원 배열에서

```js
const arr = [1, [2, [3, 4], 5], 6]
const [a, [b, [ , c], ], d] = arr
console.log(a, b, c, d)
```

#### 4) 값 교환하기

```js
var a = 10
var b = 20
var c = a
a = b
b = c
console.log(a, b)
```

```js
let a = 10;
let b = 20;
[a, b] = [b, a]
console.log(a, b)
```


## 10-2. 객체 해체할당

### 10-2-1. 사용법

#### 1) 기본: _{추출할 프로퍼티명 : 할당하고자 하는 변수명}_

```js
const iu = {
  name : '아이유',
  age : 25,
  gender : 'female'
}
const {
  name: n,
  age: a,
  gender: g
} = iu
console.log(n, a, g)
```

#### 2) 할당할 변수명은 생략 가능. (property shorthand)

```js
const iu = {
  name : '아이유',
  age : 25,
  gender : 'female'
}
const {
  name,
  age,
  gender
} = iu
console.log(name, age, gender)
```

#### 3) 발췌

```js
const iu = {
  name : '아이유',
  age : 25,
  gender : 'female'
}
const {
  name,
  gender
} = iu
console.log(name, gender)
```

#### 4) 중첩객체의 경우 - 접근자와 추출을 구분하는 것이 중요

```js
const loginInfo = {
  device: {
    createdAt: '2017-12-06T00:14:04+0000',
    deviceId: '0000000000004Vx',
    deviceType: 'desktop'
  },
  user: {
    createdAt: '2017-03-08T18:00:28+0000',
    email: 'power4ce@gmail.com',
    name: '정재남',
    nickname: 'gomugom',
    phoneNumber: '010-9185-9155'
  }
}

const {
  device,
  user: {
    name,
    nickname,
    phoneNumber: phone
  }
} = loginInfo

// user는 변수선언이 되어있을까?
// phoneNumber와 phone 중에 선언된 변수는 어느쪽일까?
```

#### 5) default parameter와의 연동

```js
const phone = {
  name : 'iPhone',
  color : undefined
}

const {
  name: n,
  version: v = '6+',
  color: c = 'silver'
} = phone
console.log(n, v, c)

const {
  name,
  version = 'X',
  color = 'black'
} = phone
console.log(name, version, color)
```

### 10-2-2. 사용예

```js
const deliveryProduct = {
  orderedDate: '2018-01-15',
  estimatedDate: '2018-01-20',
  status: '배송중',
  items: [
    {name: '사과', price: 1000, quantity: 3},
    {name: '배', price: 1500, quantity: 2},
    {name: '딸기', price: 2000, quantity: 4}
  ]
}

const {
  estimatedDate: esti,
  status,
  items: [ , ...products]
} = deliveryProduct
console.log(esti, status, products)
```

```js
const getUrlParts = (url) => /^(https?):\/\/(\w{3,}\.[A-z.]{2,})(\/[a-z0-9]{1,}\/([a-z0-9\-.,]+))$/.exec(url)

const [ , protocol, host, , title] = getUrlParts('http://abc.com/es6/7-1.destructuring')
console.log(protocol, host, title)
```

```js
const getArea = (info) => {
  const {width, height} = info
  return width * height
}
getArea({ width: 10, height: 50 })
```

```js
const getArea = ({ width, height = width }) => {
  return width * height
}
getArea({ width: 10 })
```
