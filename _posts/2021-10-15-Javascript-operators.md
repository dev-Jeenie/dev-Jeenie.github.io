---
title: "# 04. Operator,if,for loop 🎹"
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

+ 기호를 이용해서 문자열을 합칠 수 있다

문자열+문자열 = 문자열 출력
문자열+숫자 = (숫자를 문자열 화)문자열 출력

` ` 백틱으로 string literals을 만들 수 있다.
중간에 변수가 삽입되면 계산해서 문자열로 돌려준다
줄바꿈이나 특수기호도 그대로 출력이 가능
(싱글쿼트 ' ' 의 사이에 '를 넣을 때는 \' 백슬러시를 넣어야만 한다)

2. Numeric operators
```js
console.log(1 + 1); //add
console.log(1 - 1); //substract
console.log(1 / 1); //divide
console.log(1 * 1); //multiply
console.log(5 % 2); //reminder 나누고 나머지
console.log(2 ** 3); //exponentiation 2의 3승

```

3. Increment and decrement operators

```js
let counter = 2;

const preIncrement = ++counter;
// 위 코드는 아래와 동일하다
//couter = counter + 1;
//preIncrement = counter;
// counter에 1을 더해서 값을 다시 counter에 할당한 다음에 preIncrement에 counter의 값을 할당한다

console.log(preIncrement, counter);
// 3,3 출력

const postIncrement = counter++;
// 위 코드는 아래와 동일하다
// postIncrement = counter;
counter = counter + 1;
// postIncrement에 counter의 값을 할당한 뒤에, counter에 1을 더해서 값을 다시 counter에 할당한다
console.log(postIncrement, counter);
// 3,4 출력

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

6. logical operators : ㅣㅣ(or) , &&(and) , !(not)

```js

const value1 = false;
const value2 = 4 < 2;

console.log(`or: ${ value1 ㅣㅣvalue2ㅣㅣcheck() }`); //or : true

console.log(`and: ${ value1 && value2 && check() }`); //and : false

function check() {
for (let i = 0; i < 10; i++) {
console.log('print')
};
return true;
}

```

- or : finds the first truthy value

처음으로 true가 나오면 거기서 멈춘다.
만약 value1이 true라면 뒤가 뭐든 상관없음.
그러니까 check같은 expression을 제일 앞에 두면 안됨. 

=> 간단한 value들을 제일 앞에둬서 걔들이 false일때만 마지막에 마지못해 호출하는게 제일 좋다.

- and : finds the first falsy value
모두 true일 때만 true를 리턴한다.
or과 마찬가지로 앞의 value가 false라면 거기서 멈춘다. 뒤가 뭐든 상관없이 아예 실행조차 하지 않음

=> <strong>and또한 heavy한 operation일수록 제일 앞에서 체크하는 것이 좋다</strong>

<strong style="color:blue"> offen used to compress long if-statement </strong>
<strong style="color:blue"> 이러한 속성 때문에, null 체크문으로 사용된다 </strong>

```js
nullableObject && nullableObject.something
```

* 맨 처음이 false라면 뒤를 실행조차 하지않는 속성을 이용한 간단한 null체크문.
* nullableObject가 null이 들어오면 false이기 때문에, 뒤가 실행되지 않는다!

- not : !

```js
console.log(!value1);
```
값을 반대로 바꿔준다

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
: 타입을 변경해서 값을 비교한다

- === / !=== strick equality
: 타입을 엄수해서 값을 비교한다

* object equality by reference

```js
const ellie1 = { name : 'ellie' };
const ellie2 = { name : 'ellie' };
const ellie3 = ellie1;

console.log(ellie1 == ellie2); // false
console.log(ellie1 === ellie2); // false
console.log(ellie1 === ellie2);// true
```
object는 메모리에 탑재될 때, reference 형태로 저장된다<br/>
<img src="/assets/images/JS_object.png" /><br/>

object ellie1과 ellie2는 들어있는 값은 같아보이지만, <br/>
실제로 1과 2에는 <strong>각각 다른 레퍼런스가 저장</strong>되어있음 <br/>
그 다른 레퍼런스는, 서로 다른 object를 가리키고 있다<br/>
ellie3는 ellie1과 동일한 레퍼런스를 가리키고 있음.<br/><br/>

그래서 ellie1과 ellie2는 타입을 동일하게 본대도 <strong>레퍼런스가 다르기 때문에</strong> 같지 않다!<br/>
타입을 엄수해서 비교해도 마찬가지로 <strong>레퍼런스가 다르기 때문에</strong> 같지 않음.<br/>
하지만 ellie3과 ellie1는 <strong>동일한 레퍼런스이기 때문에</strong> 같다!

* equality puzzler *

```js
console.log(0 == false); // true
console.log(0 === false); // false 0은 boolean이 아니다
console.log('' == false); // true empty문자열은 false이다
console.log('' === false); // false empty 문자열은 boolean이 아니다
console.log(null == undefined); //true null과 undefined은 같다 (특이하게도)
console.log(null === undefined); //false null과 undefined는 다른 타입이다
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
if statement가 true라면, 그 안에 있는 block을 실행하게 된다<br/>
그게 아니라면 else if, 그것도 아니라면 else로 넘어와서 block을 실행한다

9. Ternary operator: ?
//condition ? value1 : value2;

```js
console.log(name === 'ellie' ? 'yes' : 'no');
```
길어지면 가독성이 떨어지기 때문에, 조건문이 간단할 때에만 사용하는 것이 좋다.

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
<strong>if문에서 else if를 반복한다면 switch를 쓰는 것을 고려하는 게 좋다!</strong>

만약 실행할 동작이 같은 경우엔 case를 연달아 쓰면 된다<br/>

TS에서 정해져있는 타입을 검사할 때에 switch를 쓰는 것이 가독성이 좋다<br/>

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

while의 statement가 false로 나오기 전까지는 무한대로 반복해서 계속 돈다.<br/>

- do while
do while loop, body code is excuted first,
then check the condition.

```js
do {
  console.log(`do while: ${i}`);
  i--;
}while (i > 0);
```

먼저 블럭을 실행한 후에 조건을 검사한다.

=> 블럭을 먼저 실행하고 싶다면 do while, <br/>
조건에 맞을 때에만 블럭을 실행하고 싶다면 while을 써야한다!

- for
for loop, for(begin; condition; step)

```js
for (i = 3; i > 0; i--) {
  console.log(`for: ${i}`);
}
```
for은 시작하는 문장, 컨디션, 어떤 스텝을 밟을 것인지를 명시한다<br/>
1) begin을 처음에 딱 한번만 실행하고 <br/>
2) 블럭을 실행하기 전에 컨디션이 맞는지 검사한 다음 <br/>
3) 블럭을 실행하고 <br/>
4) 스텝을 실행한다 <br/>

=> 컨디션이 맞을 동안 2,3,4를 반복한다 <br/>

이 for문처럼 기존에 존재하는 변수의 값을 할당하는 경우도 있고<br/>

```js
for (let i = 3; i > 0; i = i - 2) {
  // inline variable declaration
  console.log(`inline variable for: ${i}`);
}
```

이렇게 for안에서, block안에 let으로 지역변수를 선언해서 작성할 수도 있다. <br/>

<strong>nested loops</strong>

* while과 for은 nested loops이 가능하다 <br/>

```js
for (let i = 0; i < 10; i++) {
  for (let j = 0; i < 10; i++) {
    console.log(`i: ${i}, j: ${j}`);
  }
}
```

for문 속의 for문의 순서
1) i가 0일 때, j는 0~9까지 반복되고<br/>
2) i가 1일 때, j는 0~9까지 반복되고<br/>
.....<br/>
ex)구구단<br/>


* break, continue<br/>
loop 안에서는 break와 continue를 이용해 루프를 끝낼 수 있다!<br/>

- break
: 루프를 완전히 끝냄
- continue
: 지금 것만 스킵하고, 다음 스텝으로 넘어감<br/>

Q1. iterate from 0 to 10 and print only even numbers (use continue)<br/>

```js

for(let i = 0; i < 11; i++) {
  if(i % 2 !== 0) {
    continue;
    // 2로 나눴을 때 0이 아니면 스킵하고 다음 스텝으로
  }
    console.log(`even number is : ${i}`)
}
// 실무적인 답 :
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


