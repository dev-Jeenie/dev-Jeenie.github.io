---
title: "# 04. Operator,if,for loop ๐น"
permalink: /js1/JavascriptOperators
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-15
last_modified_at: 2021-10-15
---

![]()

# operator
1. string concatenation

```js
console.log('my'+' cat');
console.log('1'+2);  //12
console.log(`string literals : 1 + 2 = ${1 + 2}`);
```

+ ๊ธฐํธ๋ฅผ ์ด์ฉํด์ ๋ฌธ์์ด์ ํฉ์น  ์ ์๋ค

๋ฌธ์์ด+๋ฌธ์์ด = ๋ฌธ์์ด ์ถ๋ ฅ
๋ฌธ์์ด+์ซ์ = (์ซ์๋ฅผ ๋ฌธ์์ด ํ)๋ฌธ์์ด ์ถ๋ ฅ

` ` ๋ฐฑํฑ์ผ๋ก string literals์ ๋ง๋ค ์ ์๋ค.
์ค๊ฐ์ ๋ณ์๊ฐ ์ฝ์๋๋ฉด ๊ณ์ฐํด์ ๋ฌธ์์ด๋ก ๋๋ ค์ค๋ค
์ค๋ฐ๊ฟ์ด๋ ํน์๊ธฐํธ๋ ๊ทธ๋๋ก ์ถ๋ ฅ์ด ๊ฐ๋ฅ
(์ฑ๊ธ์ฟผํธ ' ' ์ ์ฌ์ด์ '๋ฅผ ๋ฃ์ ๋๋ \' ๋ฐฑ์ฌ๋ฌ์๋ฅผ ๋ฃ์ด์ผ๋ง ํ๋ค)

2. Numeric operators
```js
console.log(1 + 1); //add
console.log(1 - 1); //substract
console.log(1 / 1); //divide
console.log(1 * 1); //multiply
console.log(5 % 2); //reminder ๋๋๊ณ  ๋๋จธ์ง
console.log(2 ** 3); //exponentiation 2์ 3์น

```

3. Increment and decrement operators

```js
let counter = 2;

const preIncrement = ++counter;
// ์ ์ฝ๋๋ ์๋์ ๋์ผํ๋ค
//couter = counter + 1;
//preIncrement = counter;
// counter์ 1์ ๋ํด์ ๊ฐ์ ๋ค์ counter์ ํ ๋นํ ๋ค์์ preIncrement์ counter์ ๊ฐ์ ํ ๋นํ๋ค

console.log(preIncrement, counter);
// 3,3 ์ถ๋ ฅ

const postIncrement = counter++;
// ์ ์ฝ๋๋ ์๋์ ๋์ผํ๋ค
// postIncrement = counter;
counter = counter + 1;
// postIncrement์ counter์ ๊ฐ์ ํ ๋นํ ๋ค์, counter์ 1์ ๋ํด์ ๊ฐ์ ๋ค์ counter์ ํ ๋นํ๋ค
console.log(postIncrement, counter);
// 3,4 ์ถ๋ ฅ

```



4. Assignment operators
```js
let x = 3;
let y = 6;
x += y; // x = x + y;
x -= y;
x *= y;
x /= y;
```

5. Comparison operators
```js
console.log(10 < 6);
console.log(10 <= 6);
console.log(10 > 6);
console.log(10 >= 6);
```

6. logical operators : ใฃใฃ(or) , &&(and) , !(not)

```js

const value1 = false;
const value2 = 4 < 2;

console.log(`or: ${ value1 ใฃใฃvalue2ใฃใฃcheck() }`); //or : true

console.log(`and: ${ value1 && value2 && check() }`); //and : false

function check() {
for (let i = 0; i < 10; i++) {
console.log('print')
};
return true;
}

```

- or : finds the first truthy value

์ฒ์์ผ๋ก true๊ฐ ๋์ค๋ฉด ๊ฑฐ๊ธฐ์ ๋ฉ์ถ๋ค.
๋ง์ฝ value1์ด true๋ผ๋ฉด ๋ค๊ฐ ๋ญ๋  ์๊ด์์.
๊ทธ๋ฌ๋๊น check๊ฐ์ expression์ ์ ์ผ ์์ ๋๋ฉด ์๋จ. 

=> ๊ฐ๋จํ value๋ค์ ์ ์ผ ์์๋ฌ์ ๊ฑ๋ค์ด false์ผ๋๋ง ๋ง์ง๋ง์ ๋ง์ง๋ชปํด ํธ์ถํ๋๊ฒ ์ ์ผ ์ข๋ค.

- and : finds the first falsy value
๋ชจ๋ true์ผ ๋๋ง true๋ฅผ ๋ฆฌํดํ๋ค.
or๊ณผ ๋ง์ฐฌ๊ฐ์ง๋ก ์์ value๊ฐ false๋ผ๋ฉด ๊ฑฐ๊ธฐ์ ๋ฉ์ถ๋ค. ๋ค๊ฐ ๋ญ๋  ์๊ด์์ด ์์ ์คํ์กฐ์ฐจ ํ์ง ์์

=> <strong>and๋ํ heavyํ operation์ผ์๋ก ์ ์ผ ์์์ ์ฒดํฌํ๋ ๊ฒ์ด ์ข๋ค</strong>

<strong style="color:blue"> offen used to compress long if-statement </strong>
<strong style="color:blue"> ์ด๋ฌํ ์์ฑ ๋๋ฌธ์, null ์ฒดํฌ๋ฌธ์ผ๋ก ์ฌ์ฉ๋๋ค </strong>

```js
nullableObject && nullableObject.something
```

* ๋งจ ์ฒ์์ด false๋ผ๋ฉด ๋ค๋ฅผ ์คํ์กฐ์ฐจ ํ์ง์๋ ์์ฑ์ ์ด์ฉํ ๊ฐ๋จํ null์ฒดํฌ๋ฌธ.
* nullableObject๊ฐ null์ด ๋ค์ด์ค๋ฉด false์ด๊ธฐ ๋๋ฌธ์, ๋ค๊ฐ ์คํ๋์ง ์๋๋ค!

- not : !

```js
console.log(!value1);
```
๊ฐ์ ๋ฐ๋๋ก ๋ฐ๊ฟ์ค๋ค

7. Equality

```js
const stringFive = '5';
const numberFive = 5;

// loose equality, with type conversion
console.log(stringFive == numberFive); // true
console.log(stringFive != numberFive); // false

// string equality, no type conversion
console.log(stringFive === numberFive); // false
console.log(stringFive !== numberFive); // true
```
- == / !== loose equality
: ํ์์ ๋ณ๊ฒฝํด์ ๊ฐ์ ๋น๊ตํ๋ค

- === / !=== strick equality
: ํ์์ ์์ํด์ ๊ฐ์ ๋น๊ตํ๋ค

* object equality by reference

```js
const ellie1 = { name : 'ellie' };
const ellie2 = { name : 'ellie' };
const ellie3 = ellie1;

console.log(ellie1 == ellie2); // false
console.log(ellie1 === ellie2); // false
console.log(ellie1 === ellie2);// true
```
object๋ ๋ฉ๋ชจ๋ฆฌ์ ํ์ฌ๋  ๋, reference ํํ๋ก ์ ์ฅ๋๋ค<br/>
<img src="/assets/images/JS_object.png" /><br/>

object ellie1๊ณผ ellie2๋ ๋ค์ด์๋ ๊ฐ์ ๊ฐ์๋ณด์ด์ง๋ง, <br/>
์ค์ ๋ก 1๊ณผ 2์๋ <strong>๊ฐ๊ฐ ๋ค๋ฅธ ๋ ํผ๋ฐ์ค๊ฐ ์ ์ฅ</strong>๋์ด์์ <br/>
๊ทธ ๋ค๋ฅธ ๋ ํผ๋ฐ์ค๋, ์๋ก ๋ค๋ฅธ object๋ฅผ ๊ฐ๋ฆฌํค๊ณ  ์๋ค<br/>
ellie3๋ ellie1๊ณผ ๋์ผํ ๋ ํผ๋ฐ์ค๋ฅผ ๊ฐ๋ฆฌํค๊ณ  ์์.<br/><br/>

๊ทธ๋์ ellie1๊ณผ ellie2๋ ํ์์ ๋์ผํ๊ฒ ๋ณธ๋๋ <strong>๋ ํผ๋ฐ์ค๊ฐ ๋ค๋ฅด๊ธฐ ๋๋ฌธ์</strong> ๊ฐ์ง ์๋ค!<br/>
ํ์์ ์์ํด์ ๋น๊ตํด๋ ๋ง์ฐฌ๊ฐ์ง๋ก <strong>๋ ํผ๋ฐ์ค๊ฐ ๋ค๋ฅด๊ธฐ ๋๋ฌธ์</strong> ๊ฐ์ง ์์.<br/>
ํ์ง๋ง ellie3๊ณผ ellie1๋ <strong>๋์ผํ ๋ ํผ๋ฐ์ค์ด๊ธฐ ๋๋ฌธ์</strong> ๊ฐ๋ค!

* equality puzzler *

```js
console.log(0 == false); // true
console.log(0 === false); // false 0์ boolean์ด ์๋๋ค
console.log('' == false); // true empty๋ฌธ์์ด์ false์ด๋ค
console.log('' === false); // false empty ๋ฌธ์์ด์ boolean์ด ์๋๋ค
console.log(null == undefined); //true null๊ณผ undefined์ ๊ฐ๋ค (ํน์ดํ๊ฒ๋)
console.log(null === undefined); //false null๊ณผ undefined๋ ๋ค๋ฅธ ํ์์ด๋ค
```

8. Conditional operator: if
//if,else,lf,else

```js
const name = 'ellie';
if(name === 'ellie') {
  console.log('Welcome, Ellie!');
}else if(name === 'coder') {
  console.log('You are amazing coder');
}else {
  console.log('unknown');
}
```
if statement๊ฐ true๋ผ๋ฉด, ๊ทธ ์์ ์๋ block์ ์คํํ๊ฒ ๋๋ค<br/>
๊ทธ๊ฒ ์๋๋ผ๋ฉด else if, ๊ทธ๊ฒ๋ ์๋๋ผ๋ฉด else๋ก ๋์ด์์ block์ ์คํํ๋ค

9. Ternary operator: ?
//condition ? value1 : value2;

```js
console.log(name === 'ellie' ? 'yes' : 'no');
```
๊ธธ์ด์ง๋ฉด ๊ฐ๋์ฑ์ด ๋จ์ด์ง๊ธฐ ๋๋ฌธ์, ์กฐ๊ฑด๋ฌธ์ด ๊ฐ๋จํ  ๋์๋ง ์ฌ์ฉํ๋ ๊ฒ์ด ์ข๋ค.

10. Switch statement
use for multiple if checks
use for enum-like value check
use for multiple type checks in TS

```js
const browser = 'IE';

switch (browser) {
  case 'IE':
    console.log('go away!');
    break;
  // case 'Chrome':
  //   console.log('love you!');
  //   break;
  // case 'FireFox':
  //   console.log('love you!');
  //   break;
  case 'Chrome':
  case 'FireFox':
    console.log('love you!');
    break;
  default:
    console.log('love you!');
    break;
}
```
<strong>if๋ฌธ์์ else if๋ฅผ ๋ฐ๋ณตํ๋ค๋ฉด switch๋ฅผ ์ฐ๋ ๊ฒ์ ๊ณ ๋ คํ๋ ๊ฒ ์ข๋ค!</strong>

๋ง์ฝ ์คํํ  ๋์์ด ๊ฐ์ ๊ฒฝ์ฐ์ case๋ฅผ ์ฐ๋ฌ์ ์ฐ๋ฉด ๋๋ค<br/>

TS์์ ์ ํด์ ธ์๋ ํ์์ ๊ฒ์ฌํ  ๋์ switch๋ฅผ ์ฐ๋ ๊ฒ์ด ๊ฐ๋์ฑ์ด ์ข๋ค<br/>

11. Loops
- while
while loop, while the condition is truthy,
body code is executed.

```js
let i = 3;
while (i > 0) {
  console.log(`while: ${i}`);
  i--;
}
```

while์ statement๊ฐ false๋ก ๋์ค๊ธฐ ์ ๊น์ง๋ ๋ฌดํ๋๋ก ๋ฐ๋ณตํด์ ๊ณ์ ๋๋ค.<br/>

- do while
do while loop, body code is excuted first,
then check the condition.

```js
do {
  console.log(`do while: ${i}`);
  i--;
}while (i > 0);
```

๋จผ์  ๋ธ๋ญ์ ์คํํ ํ์ ์กฐ๊ฑด์ ๊ฒ์ฌํ๋ค.

=> ๋ธ๋ญ์ ๋จผ์  ์คํํ๊ณ  ์ถ๋ค๋ฉด do while, <br/>
์กฐ๊ฑด์ ๋ง์ ๋์๋ง ๋ธ๋ญ์ ์คํํ๊ณ  ์ถ๋ค๋ฉด while์ ์จ์ผํ๋ค!

- for
for loop, for(begin; condition; step)

```js
for (i = 3; i > 0; i--) {
  console.log(`for: ${i}`);
}
```
for์ ์์ํ๋ ๋ฌธ์ฅ, ์ปจ๋์, ์ด๋ค ์คํ์ ๋ฐ์ ๊ฒ์ธ์ง๋ฅผ ๋ช์ํ๋ค<br/>
1) begin์ ์ฒ์์ ๋ฑ ํ๋ฒ๋ง ์คํํ๊ณ  <br/>
2) ๋ธ๋ญ์ ์คํํ๊ธฐ ์ ์ ์ปจ๋์์ด ๋ง๋์ง ๊ฒ์ฌํ ๋ค์ <br/>
3) ๋ธ๋ญ์ ์คํํ๊ณ  <br/>
4) ์คํ์ ์คํํ๋ค <br/>

=> ์ปจ๋์์ด ๋ง์ ๋์ 2,3,4๋ฅผ ๋ฐ๋ณตํ๋ค <br/>

์ด for๋ฌธ์ฒ๋ผ ๊ธฐ์กด์ ์กด์ฌํ๋ ๋ณ์์ ๊ฐ์ ํ ๋นํ๋ ๊ฒฝ์ฐ๋ ์๊ณ <br/>

```js
for (let i = 3; i > 0; i = i - 2) {
  // inline variable declaration
  console.log(`inline variable for: ${i}`);
}
```

์ด๋ ๊ฒ for์์์, block์์ let์ผ๋ก ์ง์ญ๋ณ์๋ฅผ ์ ์ธํด์ ์์ฑํ  ์๋ ์๋ค. <br/>

<strong>nested loops</strong>

* while๊ณผ for์ nested loops์ด ๊ฐ๋ฅํ๋ค <br/>

```js
for (let i = 0; i < 10; i++) {
  for (let j = 0; i < 10; i++) {
    console.log(`i: ${i}, j: ${j}`);
  }
}
```

for๋ฌธ ์์ for๋ฌธ์ ์์
1) i๊ฐ 0์ผ ๋, j๋ 0~9๊น์ง ๋ฐ๋ณต๋๊ณ <br/>
2) i๊ฐ 1์ผ ๋, j๋ 0~9๊น์ง ๋ฐ๋ณต๋๊ณ <br/>
.....<br/>
ex)๊ตฌ๊ตฌ๋จ<br/>


* break, continue<br/>
loop ์์์๋ break์ continue๋ฅผ ์ด์ฉํด ๋ฃจํ๋ฅผ ๋๋ผ ์ ์๋ค!<br/>

- break
: ๋ฃจํ๋ฅผ ์์ ํ ๋๋
- continue
: ์ง๊ธ ๊ฒ๋ง ์คํตํ๊ณ , ๋ค์ ์คํ์ผ๋ก ๋์ด๊ฐ<br/>

Q1. iterate from 0 to 10 and print only even numbers (use continue)<br/>

```js

for(let i = 0; i < 11; i++) {
  if(i % 2 !== 0) {
    continue;
    // 2๋ก ๋๋ด์ ๋ 0์ด ์๋๋ฉด ์คํตํ๊ณ  ๋ค์ ์คํ์ผ๋ก
  }
    console.log(`even number is : ${i}`)
}
// ์ค๋ฌด์ ์ธ ๋ต :
// for(let i = 0; i < 11; i++) {
//   if(i % 2 == 0 && i > 0) {
//       console.log(`even number is : ${i}`)
//   }
// }

```
<br/>

Q2. iterate from 0 to 10 and print numbers until reaching 8 (use break)<br/>

```js

for(let i = 0; i < 11; i++) {
  if(i == 8){
    break;
  }
  console.log(`number is : ${i}`);
}

```
<br/><br/><br/><br/><br/><br/>


