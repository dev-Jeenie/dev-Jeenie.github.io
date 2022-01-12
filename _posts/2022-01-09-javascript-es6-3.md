---
title: "Java script ES6💫 제대로 알아보기! ✍️ (3) Template literal"
permalink: /cs/javascriptEs63
tags:
  - [CS]

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
console.log(`${[0,1,2]})`)
// 결과 '0,1,2'
```