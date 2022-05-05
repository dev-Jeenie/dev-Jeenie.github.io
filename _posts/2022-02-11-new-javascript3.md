---
title: "Java script ES6💫 중급🔥 ✍️ (3) Iterable, Iterator, generator"
permalink: /es62/newJavascript3
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








## 14-3. Generator

### 14-3-1. 소개

- 중간에서 멈췄다가 이어서 실행할 수 있는 함수.  
- function 키워드 뒤에 `*`를 붙여 표현하며, 함수 내부에는 `yield` 키워드를 활용한다.  
- 함수 실행 결과에 대해 `next()` 메소드를 호출할 때마다 순차적으로 제너레이터 함수 내부의 `yield` 키워드를 만나기 전까지 실행하고, `yield` 키워드에서 `일시정지`한다.
- 다시 `next()` 메소드를 호출하면 그 다음 `yield` 키워드를 만날 때까지 함수 내부의 내용을 진행하는 식이다.

```js
function* gene () {
  console.log(1)
  yield 1
  // gen.next()를 실행하면 console이 출력되고 yield를 만나서 여기서 멈춤
  console.log(2)
  yield 2
  // 다시 gen.next()를 실행하면 console이 출력되고 yield를 만나서 여기서 멈춤
  console.log(3)
}
const gen = gene()

gen.next()
// 1
// {value: 1, done: false}

gen.next()
// 2
// {value: 2, done: false}

gen.next()
// 3
// {value: undefined, done: true}
```

iterable한 개체의 장점! <br/>
이렇게 yield를 만나기 전에 할 일을 한 뒤에, <br/>
외부에서 다른 필요한 동작을 하고 <br/>
다시 next를 호출하면 다음 동작이 이루어지니까 <br/>
next의 호출 순서를 이용해 개발자의 의지대로 동작 순서를 조절할 수 있다. <br/>

```js

function* gene () {
// 동작 1
yield 1
// 동작 3
yield 2
// 동작 5
}
const gen = gene()

gen.next()
// 동작 2
gen.next()
// 동작 4
gen.next()
// 동작 6

```

- 선언 방식

```js
function* gene () { yield }
// 함수 선언문일 경우

const gene = function* () { yield }
// 함수 표현식일 경우

const obj = {
  gene1: function* () { yield }
// 기존 방식대로 함수 선언문을 객체의 key에 할당하는 방법
  *gene2 () { yield }
// 메소드 축약형일 땐 이렇게
}
// 객체의 메소드로 할당할 경우

class A {
  *gene () { yield }
}
// class에서도 마찬가지
```

### 14-3-2. 이터레이터로서의 제너레이터

```js
function* gene () {
  console.log(1)
  yield 1
  console.log(2)
  yield 2
  console.log(3)
}
const gen = gene()
console.log(...gen)
```


**다시한번 보는 `iterable한 객체` 만드는 방법 ⭐️**  <br/>

1) 복잡한 방법

- 그 객체의 prototype 상에 Symbol.iterator라는 메소드가 있어야하고,<br/>
- 그 메소드는 객체를 반환해야하고<br/>
- 반환한 객체는 next라는 메소드를 반환해야했고<br/>
- 그 next메소드는 다시 done를 키로 가지고 있는 객체를 반환해야했다

```js
[Symbol.iterator] () {
  return {
    next () {
      return {
        done: false
      }
    }
  }
}
```

2) `generator`를 사용하는 방법

generator를 쓰면 이렇게 복잡하게 구현하지 않아도 됨!<br/>
객체안에 Symbol.iterator를 generator로 받을 수 있다<br/>
그러기 위해서는 내부에서 신경써야할 것은 `yield`만 만들어주면 됨

```js
[Symbol.iterator] () {
  yield 123123
}
```

이럴 경우 이 자체가 Symbol.iterator로써의 기능을 수행함.<br/>
왜? next를 실행할 때마다 yield에서 멈추고, value를 반환하고 done을 알아서 처리해주기 때문에.<br/>

```js
const obj = {
  a: 1,
  b: 2,
  c: 3,
  *[Symbol.iterator] () {
    for (let prop in this) {
      yield [prop, this[prop]]
      // 여기서 prop안에는 a, b, c,가 담길 것이고
      // this[prop]안에는 1,2,3이 담길 거니까
      // 이 배열을 가지고 yield가 된다
    }
  }
}
console.log(...obj)
// > (2) ["a",1] > (2) ["b",2] > (2) ["c",3]

for (let p of obj) {
  console.log(p)
}
//  > (2) ["a",1]
//  > (2) ["b",2]
//  > (2) ["c",3]

```


### 14-3-3. `yield* [iterable]`

yield* 은 뒤에 iterable한 객체를 받아서, <br/>
그 객체 **하나하나마다 멈춤**!

```js
function* gene () {
  yield* [1, 2, 3, 4, 5]
  yield
  yield* 'abcde'
}

const gen = gene();

gen.next()
// {value: 1, done: false}
gen.next()
// {value: 2, done: false}
gen.next()
// {value: 3, done: false}
gen.next()
// {value: 4, done: false}
gen.next()
// {value: 5, done: false}
gen.next()
// {value: undefined, done: false}
gen.next()
// {value: 'a', done: false}
gen.next()
// {value: 'b', done: false}
gen.next()
// {value: 'c', done: false}
gen.next()
// {value: 'd', done: false}
gen.next()
// {value: 'e', done: false}
gen.next()
// {value: undefined, done: true}

```

💁🏻‍♀️ : generator로 만드니까 굉장히 간단하게 iterator를 만들 수 있게 됐구나! <br/>

generator를 중첩해서 쓸 수도 있음.


```js
function* gene1 () {
  yield [1, 10]
  yield [2, 20]
}
function* gene2 () {
  yield [3, 30]
  yield [4, 40]
}
function* gene3 () {
  console.log('yield gene1')
  yield* gene1()
  // gene1을 실행한 결과를 yield* 로 줬기 때문에 아래와 같다
  // yield [1, 10]
  // yield [2, 20]

  console.log('yield gene2')
  yield* gene2()
  // gene2을 실행한 결과를 yield* 로 줬기 때문에 아래와 같다
  // yield [3, 30]
  // yield [4, 40]

  console.log('yield* [[5, 50], [6, 60]]')
  yield* [[5, 50], [6, 60]]
  // [5, 50]
  // [6, 60]

  console.log('yield [7, 70]')
  yield [7, 70]
}
const gen = gene3()

gen.next()
// yield gene1
// {value: Array(2), done: false}

gen.next().value
// (2) [2, 20]

gen.next().value
// yield gene2
// (2) [3, 30]

gen.next().value
// (2) [4, 40]

gen.next().value
// yield* [[5, 50], [6, 60]]
// (2) [5, 50]

gen.next().value
// (2) [6, 60]

gen.next().value
// yield [7, 70]
// (2) [7, 70]

gen.next().value
// undefined

gen.next()
// {value: undefined, done: true}

```


#### 14-3-4. 인자 전달하기

```js
function* gene () {
  let first = yield 1
  console.log(first)
  let second = yield first + 2
  console.log(second)
  yield second + 3
}
const gen = gene()

// 설명 (1)
gen.next()
// {value: 1, done: false}

// 설명 (2)
gen.next()
// undefined
// {value: NaN, done: false}


```

동작을 자세히 살펴보면<br/>

**설명 (1)**<br/>

- let first의 호이스팅 과정

`let first`를 위로 끌어올리고<br/>
`first = yield 1`
yield 1는 first로 할당한다, 이런 순서이기 때문에<br/>
first는 아직 선언만 되고 값이 할당되지 않아서 TDZ 영역에 갇힌 상태인데,<br/>
yield에서 멈춰버린다! (다음 next를 만나기 전까지는)<br/>
let first = yield 1 이게 완료(실행)가 되지 않은 상태로 끝나버림<br/>

**설명 (2)**<br/>

`let first = yield 1` 이제 끝났다.<br/>

`let second`를 위로 끌어올리고<br/>
`secont = yield first + 2` 할당하려는데 yield에서 멈춰버림.<br/>
`let second = yield first + 2` 가
완료(실행)이 되지 않았기 때문에 second에는 값이 들어가지 않았다.<br/>

🤷🏻‍♀️ : 그런데 yield의 출력값은 3으로 잘 나와야할 텐데 NaN이 왜 나왔지??<br/>
**=> first의 값이 `undeined`이기 때문에.**

🤷🏻‍♀️ : 그럼 `undefined`는 왜 들어갔지??<br/>
`let first`에 값을 할당하는 줄이 이제 끝나서 할당 되었지만,<br/>
`yield 1` 은 아까 **밖으로 던져버려서 값이 없다**!<br/>
넣어야할 **값이 없으니 first에는 undefined**가 들어간 것.<br/>

🤷🏻‍♀️ 이상한데 안이상한 방법은 없어?<br/>

=> `next()`의 **인자**로 **값**을 넣어주면 된다.<br/>

```js

gen.next(10)
// {value: 12, done: false}

```
yield 구문 앞에 있는 변수에다가, 다음번에 넘겨준다<br/>
그래서 first에 10이 들어가서 12가 출력된 것!

```js

gen.next(20)
// {value: 23, done: false}

```
이젠 second에 20이 들어가서 23이 출력.<br/>

이 함수는, **내가 넘겨준 값을 가지고 다음 yield 동작에 영향을 주게끔** *만든 함수.<br/>
next의 인자로 넘겨준 덕분에 외부와 소통수단이 열린 것.<br/>
이렇게 하지 않으면, gen 함수 scope안에 갇혀있는 변수들과 소통할 방법이 없다!<br/>

#### 14-3-5. 비동기 작업 수행

userId가 1000번 이후인  데이터를 가져와서
그 중에 4번째에 위치한 User정보를 보고싶다.

우선 이 동작을 살펴보자.<br/>

```js
const ajaxCalls = () => {
  const res1 = fetch.get('https://api.github.com/users?since=1000')
}
const m = ajaxCalls()
```
서버에 request 를 보내고, 서버에서 response가 온다.<br/>
그런데 이 사이의 시간 갭이 있음. 네트워크에 따라서 응답시간은 천차만별이다.<br/>
res1에는 내가 원하는 데이터가 담기지는 않음!<br/>
res1은 요청해라~ 하는 선언일 뿐.<br/>
**요청하자마자** 이 내용에 대한 분석은 끝났고 그 값이 그대로 res1에 담길 뿐이다.<br/>
res1에는 request를 하자마자 바로 결과가 담긴다.<br/>
즉, **response된 결과가 담기는게 아니라, `원하지 않는 불필요한 데이터`가 담기는 것**<br/>
서버에 보내고 응답이 언제올 지 모르는데,<br/>
응답이 오기도 전에 이 문장은 바로 순식간에 이뤄져서 무의미한 데이터가 담겨버린다.<br/>

```js
const ajaxCalls = () => {
  const res1 = fetch.get('https://api.github.com/users?since=1000')
  const res2 = fetch.get(`https://api.github.com/user/${res1[3]}`)
}
const m = ajaxCalls()
```

그래서 이렇게 res2로 res1의 3번째 데이터를 담아봤자<br/>
애초에 res1 데이터가 들어있지 않으니 의미없다.<br/>

**=> 이것이 바로 `동기 처리`**<br/>
시간에 대한 고려없이, 그냥 이문장 먼저 실행하고, 다음 문장을 실행시키는 것 뿐.<br/>

🤷🏻‍♀️ : 그럼, 한 문장이 **`실행된 다음에`** 실행을 시키기 위해서는 어떻게 해야해?<br/>

**=> 바로 `비동기 처리`를 해야한다!**

- 1) 콜백방식의 비동기처리(기존 JQuery에서 사용했던 방식)

```js
$.ajax({
  method: 'GET',
  url:'https://api.github.com/users?since=1000',
  success: function (res) {
  const res2 = fetch.get(`https://api.github.com/user/${res1[3]}`)
  }
});

```
서버에서 요청에 대한 결과가 success가 왔을 때에만 그 결과값으로 어떠한 처리를 하게함.


- 2) Promise 방식의 비동기처리

```js
fetch.get('https://api.github.com/users?since=1000')
.then(function (res) {
  const res2 = fetch.get(`https://api.github.com/user/${res1[3]}`)
  });
```
fetch.get는 원래 하나의 promise!<br/>
그렇기 때문에 then을 붙여서 사용할 수 있따.


- 3) Generator 방식의 비동기처리

```js
const fetchWrapper = (gen, url) => fetch(url)
// (6) 이 promise의 과정을 거쳐서 서버에 갔다가
  .then(res => res.json())
// (7) 결과가 오면 그 결과를 json으로 바꿔서
  .then(res => gen.next(res));
  // 여기서의 res는 json으로 바뀌어있는 채로 gen.next로 전달됨
// (8) 그 json 받은걸 가지고 다시 들어온 gen의 next를 돌림. 이건 yield 앞에있는 req1에 들어간다
// => 서버에 갔다가 응답이 온 데이터가 req1에 담기는 것이 확인됨!

function* getNthUserInfo() {
  const [gen, from, nth] = yield;
  // 처음에 그냥 yield만 실행하게 되어있다.
  // (4) gen에는 getNthUserInfo, from엔 1000, nth엔 4가 들어간다
// 다음번 next를 할 때 yield의 다음부터 실행되니까, 그때 그 값이 해체할당되어서 들어가는 것
  const req1 = yield fetchWrapper(gen, `https://api.github.com/users?since=${from || 0}`);
  // (5) fetchWrapper를 실행해서 gen과 url을 넘겨준다
  const userId = req1[nth - 1 || 0].id;
  // (9) req1에 들어있는 확실한 데이터를 바탕으로 유저정보를 빼냄
  console.log(userId);
  const req2 = yield fetchWrapper(gen, `https://api.github.com/user/${userId}`);
  // (10),  fetchWrapper의 인자로 generator와 유저ID를 보내서 (6,7,8) 순서를 거친 뒤 req2에는 확실한 유저정보가 담김.
  console.log(req2);
}
const runGenerator = (generator, ...rest) => {
  const gen = generator();
  gen.next();
  // 첫째 yield인  const [gen, from, nth] = yield; 에서 멈춤
  gen.next([gen, ...rest]);
  // (3) 아래에서 받은 generator와 1000,4배열을 풀어헤쳐서 배열로 묶어 보냈다.
}
runGenerator(getNthUserInfo, 1000, 4);
runGenerator(getNthUserInfo, 1000, 6);
// (1) runGenerator를 실행해. generator는 getNthUserInfo이고, 
// 1000과 4는 ...rest라고 하는 배열로 받아라.

```

generator방식의 비동기 처리는 이렇게 yield를 이용한다.<br/>
분명 비동기 처리인데 동기처리하는 것처럼 순차적으로 같은 뎁스에 내려서 쓸 수 있게 됨.
  

```js
const fetchWrapper = url => fetch(url).then(res => res.json());
function* getNthUserInfo() {
  const [from, nth] = yield;
  const req1 = yield fetchWrapper(`https://api.github.com/users?since=${from || 0}`);
  const userId = req1[nth - 1 || 0].id;
  console.log(userId);
  const req2 = yield fetchWrapper(`https://api.github.com/user/${userId}`);
  console.log(req2);
}
const runGenerator = (generator, ...rest) => {
  const gen = generator();
  gen.next();
  gen.next([...rest]).value
    .then(res => gen.next(res).value)
    .then(res => gen.next(res));
}
runGenerator(getNthUserInfo, 1000, 4);
runGenerator(getNthUserInfo, 1000, 6);
```

promise를 다른 위치에서 구현할 수도 있다.<br/>

아까는 `fetchWrapper`에게 `generator`를 넘겨서 `fetchWrapper`가 `next`를 호출하는 방식이었지만,<br/>

이번 방식은 `fetchWrapper`에겐 url만 넘기고,<br/>
`runGenerator`가 `next`를 실행한 것을 바탕으로 `promise`를 여기서 구현<br/>


=> 하지만 `async`와 `await`로 더욱 간단하게 구현할 수 있다. <br/>
나온지 몇년 되지 않았고, 이게 없어서 generator로 비동기처리하려고 고군분투를 했음!<br/>

