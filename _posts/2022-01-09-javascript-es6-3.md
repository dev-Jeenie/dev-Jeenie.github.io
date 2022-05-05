---
title: "Java script ES6💫 제대로 알아보기! ✍️ (3) Template literal"
permalink: /js2/javascriptEs63
tags:
  - [es6]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-11
last_modified_at: 2022-01-11
---

![]()

## 1. Template literal이란?


**string literal** <br/>
: 문자 그대로의. <br/>

**Template literal** <br/>
: 템플릿 그대로의. <br/>

### 1-1. Template literal의 장점

- **backtick (`)**
  ```js
  var a = 'abc';
  var a = "abc";
  var a = `abc`;
  ```

  이 세개는 모두 같은 값. <br/>

- **multi-line**

```js
var a = 'abc\n' +
'def';
console.log(a)
// "abc
// def"

var b = `a
bb
ccc`;
console.log(b)
// "a
// bb
// ccc"
```


- **string interpolation**(문자열 안에 보간, 끼워넣기)

```js
const a = 10
const b = 20
const strBefore = a + ' + ' + b + ' = ' + (a + b);

const str = `${a} + ${b} + = ${a + b}`
console.log(str)
```
이렇게 ${ }로 묶은 것 안에는 `값`이나 `식`, `함수의 호출`을 넣을 수 있음.<br/>
`문`은 값이 없기 때문에 넣지 못함!<br/>


### 1-2. Template literal 상세

- 1) multi-line의 경우 들여쓰기에 주의해야함.

```js
var a = 'abc\n' +
            'def';
console.log(a)
// "abc
// def"

var b = `a
  bb
    ccc`;
console.log(b)
// "a
//   bb
//    ccc"
```
들여쓰기하면 그대로 출력된다

함수에서 문제가 될 수 있음.

```js
const f = function () {
  const a = `abc
    def
    ghij`;
console.log(a)
}
f()
// 결과
//  abc
//     def
//     ghij

```

함수를 실행하면 들여쓰기가 그대로 출력된다.<br/>


```js
const f = function () {
  const a = `abc\n`+
    `def`+
    `ghij`;
console.log(a)
}
f()
// 결과
//  abc
//  def
//  ghij

```

기존처럼 사용하면 들여쓰기 문제 해결.<br/>
여전희 백틱 안에서는 보간을 사용할 수 있음.<br/>

- 2) 결국 문자열이라 자동으로 toString 처리된다

```js
console.log(`${[0,1,2]})`) // 0,1,2
console.log(`${{a:0,b:1}})`) // [object object]
console.log(`${function(){return 1}})`) // function()
console.log(`${(() => 1)()}` + 1 ) // 11
```
- 배열의 toString
- 객체의 toString
- 함수의 toString
- `즉시실행함수`의 toString

**`즉시실행함수`가 어떻게 저렇게 나오는가?**

```js
`${(function(){ return 1; })()})` // '1'
+ 1
```
함수를 괄호로 감싸서 `즉시실행함수` 실행.<br/>
1을 반환. 백틱으로 감쌌기 때문에 **`문자열`**.<br/>
+ 숫자 1을 더함<br/>
= **문자열** 1 + **숫자** 1 => 더해져서 11!<br/>



- 3) 중첩된 backtick 처리

```js
console.log(`     Foo ${` Bar `}     `)
console.log(`    Foo ${`   Bar ${` Bar `}   `}   `)
```

- 4) 앞 뒤를 트림처리 할 수 있다.

```js
function a () {
  return `
<div>
    <h1>Lorem ipsum.</h1>
</div>
  `.trim()
}
// 백틱과 div사이에 들어갈 공백만 trim처리하면 됨.
console.log(a())
console.log(a().replace(/\n/g, ''))
```

Template literal이 나오게 된 계기?<br/>

>reduce를 배운 뒤에 다시 듣기

```js
const linesToHTML = function (characters) {
  return characters.reduce(function (charactersResult, character) {
    let {name, lines} = character
    return `${charactersResult || ''}
<article>
  <h1>${name}</h1>
  <ul>
    ${lines.reduce(function (linesResult, line) {
      return `${linesResult || ''}
    <li>${line}</li>
      `.trim()}, 0)}
  </ul>
</article>
  `.trim()}, 0)
}
const characters = [{
  name: 'Aria Stark',
  lines: ['A girl has no name.']
}, {
  name: 'John Snow',
  lines: [
    'You know nothing, John Snow.',
    'Winter is coming.'
  ]
}]
document.body.innerHTML = linesToHTML(characters)
```


## 2. forEach, map, reduce

### 2-1. forEach

for문을 편하게 쓰기 위한 방법!<br/>

> Array.prototype.forEach(callback[, thisArg])
 <br/>

forEach는 인자를 두개 받는다. <br/>
`콜백함수`라는 인자와, **생략이 가능한 `thisArg`**

- callback
  > function (currentValue, [, index[, originalArray]]) <br/>
  - currentValue : 콜백함수를 실행하는 배열의 현재값이 들어옴(필수)
  - index : 현재 인덱스가 들어옴(생략가능)
  - originalArray: 원본 배열(생략가능)
- thisArg
  - this에 할당할 대상. 생략시 global객체

```js
const a = [ 1, 2, 3 ]
a.forEach(function (v, i, arr) {
    console.log(v, i, arr, this)
}, [ 10, 11, 12 ])
```

<img src="/assets/images/es6-foreach.jpeg" /><br/>
결과<br/>
<img src="/assets/images/es6-foreach-2.jpeg" /><br/>


근데 여기서 this를 뭐하러 넣어?<br/>


```js
const a = [ 1, 2, 3 ]
a.forEach(function (v, i, arr) {
    console.log(this.[i])
}, [ 10, 11, 12 ]) // 10, 11, 12
```
뭐 이렇게 a를 가지고 순회를 돌면서, <br/>
다른 this의 i를 써야할 수도 있으니까~


### 2-2. map



> Array.prototype.map(callback[, thisArg])

- callback
  > function (currentValue[, index[, originalArray]])<br/>
  - `currentValue`: 현재값
  - `index`: 현재 인덱스
  - `originalArray`: 원본 배열
- `thisArg`: this에 할당할 대상. 생략시 global객체



```js
const a = [ 1, 2, 3 ]
const b = a.map(function (v, i, arr) {
    console.log(v, i, arr, this)
    return this[0] + v
}, [ 10 ])
```

<img src="/assets/images/es6-map.jpeg" /><br/>

결과<br/>
<img src="/assets/images/es6-map-2.jpeg" /><br/>



### 2-3. reduce

es5에서 등장.

> Array.prototype.reduce(callback[, initialValue])

- `initialValue`: 초기값. 생략시 첫번째 인자가 자동 지정되며,  
  이 경우 currentValue는 두번째 인자부터 배정된다.
- `callback`
> function (accumulator, currentValue[, currentIndex[, originalArray]])<br/>
  - `accumulator`: 누적된 계산값
  - `currentValue`: 현재값
  - `currentIndex`: 현재 인덱스
  - `originalArray`: 원본 배열




#### 2-3-1. initial value 유무의 차이


- 1) initial value 있을 경우
```js
const arr = [ 1, 2, 3 ]
const res = arr.reduce(function (p, c, i, arr) {
  console.log(p, c, i, arr)
  return p + c
}, 10)
```

<img src="/assets/images/es6-reduce-initial.jpeg" /><br/>


**예제**

```js
const arr = [ 1, 2, 3, 4 ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
}, '') // initial value 있음
console.log(str)
```

step | res | item | index | array
:-:|:-:|:-:|:-:|:-:
1 | `''` | 1 | 0 | [1,2,3,4]
2 | '1' | 2 | 1 | [1,2,3,4]
3 | '12' | 3 | 2 | [1,2,3,4]
4 | '123' | 4 | 3 | [1,2,3,4]
result | '1234' | | | 




- 2) initial value 없을 경우

```js
const arr = [ 1, 2, 3 ]
const res = arr.reduce(function (p, c, i, arr) {
  console.log(p, c, i, arr)
  return p + c
})
console.log('res', res)
```


<img src="/assets/images/es6-reduce-initial-2.jpeg" /><br/>



**예제**



```js
const arr = [ 1, 2, 3, 4 ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
}) // initial value 없음
console.log(str)
```

step | res | item | index | array
:-:|:-:|:-:|:-:|:-:
1 | `'a'` | 'b' | 1 | ['a','b','c','d']
2 | 'ab' | 'c' | 2 | ['a','b','c','d']
3 | 'abc' | 'd' | 3 | ['a','b','c','d']
result | 'abcd' | | |



#### 2-3-2. reduce의 활용

- 1) `문자열`을 만들 수 있음

```js
const arr = [ 'a', 'b', 'c', 'd' ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
})
console.log(str)
// 결과 : abcd
```
- 2) `객체`를 만들 수 있음

```js
const arr = [ 'a', 'b', 'c', 'd' ]
const str = arr.reduce(function (res, item, index, array) {
  res[item] = item;
  return res;
},{}) //initial value 없음
console.log(str)

// {a:'a', b:'b', c:'c', d:'d'}
```
<img src="/assets/images/es6-reduce-object.jpeg" /><br/>


근데 이해안됨....


**예제**

**𝑸. 1 ~ 10까지 더하라.**

- for로 하면....

```js
const a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let res = 0;
for(let b = 0; b < a.length; b++) {
  res += a[b];
}

// 결과 55
```
세상 오래걸림

- reduce로 하면.....

```js
const a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

const res = a.reduce(a,c => a + c);
```

<img src="/assets/images/es6-reduce-add-numbers.jpeg" /><br/>



### 2-4. 이 모든 것들의 공통점!

배열의 모든 메소드의 **받는 인자**는, `중요한 순서로 나열`되어있다.

- forEach
  - currentValue 필수, index 필수X
- map
  - currentValue 필수, index 필수X
- reduce
  - accumulator 필수, currentValue 필수, index 필수X


> jQuery의 each메소드는 index, item순서이니 헷갈릴 수 있음<br/>


### 2-4. 이 모든 것들의 차이점!

- forEach
  - for문 돌리는 것과 같은 개념
- map
  - for문을 돌려서 새로운 배열을 만드는 목적
  - 그래서 반드시 return 필요!
- reduce
  - for문을 돌려서 최종적으로 다른 무언가를 만드는 목적
  - 그래서 반드시 return 필요!



## 3. tag function

```js
const tag = function (strs, arg1, arg2) {
  return {strs: strs, args: [arg1, arg2]}
}
const res = tag `순서가 ${1}이렇게 ${2}`
console.log(res)
```




```js
const tags = function (strings, ...expressions) {
  console.log(strings, expressions)
}
const a = 'iu', b = 'Friday'
const str = tags `Hello, ${a}! Today is ${b}!!`
// ["Hello, ", "! Today is ", "!!"]
// ["iu", "Friday"]
```


- strings와 expression을 조합한 예제


```js
const setDecimalSeperators = function (strs, ...args) {
  return args.reduce(function (p, c, i) {
    return p + strs[i] + (c + '').replace(/\d{1,3}(?=(\d{3})+(?!\d))/g, '$&,')
  }, '') + strs[strs.length - 1]
}
const res = setDecimalSeperators `이 사과는 하나에 ${2000}원이고, 총 ${1234567}개를 구입하시면 총 ${2000 * 1234567}원 이에요.`
console.log(res)
```
