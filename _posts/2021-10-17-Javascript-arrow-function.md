---
title: "# 05.Arrow Function ๐ฟ"
permalink: /js1/JavascriptArrowFunction
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-17
last_modified_at: 2021-10-17
---

![]()

# 5. Arrow function

6. sub-program<br/>

๋ชจ๋  ํ๋ก๊ทธ๋จ์ด ๊ฐ๊ฐ์ ๊ธฐ๋ฅ์ด ์๋๊ฑด ๋ชจ๋ ๋ค๋ฅธ function์ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ.<br/>
ํ๋ก๊ทธ๋จ ์์์ ์์ ๊ธฐ๋ฅ๋ค์ ์ํํ๋ ๊ฒ์ด function์ด๋ค<br/>

Input์ผ๋ก parameter๋ฅผ ๋ฐ์์ ์ฒ๋ฆฌํ๊ณ ,<br/>
Output์ผ๋ก return์ ํ๋ ๊ฒ์ด function<br/>

๊ทธ๋์, ์ธ์ด ์์ฒด์ ์กด์ฌํ๋ function์ ์ฐ๊ฑฐ๋<br/>
API(application programming Interface)๋ฅผ ์ธ ๋, function์ ์ด๋ฆ์ ๋ณด๊ณ  ๊ทธ ๊ธฐ๋ฅ์ ์์ํ  ์ ์์<br/>
์ ๋ฌํด์ผํ๋ ํ๋ผ๋ฏธํฐ ๊ฐ์ด ๋ญ์ง, ์ด๋ค ๊ฐ์ด return๋๊ธฐ๋ฅผ ๊ธฐ๋ํ  ์ ์๋์ง ์ด๋ฐ Interface๋ฅผ ๋ณด๋ฉด์ ์์ํ  ์ ์๋ค<br/>

๊ทธ๋์ Input๊ณผ output์ด ์ค์ํ๊ณ , function์ ์ด๋ฆ์ด ์ค์ํ ๊ฒ!

## function
ํ๋ก๊ทธ๋จ์ ๊ตฌ์ฑํ๋ ๊ธฐ๋ณธ์ ์ธ ๋น๋ฉ๋ธ๋ญ<br/>
sub program์ด๋ผ๊ณ ๋ ๋ถ๋ฆฌ๋ฉฐ, ์ฌ๋ฌ๋ฒ ์ฌ์ฌ์ฉ์ด ๊ฐ๋ฅํ๋ค<br/>
ํ๊ฐ์ง์ task๋, ์ด๋ค ๊ฐ์ ๊ณ์ฐํ๊ธฐ ์ํด ์ฐ์ฌ์ง<br/>

 ## 1. function declaration
ํจ์๋ฅผ ์ ์ํ๋ ๋ฐฉ๋ฒ!<br/>

```js

function name (param1,param2) { body... return; }

```
function ํค์๋ ์๋ ฅ<br/>
name ์ด๋ฆ ์ง์ <br/>
parameters ๋์ด<br/>
body ํจ์์ ๊ธฐ๋ณธ์  ๋น์ฆ๋์ค ๋ก์ง ์์ฑ<br/>
return<br/><br/><br/>

- ํ๋์ ํจ์๋ ํ๊ฐ์ง์ ์ผ๋ง.
- ๋ณ์ ๋ค์ด๋ฐ์ด ๋ช์ฌ์ด๋ฏ์ด ํจ์ ๋ค์ด๋ฐ์ doSomethingํํ, command ํํ, verb ํํ๋ก
* ๋ง์ฝ ์ด๋ฆ์ง๋๊ฒ ๋๋ฌด ์ด๋ ต๋ค๋ฉด? ๋๋ฌด ๋ง์ ์ผ์ ํ๊ณ ์์ง๋ ์๋์ง ์๊ฐ! *
e.g. createCardAndPoint -> createCard, createPoint๋ก ์ธ๋ถํ<br/><br/>

- function์ JS์์ object๋ก ๊ฐ์ฃผ๋๋ค
๊ทธ๋์ ๋ณ์์ ํ ๋นํ  ์ ์๊ณ , parameter๋ก ์ ๋ฌ์ด ๋๊ณ , ํจ์๋ฅผ returnํ  ์ ์๋ ๊ฒ.<br/>

Type Script )

function log(message:string) {
    console.log(message);
}

TS์์๋ parameter๋, return์ ํ์์ ์ง์ ํ์ง ์์ผ๋ฉด ์ค๋ฅ๊ฐ ๋ฌ๋ค.
- parameter์ ํ์์ (message:string) ์ด๋ ๊ฒ
-return์ ํ์์ (message:string):number์ด๋ ๊ฒ

ํ์์ ๋ช์ํด์ค์ผํจ

* ์ด TS๋,

- ๊ท๋ชจ์๋ ํ๋ก์ ํธ
- ์ฌ๋ฌ ๊ฐ๋ฐ์์ ํ์์ ํ  ๋
- ์ฐ๋ฆฌ๊ฐ ์์ฑํ ๊ฒ์ APIํํ๋ก ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก ์ ๊ณตํด์ผํ  ๋

์์ ๊ฐ์ ์ํฉ์์ ๊ฐ๋ฐ์ ์ํํ๊ฒ ๋ง๋ค์ด์ค๋ค!

: ํจ์์ ์ธํฐํ์ด์ค๋ง ๋ด๋, ์ด ํจ์๊ฐ ๋ญ ํ๋ ํจ์์ด๊ณ  ์ด๋ค ํ๋ผ๋ฏธํฐ๋ฅผ ์ ๋ฌํด์ผํ๊ณ  ์ด๋ค ๋ฐ์ดํฐ ํ์์ธ์ง, ์ด๋ค ๊ฐ์ด ๋ฆฌํด๋๋์ง๋ฅผ ๋ชํํ๊ฒ ์ ์ ์๊ธฐ ๋๋ฌธ์.


 ## 2. Parameters

function์ ์ ๋ฌ๋๋ ์ด parameters๋
- Premitive parameters: passed by value
: ๋ฉ๋ชจ๋ฆฌ์ ๊ทธ๋๋ก ์ ์ฅ๋๊ธฐ ๋๋ฌธ์, value๊ฐ ์ ๋ฌ๋๋ค

- object parameters: passed by reference
: reference๊ฐ ์ ์ฅ๋๊ธฐ ๋๋ฌธ์ reference๊ฐ ์ ๋ฌ๋๋ค

```js

 function changeName(obj) {
   obj.name = 'coder';
 }
 //์ ๋ฌ๋ ๊ฐ์ฒด ์์ name์ ๋ณ๊ฒฝํ๋ ํจ์
 const ellie = { name: 'ellie'};
 changeName(ellie);
 console.log(ellie); //ellie

 ```

object๋ reference๋ก ์ ์ฅ๋จ. ์๋๋ ์์
<img src="/assets/images/JS_object.png" /><br/>

object๋ reference๋ก ์ ๋ฌ๋๊ธฐ ๋๋ฌธ์,<br/>
ํจ์ ์์์ ๊ฐ์ฒด์ ๊ฐ์ ๋ณ๊ฒฝํ๊ฒ ๋๋ฉด ๋ณ๊ฒฝ๋ ์ฌํญ์ด ๊ทธ๋๋ก ๋ฉ๋ชจ๋ฆฌ์ ์ ์ฉ๋๋ค


## 3. Default parameters (added in ES6)
default ๊ฐ์ ๋ฏธ๋ฆฌ ์ง์ ํ  ์ ์๋ default parameters

* ๊ธฐ์กด์ ๋ฐฉ์

```js
function showMessage(message, from) {
  if(from == undefined) {
    from = 'unknown';
  }
  console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```
๊ธฐ์กด์๋ ์ด๋ ๊ฒ, undefined์ผ ๊ฒฝ์ฐ๋ฅผ ๋๋นํด์ ์กฐ๊ฑด๋ฌธ์ ์์ฑํด์ผํ์ง๋ง

* ES6์ ๋ฐฉ์

```js
function showMessage(message, from = 'unknown') {
  console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```

์ฌ์ฉ์๊ฐ parameter๊ฐ์ ์ ๋ฌํ์ง ์์๋, ๊ฐ์ด ์ด๋ ๊ฒ ๊ธฐ๋ณธ๊ฐ์ผ๋ก ๋์ฒด๋์ด์ ์ฌ์ฉ๋๋ค

4. Rest parameters (added in ES6)

```js
function printAll(...args) {
  for(let i = 0; i < args.length; i++) {
    console.log(arg[i]);
  }
}
printAll('dream','coding','ellie'); //์ธ์๋ก ์ธ๊ฐ์ ๊ฐ์ ์ ๋ฌ
```
... ์ด๋ ๊ฒ ์ ๋ฌํ๋ฉด ๋ฐฐ์ด ํํ๋ก ์ ๋ฌ์ด ๋๋ค!<br/>
'dream','coding','ellie' ์ด๋ ๊ฒ ์ ๋ฌ๋ฐ์ ๊ฐ์ ์ธ๊ฐ์ ๊ฐ์ด ๋ด๊ธด ๋ฐฐ์ด์ด ๋๋ค<br/>

```js
function printAll(...args) {
    for(const arg of args) {
    console.log(arg);
  }
}
printAll('dream','coding','ellie'); //์ธ์๋ก ์ธ๊ฐ์ ๊ฐ์ ์ ๋ฌ
```
for๋ฌธ๋ณด๋ค ๊ฐ๋จํ for of๋ฌธ์ผ๋ก ์์ฑํ  ์๋ ์์ <br/>
arg์ ์๋ ๋ชจ๋  ๊ฐ๋ค์ด, ์ฐจ๋ก๋๋ก ํ๋์ฉ arg๋ก ์ง์ ์ด ๋๋ฉด์ ์ถ๋ ฅํ๊ฒ ๋๋ค

```js
function printAll(...args) {
    args.forEach((arg) => console.log(arg));
  }
}
printAll('dream','coding','ellie'); //์ธ์๋ก ์ธ๊ฐ์ ๊ฐ์ ์ ๋ฌ
```


## 5. Local scope

์ฐธ์กฐ) closer, LexicalEnvironment <br/>

* ๋ฐ์์๋ ์์ด ๋ณด์ด์ง ์๊ณ , ์์์๋ง ๋ฐ์ ๋ณผ ์ ์๋ค

์ด๊ฒ์ด scope์ ๊ฐ๋

```js
let globalMessage = 'global'; // global variable ์ ์ญ๋ณ์
function printMessage() {
  let message = 'hello';
  console.log(message); // lacal variable ์ง์ญ๋ณ์
  console.log(globalMessage);

  function printAnother() {
    let childMessage = 'hello';
  }
  // console.log(childMessage) //error
}
printMessage();
```

์์์ ๋ถ๋ชจ์๊ฒ์ ์ ์๋ ๋ฉ์์ง๋ฅผ ํ์ธํ  ์ ์๋ค์ง๋ง <br/>
์์ ์์ ์ ์๋ childMessage๋ฅผ ๋ถ๋ชจ์์ ๋ณผ ์ ์์

* ์ค์ฒฉ๋ ํจ์์์ ์์์ ํจ์๊ฐ, ๋ถ๋ชจ ํจ์์ ์ ์๋ ๋ณ์์ ์ ๊ทผ์ด ๊ฐ๋ฅํ ๊ฒ๋ค์ด ๋ฐ๋ก closer.



## 6. Return a value

```js
function sum(a, b) {
  return a + b;
  }
  const result = sum(1,2); //3
  console.log(`sum: ${sum(1,2)}`);
```

parameters๋ก ๊ฐ์ ์ ๋ฌ ๋ฐ์์, ๊ณ์ฐ๋ ๊ฐ์ returnํ  ์ ์๋ค

```js
let globalMessage = 'global';
function printMessage() {
  let message = 'hello';
  console.log(message);
  console.log(globalMessage);

  function printAnother() {
    let childMessage = 'hello';
  }
   return undefined;
}
printMessage();
```

์๊น ๋ดค๋, ์ด๋ ๊ฒ return์ด ์๋ ํจ์๋ค์ return undefined๊ฐ ๋ ๊ฒ๊ณผ ๊ฐ๋ค<br/>
๋ชจ๋  ํจ์๋ return undefined์ด๊ฑฐ๋, ๊ฐ์ Returnํ  ์ ์๋ค


## 7. Early return, early exit

* ๋์ ์!

```js
Function upgraderUser(user) {
  if(user.point > 10) {
    //long upgrade logic
  }
}
```
ํด๋น ์กฐ๊ฑด์ผ ๋์๋ง ๋ฌด์ธ๊ฐ ์๋ํ๋ ๋ก์ง์ด ์๋ค. block์์์ ๋ก์ง์ ๋ง์ด ์์ฑํ๋ฉด ๊ฐ๋์ฑ์ด ๋จ์ด์ง๋ค.

* ์ข์ ์!

```js
Function upgraderUser(user) {
  if(user.point <= 10) {
    return;
  }
    //long upgrade logic
}
```
if else๋ฅผ ๋ฒ๊ฐ์์ ์ฐ๋ ๊ตฌ์กฐ๋ณด๋ค๋, ์กฐ๊ฑด์ด ๋ง์ง ์์ ๋ ์ด๋ ๊ฒ ๋นจ๋ฆฌ return ์์ผ๋ฒ๋ฆฌ๊ณ !<br/> 
์กฐ๊ฑด์ด ๋ง์ ๋๋ง ๊ทธ ๋ค์์ผ๋ก ์์ ํ์ํ ๋ก์ง๋ค์ ์ญ ์คํํ๋ ๊ตฌ์กฐ๊ฐ ์ข๋ค.

- ์กฐ๊ฑด์ด ๋ง์ง ์๋ ๊ฒฝ์ฐ
- ๊ฐ์ด undefined์ธ ๊ฒฝ์ฐ
- ๊ฐ์ด -1์ธ ๊ฒฝ์ฐ




