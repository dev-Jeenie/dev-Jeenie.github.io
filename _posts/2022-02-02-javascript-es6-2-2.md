---
title: "Java script ES6💫 중급🔥 ✍️ (2) 새로운 자료구조"
permalink: /cs/javascriptEs622
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
// a 1
// b 2
// c 3


// (2)
Object.prototype.method = function () { }
for (let key in o) {
  console.log(key, o[key])
}
// a 1
// b 2
// c 3
// method f() {}


// (3)
for (let key in o) {
  if(o.hasOwnProperty(key)) {
    // 이 객체안에있는 key가 정말 내가 가진 고유 프로퍼티가 맞는지
    console.log(key, o[key])
  }
}
// a 1
// b 2
// c 3

```

for in 문을 돌리면 iterable한 것처럼 보이지만 iterable하지 ❌<br/>그렇게 보이도록 만든 것.<br/>
실제로 모든 요소들을 돌면서 하나하나 진행하는 건 아님<br/>
prototype까지 검사를 함. <br/>

iterable하지 않고 그렇게 보이도록 따라한 것이기 때문에,<br/>
**객체의 고유 property**인지, **prototype 체이닝 상에 있는 더 상위의 메소드**인지 판단하지 않고 무조건 가져와서 prototype도 출력되는 것.<br/>

이걸 해결하기 위해서 3같은 짓을 또 해야함.<br/>
이 객체안에있는 key가 정말 **내가 가진 고유 프로퍼티가 맞는지 체크**해야 제대로 동작.<br/>


그래서 객체를 key와 value로 묶인 배열로 변환하는 방법은,<br/>
property 판단을 하거나 key값만 반환하게 하는 수 밖에 없었다.

```js
const o = { a: 1, b: 2, c: 3 }


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
// (2) ["a", 1]
// (2) ["b", 2]
// (2) ["c", 3]


// (5)
const oArr2 = Object.keys(o).map(k => [k, o[k]])
oArr2.forEach(v => console.log(v))
```

(4)처럼 객체의 property를 가지고 판단해서 배열로 푸시<br/>

또는 (5)처럼 object.keys로 key값만 반환하게 해서 새로운 배열<br/>


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
// 0123
```
01을 문자열로 인식했듯이, key를 문자열로 인식해서,<br/>
key를 모두 더하라고 해도 출력값이 문자열로 나옴

- 3. 따라서 키값의 unique함을 완벽히 보장하지 못함.

```js
const obj = {
  1: 10,
  01: 20,
  '01': 30
}
console.log(obj)
// {1: 20, 01: 30}

```
숫자 01과 문자 01을 똑같이 **문자 01로 취급**.<br/>
=> 캐스캐이딩 되어서 하나만 남음


- 4. 프로퍼티 개수를 직접 파악할 수 없다.

```js
const obj = { a: 1, b: 2, c: 3 }
console.log(obj.length)
// undefined

console.log(Object.keys(obj).length)
// 2
console.log(Object.values(obj).length)
// 2
```

### 1-3-2. Map
이런 `객체의 장점`만 가지고 새롭게 만들어낸 데이터 타입<br/>


- 1. [ key, value ] 쌍(pair)으로 이루어진 요소들의 집합.
  - 배열 묶음이 하나의 데이터 요소가 됨
  - 0번째 인덱스엔 key, 1번째 인덱스엔 value

- 2. 순서를 보장하며, iterable하다.

- 3. 키에는 어떤 데이터타입도 저장할 수 있으며, 문자열로 취급하지 않는다.

- 4. 추가 / 값 가져오기 / 삭제 / 초기화 / 요소의 총 개수 / 포함여부확인

- 5. 초기값 지정

- 6. 배열로 전환하기

- 7. 객체로 전환하기


#### 상세 - 3. 어떤 데이터 타입도 저장가능

```js
const map = new Map()
map.set(1, 10)
map.set(01, 20)
map.set('01', 30)
map.set({}, 40)
map.set(function(){}, ()=>{})
console.log(map)
// Map(2) {1 => 20, "01" => 30}
```
> set 메소드<br/>
map에는 set으로 추가 가능<br/>
첫번째가 key, 두번째가 value

객체의 경우엔 01과 "01"을 동일하게 간주했지만,<br/>
map은 1과 01을 동일하게 간주!

#### 상세 - 4. 추가 / 값 가져오기 / 삭제 / 초기화 / 요소의 총 개수 / 포함여부확인

```js
const map = new Map()
map.set('name', '재남')
map.set('age', 30)

console.log(map.size)

console.log(map.get('name'))
console.log(map.get('age'))

map.delete('name')
console.log(map.has('name'))
console.log(map.has('age'))
console.log(map.size)

map.clear()
console.log(map.has('name'))
console.log(map.has('age'))
console.log(map.size)
```

- get
객체는 obj.name 하면 나왔겠지만,<br/>
map은 key를 알고있으면 그 key의 값을 가져올 때 `map.get('name')` 이렇게 가져옴.

- delete
객체는 delete obj.name으로 지웠겠지만,<br/>
map은 `map.delete('name')` 이렇게 지움

- has
`map.has('name')` 로 있는지 확인할 수 있음

#### 상세 - 5. 초기값 지정


map도 set처럼 인자로 iterable한 개체를 지정할 수 있다.<br/>

- 각 요소의 내용들이 `배열`로 이루어져있어야 함.<br/>
- 각 배열 안에는 `key와 Value`라는 인덱스 2개가 있어야 함.

```js
const map1 = new Map([[10, 10], ['10', '10'], [false, true]])
console.log(map1)
// Map(3) {10 => 10, "10" => "10", false => true}
const map2 = new Map([[10, 10, 10], ['10', '10', '10'], [false, true, false]])
console.log(map1)
// Map(3) {10 => 10, "10" => "10", false => true}
```
요소 3개를 넣으면 마지막 요소는 무시<br/>
Set의 경우에는 Entries안에 화살표 없이 그냥 값만 출력이 되었는데,<br/>
Map은 중괄호 묶음과 화살표가 있고 key => value로 이루어져있다.<br/>


```js
map1.keys()
// MapIterator {10, "10", false}

map1.values()
// MapIterator {10, "10",true}

map1.entries()
// MapIterator {10 => 10, "10" => "10", false => true}
```
`MapIterator`로 출력이 되는데, `MapIterator`가 뭘까?

```js

const keys = map1.keys()
// MapIterator {10, "10", false}

keys.next().value
// 10
keys.next().value
// "10"
keys.next().value
// "false"
keys.next().value
// undefined

const values = map1.values()
values.next()
// {value: 10, done: false}
values.next()
// {value: "10", done: false}
values.next()
// {value: false, done: false}
values.next()
// {value: undefined, done: true}

```

`MapIterator`는 map iterating을 한다. <br/>
그럼 `next`라는 method를 호출할 때, 그 안에 `value`와 `done`이라는 값을 준다.<br/>
요소들을 다 꺼내서 하나하나 다 살펴본 뒤에 더이상 없다, 그럴 때 done을 true로 돌려줌<br/>


`객체`는 원래 이런 것이 불가능하다.<br/>
이렇게 하나하나 살펴볼 수 있게(`iterable하게`) 만들어주는 것이 바로 `map`이고,<br/>그럼 spread를 할 수 있다.<br/>
그럼 이 map에 `keys`, `values`, `entries` 등을 쓰면 `next`라는 method를 사용할 수 있다.<br/>
(`set`에도 마찬가지로 존재)


```js
console.log(map1 === map2)

const gen = function* () {
	for (let i = 0; i < 5; i++) {
		yield [i, i+1]
  }
}
const map3 = new Map(gen())
console.log(map3)
```

#### 6. 배열로 전환하기

```js
const map = new Map([[10, 10], ['10', '10'], [false, true], ['name', '재남']])
const mapArray1 = [...map]
// (4) [Array(2), Array(2), Array(2), Array(2)]

const mapArray2 = [...map.keys()]
// (4) [10, "10", false, "name"]

const mapArray3 = [...map.values()]
// (4) [10, "10", true, "재남"]

const mapArray4 = [...map.entries()]
// (4) [Array(2), Array(2), Array(2), Array(2)]

```

```js

// 여기서 set은
// Set(5) {1,2,3,4,5}

[...set.keys()]
// (5) [1, 2, 3, 4, 5]

[...set.values()]
// (5) [1, 2, 3, 4, 5]

[...set.entries()]
// (5) [Array(2), Array(2), Array(2), Array(2), Array(2)]
// key와 value로 묶인 쌍으로 나옴

```

주의할 점 ⭐️ <br/>

- Object에서의 key, values, entries
  - : 그냥 배열로 나옴

```js
const obj = {a: 1, b: 2, c: 3}
Object.keys(obj)
// (3) ["a", "b", "c"]
Object.values(obj)
// (3) [1, 2, 3]
Object.entries(obj)
// (3) [Array(2), Array(2), Array(2)]
Object.entries(obj).next()
// undefined
```

- set에서의 key, values, entries
  - : MapIterator로 나옴
```js
const set = new Set([1,2,3,4,5,3,4,2])

set.entries().next()
// {value: Array(2), done: false}

set.entries()
// setIterator {1, 2, 3, 4, 5}
```
`Object.keys()`는 es5의 문법이기 때문에 MapIterator가 아닌 그냥 배열로 나온다!<br/>
그에 맞춰서 values와 entries도 동일.<br/>
당연히 next도 쓸 수 없음.<br/>

#### 7. 객체로 전환하기

```js
const map1 = new Map([[10, 10], ['10', '10'], [false, true], ['name', '재남']])
const map2 = new Map([[{}, 10], [function(){}, '10'], [[], true], [Symbol('심볼'), '재남']])
const convertMapToObject = map => {
  const resultObj = {}
  [...map].forEach(([k, v]) => {
    if(typeof k !== 'object') {
      resultObj[k] = v
    }
  })
  return resultObj
}
const obj1 = convertMapToObject(map1)
const obj2 = convertMapToObject(map2)
```


### 1-3-3. WeakMap





