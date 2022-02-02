---
title: "Java script ES6💫 중급🔥 ✍️ (2) 새로운 자료구조"
permalink: /cs/javascriptEs610
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-02-02
last_modified_at: 2022-02-02
---

![]()


# 1. set, weakset

## 1-1. Set
새로 등장한 참조형 데이터<br/>

**중복을 허용하지 않고** **순서를 보장하는 값**들로만 이루어진 리스트<br/>
추가 삭제 초기화 요소의 총 개수, 포함 여부 확인이 가능

**예제**

배열 a의 요소들 중 중복되는 것을 제거하려면,<br/>


```js

const a = [1, 2, 3, 4, 5, 4, 3, 2, 5, 4]

const b = a.reduce((acc,v) => {
  if(acc.includes(v)) return acc;
  acc.push(v);
  return acc;
}, []);

```
- 1) reduce를 활용한 방법
a안에 이미 v가 있다면 누적 acc을 배열을 반환하고<br/>
없다면 누적 acc에 그 v를 push를 해라<br/>

```js

const a = [1, 2, 3, 4, 5, 4, 3, 2, 5, 4]

const c = new Set(a)

```
- 2) set을 활용한 방법
set으로 배열을 넘기면 이 자체가 중복을 배제한 값들로 이루어진 세트가 된다.<br/>


```js
const set = new Set();
set.add(5)
set.add('5')
set.add(-0)
set.add(+0)

// Set(3) {5,'5',0}

set.add(5)
// Set(3) {5,'5',0}

console.log(set.size)
// 3

const set2 = new Set([1,2,3,4,5])
// Set(5) {1,2,3,4,5}

```
하나하나 add로 넣을 수도 있지만, 초기값을 배열인 상태로 넣을 수 있다<br/>
배열이 아니라도, iterable한 모든 것들을 넣을 수 있음


### 1-1-1. 배열과 set의 차이


set은 `중복을 무시`하고, `인덱스가 없다`는 걸 제외하면 배열과 큰 차이가 없다.

- 요소를 추가하려면?<br/>
  - 배열 : `push` 
  - set : `add`
- 길이를 가져오려면?<br/>
  - 배열 : `length`
    - length의 값이 바로 노출
  - set : `size`
    - size는 invoke를 해야 볼 수 있다
- 포함여부를 알려면?<br/>
  - 배열 : `includes`, `indexOf`, `find`, `findIndex`
    - 배열 전체를 순회하면서 값을 비교해보고 찾아냄(그래서 느림)
  - set : `has`
- 요소를 삭제하려면?<br/>
  - 배열 : `indexOf` + `splice` or `delete`
    - 인덱스를 알아내서 그 배열에서 splice를 시키거나
    - 인덱스를 알아내서 그 인덱스를 delete해서 undefined가 들어감
  - set : `delete`


### 1-1-2. set 상세

- 초기값 지정
  : 인자로 iterable한 개체를 지정할 수 있다
  `펼칠 수 있는 모든 것들`은 배열로 만들 수 있으니까, <br/>
  이걸 이용해서 다시 `새로운 Set`을 만들 수 있음 <br/>

```js
const s = new Set([1,2,3,'1','2','3',2,5,6])
// Set(8) {1,2,3,'1','2','3', ....}

const ss = new Set([...s])
// Set(8) {1,2,3,'1','2','3', ....}

```
하나하나 add로 넣을 수도 있지만, 초기값을 배열인 상태로 넣을 수 있다<br/>

```js
const map = new Map()
map.set('a',1).set('b',2).set({}, 3)
const set2 = new Set([...map])
// Map(3) {'a' => 1, 'b' => 2, {...} => 3}

const set3 = new Set(map)

```

배열이 아니라도, iterable한 모든 것들을 넣을 수 있음<br/>
Map도 iterable하기 때문에 새로운 set의 요소로 넣을 수 있음!<br/>

**new Set(iterable한 모든 것)**

> iterable Object<br/>
: array, string, map, set


- 인덱스(키)가 없다

```js
console.log(...set.keys())
console.log(...set.values())
console.log(...set.entries())
// 1 2 3 4 5
// 1 2 3 4 5

set.forEach(function(key, value, ownerSet){
  console.log(key, value, this)
}, {})
// 1 1 > {}
// 2 2 > {}
// 3 3 > {}
// 4 4 > {}
// 5 5 > {}

console.log(set[1])
// undefined
```

키가 곧 value이고, value가 곧 key이기 때문에 모두 동일하게 나옴<br/>
set은 index를 주지않기 때문에 `index로 접근할 수 없음`<br/>

🤷🏻‍♀️ : 아니 그럼 set 안에 있는 요소에 접근을 어떻게 해??<br/>

=> set은 그런 용도 ❌<br/>
하나하나 순회하면서 각각의 동작들을 처리하게 하고싶을 때 사용하는 게 set.<br/>
인덱스 값을 몰라도 될 때, 더 빨리 순회할 수 있음<br/>

```js
const arr = [...set]
// (5) [1,2,3,4,5]

const arr2 = [1,2,3,1,2,3,1,2,3]
const newArr = [...new Set(arr2)]
// (3) [1,2,3]
```

set도 iterable하니까 펼치면 배열의 요소가 됨.<br/>
그걸 활용해서 중복이 배제된 배열을 만들 수 있음
 
👩🏻‍💻 실무에서 set은<br/>

- 이럴 땐 set🆗
  - 1) 중복제거
  - 2) 전체순회할 필요성이 있는 경우
  - 3) 값의 유무 판단
- 이럴 땐 set❌
  - 1) 특정 요소에 접근
  - 2) 인덱스가 필요한 경우


## 1-2. WeakSet





### 1-2-1. Set과의 비교


#### 1-2-1-1. 참조 카운트를 올리지 않음

이것이 목적이기 때문에, `참조형 데이터만 요소로` 삼을 수 있다


```js
const s = new WeakSet(); // 1)

let obj = {}; // 2)

let obj2 = obj; // 3)

obj2 = null; // 4)

obj = null; // 5)

```

- 1) WeakSet은 참조카운트를 증가시키지 않음.<br/>
- 2) obj라는 변수가 {} 객체를 참조한다
  - {}의 참조 카운트 **1**
- 3) obj2라는 변수가 obj 변수를 통해서 {} 객체를 참조한다
  - {}의 참조 카운트 **2**
- 4) obj2에 null이 들어감
  - {}의 참조 카운트 **1**
- 5) obj에 null이 들어감
  - {}의 참조 카운트 **0** **reference count : 0**
  - `Garbage collector`의 수거 대상
  
`Garbage collector`의 수거 대상이 된 {}는 <br/>
아직은 사라지지 않았지만, <br/>
`Garbage collector`가 collecting을 하는 순간 사라짐 <br/>


```js
const s = new WeakSet(); // 1)

s.add(obj); // 6)

obj = null; // 7)

```

- 6) obj라는 변수가 가리키는 {}를 s에 추가
  - 여전히 {}의 `참조카운트는 1`
  - WeakSet은 참조카운트를 증가시키지 않기 때문에.
  - 그냥 Set이었다면 {}의 참조카운트는 2가 되었을 것
- 7) obj에 null이 들어감
  - {}의 참조카운트는 0
  - {}는 수거대상. 수거되면 s의 안에는 **아무것도 없게 된다** 

그래서 지금처럼 변수 안에 넣는 것이 안전하고, <br/>
new WeakSet(obj)처럼 literal 선언한 것들을 바로 넣는 것은, <br/>
해당 변수의 참조 카운트가 사라지면 통째로 `사라지기 때문에` **안전성이 떨어진다**. <br/>

**`set`에 객체를 저장할 경우** <br/>
set에도 `해당 객체에 대한 참조가 연결`되어, 그 객체를 참조하는 변수가 그 참조를 없애도 set에는 여전히 그 객체가 `살아있음` <br/>

**`WeakSet`에 객체를 저장할 경우** <br/>
객체에 대한 `참조카운트를 올리지 않음`. 그 객체를 참조하는 변수가 그 참조를 없애면 WeakSet 내의 객체는 `수거대상이 됨` <br/>

```js
const obj1 = { a: 1 }
const set = new Set()
set.add(obj1)
obj1 = null
```


#### 1-2-1-2. iterable이 아님

- 약한 결합, 언제 사라질지 모름.
iterable이 아니기 때문에 <br/>
size, keys, values, entries, forEach, for of 모두 사용 ❌ <br/>

단 has는 가능<br/>



<hr/>



## 1-3. map, weakMap

### 1-3-1. 객체와의 비교

#### 1-3-1-1. 객체의 단점

- 1. `iterable`하지 않다.

> `iterable`이란? <br/>
안에 있는 내부 요소들을 `하나하나` `순차적으로 반복`해서 `모든 요소를 검토`할 수 있는 것.


```js
const o = { a: 1, b: 2, c: 3 }

// (1)
for (let key in o) {
  console.log(key, o[key])
}

// (2)
Object.prototype.method = function () { }
for (let key in o) {
  console.log(key, o[key])
}

// (3)
for (let key in o) {
  if(o.hasOwnProperty(key)) {
    console.log(key, o[key])
  }
}

// (4)
const obj2Arr = obj => {
  const arr = []
  for (let key in obj) {
    if(obj.hasOwnProperty(key)) {
      arr.push([key, obj[key]])
    }
  }
  return arr
}
const oArr = obj2Arr(o)
oArr.forEach(v => console.log(v))

// (5)
const oArr2 = Object.keys(o).map(k => [k, o[k]])
oArr2.forEach(v => console.log(v))
```

- (1)






- 2. 키를 문자열로 취급한다.

```js
const obj = {
  1: 10,
  2: 20,
  3: 30
}
let res = 0
for (let key in obj) {
  res += key
}
console.log(res)
```

- 3. 따라서 키값의 unique함을 완벽히 보장하지 못함.

```js
const obj = {
  1: 10,
  01: 20,
  '01': 30
}
console.log(obj)
```

- 4. 프로퍼티 개수를 직접 파악할 수 없다.

```js
const obj = { a: 1, b: 2, c: 3 }
console.log(Object.keys(obj).length)
```

#### 1-3-1-2. Map
