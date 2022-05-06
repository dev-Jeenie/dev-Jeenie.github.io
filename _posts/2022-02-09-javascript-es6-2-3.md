---
title: "(3) Iterable, Iterator, generator"
permalink: /es62/javascriptEs623
tags:
  - [es62]

navigation: true
toc: true
toc_sticky: true

date: 2022-02-11
last_modified_at: 2022-02-11
---

![]()


# 1. iterable, iterator, generator

## 1-1. iterable

### 1-1-1. 소개

내부 요소들을 공개적으로 탐색(반복)할 수 있는 데이터 구조.  <br/>
[Symbol.iterator] 메소드를 가지고 있다.<br/>
이 메소드를 가지고 있으면 iterable한 객체.<br/>

기본적으로 [Symbol.iterator]를 가지고 있는 대표적인 `iterable`한 타입!

- Array
- Set
- Map
- String

```js
const arr = ['a', 'b', 'c']
const set = new Set(['a', 'b', 'c'])
const map = new Map([[false, 'no'], [true, 'yes'], ['well', 'soso']])
const str = '문자열도 이터러블하다!?!!'

const obj = {0: 1, 1: 2, 2: 3, length: 3}
console.dir(obj)
// Object
// 0: 1
// 1: 2
// 2: 3
// 유사배열 객체
```



### 1-1-2. 개체 자신이 iterable한 경우

#### 1) array, map, set, string

#### 2) `[Symbol.iterator]` 메소드가 존재하는 모든 개체

```js
console.dir([1, 2, 3])
console.dir(new Set([1, 2, 3]))
console.dir(new Map([[0, 1], [1, 2], [2, 3]]))
```

- 없는 경우

```js
const obj = { 0: 1, 1: 2, 2: 3, length: 3 }
console.dir(obj)
```
에러가 나지만, 여기에다가 만들어서 넣어주면 iterable한 객체가 될 수 있다<br />

#### 3) `generator`를 호출한 결과
generator는 함수인데, 함수 뒤에 *이 붙고 <br/>
next로 호출할 때마다 yeild에서 호출이 된다
```js
function* generator () {
  yield 1
  yield 2
  yield 3
}
const gene = generator()

gene.next()
// {value: 1, done: false}

gene.next()
// {value: 2, done: false}

gene.next()
// {value: 3, done: false}

gene.next()
// {value: undefined, done: true}

```


### 1-1-3. iterable한 개체의 특징

```js
const arr = [1, 2, 3]
const map = new Map([['a', 1], ['b', 2], ['c', 3]])
const set = new Set([1, 2, 3])
const str = '이런것도 된다.'
const gene = (function* () {
  yield 1
  yield 2
  yield 3
})()
```

#### 1) Array.from 메소드로 배열로 전환 가능

`Array.from()` <br/>
새로운 메소드. iterable한 객체가 들어오면 `배열로 반환`해준다<br/>

```js
const arrFromArr1 = Array.from(arr)
// (3) [1,2,3]
const arrFromMap1 = Array.from(map)
// (3) [Array(2),Array(2),Array(2)]
const arrFromSet1 = Array.from(set)
// (8) ["이", "런", "것", "도", " ", "된", "다", ".", ]
const arrFromStr1 = Array.from(str)
// (8) ["이", "런", "것", "도", " ", "된", "다", ".", ]
const arrFromGene1 = Array.from(gene)
// (3) [1,2,3]
```

#### 2) spread operator로 배열로 전환 가능

```js
// const map = new Map([['a', 1], ['b', 2], ['c', 3]])

const arrFromArr2 = [...arr]
// (3) [1,2,3]

const arrFromMap2 = [...map]
// (2) ["a", 1] (2) ["b", 2] (2) ["c", 3]

const arrFromSet2 = [...set]
// 1 2 3

const arrFromStr2 = [...str]
// 이 런 것 도  된 다 .

const arrFromGene2 = [...gene]
```

#### 3) 해체할당 가능

```js
const [arrA, , arrC] = arr
console.log(arrA, arrC)
// 1 3
```


### 1-1-3-1.`Array.from`과, `spread operator`와, `해체할당`의 동작원리

⭐️ 여기서 중요한 점 ⭐️ <br/>

`Array.from`과, `spread operator`와, `해체할당`은 모두 <br/>동작원리가 같다!<br/>

```js
Array.from(iterable)
...iterable
[, , a] = iterable

var a = iterable[Symbol.iterator]()
```

- 1) `iterable`한 객체를 받아서
- 2) 모두 `Symbol.iterator`를 호출해서 변수에 담고
- 3) 변수.`next()`를 done이 true가 되기 전까지 `반복호출`하고

`Array.from()` : 반복된 결과를 배열로 만들어준다 <br/>
`spread operator` : 반복된 결과를 묶음처리해서 넘겨준다 <br/>
`해체할당` : 반복된 결과와 매칭되는 것마다 할당해준다 <br/>

- 예제) 배열

```js
const iter = arr[Symbol.iterator]();
console.log(iter)
// Array Iterator {}

iter.next()
// {value: 1, done: false}

iter.next()
// {value: 2, done: false}

iter.next()
// {value: 3, done: false}

iter.next()
// {value: undefined, done: true}

```
arr 배열 자신에게는 없지만,<br/>
배열의 Prototype에 정의되어있는 `Symbol.iterator`가 있기 때문에<br/>
iterable하고, 따라서 `next`를 사용할 수 있음!<br/>

`next` 배열의 요소 하나하나를 꺼내서 value와 done을 반환해주는 것<br/>
그 `next`라는 메소드를 만들 수 있는 게 `Symbol.iterator`가 있기 때문에.<br/>
<br/>

이런 동작원리는 `for of`도 동일.



#### 4) for ... of 명령 수행 가능

```js
for (const x of arr) {
  console.log(x)
}
for (const x of map) {
  console.log(x)
}
for (const x of set) {
  console.log(x)
}
for (const x of str) {
  console.log(x)
}
for (const x of gene) {
  console.log(x)
}
```

#### 5) `Promise.all`, `Promise.race` 명령 수행 가능

(Promise 강의 이후에 다시와서 보기)

```js
const a = [
  new Promise((resolve, reject) => { setTimeout(resolve, 500, 1) }),
  new Promise((resolve, reject) => { setTimeout(resolve, 100, 2) }),
  3456,
  'abc',
  new Promise((resolve, reject) => { setTimeout(resolve, 300, 3) }),
]
Promise.all(a)
  .then(v => { console.log(v) })
  .catch(err => { console.error(err) })

const s = new Set([
  new Promise((resolve, reject) => { setTimeout(resolve, 300, 1) }),
  new Promise((resolve, reject) => { setTimeout(resolve, 100, 2) }),
  new Promise((resolve, reject) => { setTimeout(reject, 200, 3) }),
])
Promise.race(s)
  .then(v => { console.log(v) })
  .catch(err => { console.error(err) })
```

#### 6) `generator - yield*` 문법으로 이용 가능

```js
const arr = [1, 2, 3]
const map = new Map([['a', 1], ['b', 2], ['c', 3]])
const set = new Set([1, 2, 3])
const str = '이런것도 된다.'

const makeGenerator = iterable => function* () {
  // yield* [1, 2, 3]
  yield* 1;
  yield* 2;
  yield* 3;
}
// yield뒤에 *이 붙으면 iterable 객체가 올 수 있다

const arrGen = makeGenerator(arr)()
const mapGen = makeGenerator(map)()
const setGen = makeGenerator(set)()
const strGen = makeGenerator(str)()

console.log(arrGen.next())
console.log(mapGen.next())
console.log(...setGen)
console.log(...strGen)
```

> 여기까지 모두 내부적으로는 
> `Symbol.iterator` 또는 `generator`을 실행하여 iterator로 변환한 상태에서
> `next()`를 반복 호출하는 동일한 로직을 기반으로 함.

#### 7) iterable 객체에 `[Symbol.iterator]`가 **잘** 정의되지 않은 경우

Symbol.iterator가 있으면 무조건 다 iterable한 객체일까? ❌❌ <br/>

```js
const obj = {
  a: 1,
  b: 2,
  [Symbol.iterator] () {
    return 1
  }
}
console.log([...obj])
// error! Result of the Symbol.iterator method is not an object
```
obj는 Symbol.iterator를 실행한 결과가 개체가 아니다. 결과가 1이니까 <br/>

```js

const obj2 = {
  a: 1,
  b: 2,
  [Symbol.iterator] () {
    return {

    }
  }
}
console.log([...obj2])
// error! object is not iterable

```
그럼 빈 객체를 반환하면? <br/>
내부를 채워야만 iterable한 개체가 된다


### 1-1-4. iterable한 개체를 인자로 받을 수 있는 개체

```js
new Map()
new Set()
new WeakMap()
new WeakSet()
Promise.all()
Promise.race()
Array.from()
```

WeakMap과 WeakSet으로 만들어진 데이터는 iterable하지 않지만, <br/>
괄호 안에는 iterable한 개체를 받을 수 있다<br/>

```js
const a = new WeakMap([
  [{} , 1],
  [{a: 1}, 2]
]);
console.log(a)
[...a]
// error! a is not iterable
```

WeakMap은 `Symbol.iterator`가 없기 때문에