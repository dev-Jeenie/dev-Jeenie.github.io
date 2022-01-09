---
title: "Java script ES6💫 제대로 알아보기! ✍️ (1) Block Scope"
permalink: /cs/javascriptEs61
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-09
last_modified_at: 2022-01-09
---

![]()

## 1. scope란?

**용어 정의**

- Scope란?
	: 범위, 유효공간, 살 수 있는 공간, 허용되던, 허용범위 …

- 함수 스코프
	: 함수에 의해서 생기는 범위, 변수의 유효범위

- 블락 스코프(Block scope)
	: 블록에 의해 생기는 유효범위

**예제**

```JS
{
	let a = 10
	{
		let a =20
		console.log(a) // 20
	}
	console.log(a) // 10
}
	console.log(a) // error! a is not defined
```

=> 이렇게 `{ }` 에 의해서 **`변수의 유효범위 결정`**되는 것이 바로 블록 스코프!

## 2. block scope의 유효범위

하지만 이 block scope는,
`let/const`로 선언했을 경우와 `var`로 선언했을 경우가 유효범위가 다르다!

### 2-1. `let`으로 선언했을 경우

```JS
function hasValue(p) {
	console.log(v) // error! v is not undefined
	if (p) {
		let v = 'blue'
		console.log(v)
	}else {
		let v = 'red'
		console.log(v)
	}
	console.log(v)
}
hasValue(10) // error! v is not undefined

```


### 2-2. `var`로 선언했을 경우

```JS
function hasValue(p) {
	console.log(v) // undefined
	if (p) {
		var v = 'blue'
		console.log(v) // blue
	}else {
		var v = 'red'
		console.log(v)
	}
	console.log(v) // blue
}
hasValue(10)

```

`var`로 선언한 변수는 **block scope의 영향을 `받지 않는다`**!

=> block scope는 `let과 const에 대해서만` 동작한다.



## 3. Hoisting

그렇다면 block scope는 `hoisting`을 할까?

그 전에 알고가야할 정의!<br/>
모든 데이터는 크게 세가지로 나뉜다.
`문`, `식`, `값`
(여기서 식과 값은 동일한 것으로 간주된다)

**데이터의 분류**
- `~문` (문단)
	- if**문**, for**문**, while**문**, swith-case**문**
- `식` (expression)
	- `값`이 될 수 있는 경우
	- 10 + 20, 'abc' + 'def'(abcdef라는 문자열인 값이 된다)
	- a() 이렇게 함수가 있을 때 그 함수를 호출한 것 또한 식.
- `값`
	- 값과 식은 동일한 것으로 간주됨

**`문`과 `식`의 차이**
- `문`은 **결과를 리턴하지 않는다**! 결과가 존재할 수 없음.
- if문이 끝났다고 해도 그 if문의 결과를 어디에 담아둘 수 없다.
그냥 그 안에있는 구문을 실행하고 끝이다.
for문 또한 반복을 끝내고 그 결과를 넣어주는 부분은 어디에도 없음. 그냥 다음으로 넘어감
while문과 switch-case도 이 안에 있는 내용을 실행하고 끝.

=> <strong style="color:black;background-color:yellow">문 자체가 하나의 block scope<srtong>가 된다.


그래서 scope가 두개.
1. 함수 스코프
2. block 스코프

```JS
// 아이패드에 정리한 부분 붙이기
```

위에서 찾지 않고 에러(undefined였나?)가 난 이유?
Temporal Dead Zone(TDZ : 임시 사망지역, 임시 사각지대)
정식명칭은 아니지만 널리 통용되는 명칭.<br/>
이 구간에서는 레퍼런스 에러가 나와야한다

let이나 const에 대해서,
실제로 선언한 곳에 오기 전까지는 이 변수를 호출할 수 없다.

**기존 자바스크립트의 문제점**
- 가장 주의해야했던 점
	- `Hoisting`

```JS
console.log(a) // 이쪽에서 많은 일을 처리함

var a = 10; // 그런데 선언은 여기서 함
```

개발자의 의지로 변수를 만들고, 그 변수로 어떤 처리를 하기 위해서는
위에서부터 아래로 내려가야함!

하지만 소스코드의 길이가 너무 길 경우 등의 문제로,
실수로 밑에서 선언한 변수를 위에서 처리한다면
어떠한 오류도 생기지 않고 넘어간다.
(이것 때문에 자바스크립트는 디버깅이 어렵다는 말이 나오는 것.)

에러가 안나는 게 좋은 것이 아니고,
에러가 나서 고칠 수 있어야 좋은 것!


es6의 철학은,
- 암묵적인 암기사항을 최대한 배제할 것
- 하지만 기존의 기능은 유지할 것

그래서
- **"`함수` 선언보다 이른 호출"**과 **`var`로 선언한 변수의 선언보다 이른 호출**은 hoisting이 가능하고
- **`let`과 `const`로 선언한 변수의 선언보다 이른 호출**은 hoisting이 불가능한 것.

=> undefined가 뜬 이유?
hoisting해서 undefined가 할당됐기 때문에.
block scope가 아닌 함수 scope로 봐도 마찬가지.


## 3-1. 기존과 es6의 호이스팅 비교

**기존 `var`**
-  변수명만 위로 끌어올리고 / undefined 할당(값이 없으니 그냥 undefined로 인식하게끔 구성되어있음)

```JS
if (true) {
	vqr a = 10
	if (true) {
		console.log(a) // undefined
		var a = 20
	}
	console.log(a)
}
console.log(a)

```
- (1) 변수명을 위로 끌어올리고
- (2) undefined를 할당

**`let`과 `const`**
-  변수명만 위로 끌어올리고 / 끝!


그럼 여기서 reference error가 왜 나오느냐!
=> 바로 hoisting이 됐기 때문!

```JS
if (true) {
	let a = 10
	if (true) {
		console.log(a) // reference error: a is not defined.
		const a = 20
		console.log(a) // 20
	}
	console.log(a)
}
console.log(a)

```

- (1) 변수명을 위로 끌어올리고 끝.

<strong style="color:black;background-color:yellow">⭐️hoisting을 하지 않는다고 생각하면 안됨!⭐️</strong>

hoisting이 안됐으면 위에 있는 변수를 찾아서 10을 출력했어야함.<br/>
block scope에 대한 **실행 컨텍스트가 열리는 순간**에,<br/>
const <strong style="color:black;background-color:yellow">a를 hoisting을 했다.</strong><br/>
그래서 a의 존재를 알고있다.(아까 두번째 필기도, 존재를 모르고있는 것이 맞음)<br/>
다만 var와 다른점은, <br/><strong style="color:black;background-color:yellow">undefined를 할당하지 않는다</strong>는 것!<br/>

let과 const로 선언한 변수를 hoisting할 경우, 그 변수명과 어떤 값이 매칭되어있지 않다.<br/>
그 상태에서는 a가 가진 어떤 값을 꺼내올 수 없음.<br/>
그래서 **reference error: a is not defined.** 오류가 뜨는 것.





## 4. this

```JS
var value = 0;
var obj = {
	value: 1,
	setValue: function () {
		this.value = 2
		(function () {
			this.value = 3
		})()
	}
}
```
- (1) 변수 obj에 객체를 만들었는데,
- (2) 객체의 value라는 property에는 1이 들어가있음.
- (3) setValue라는 메소드에는 함수의 내부에서 this.value에서는 2를 넣고 있고,
- (4) 다시 함수 내부에서 this.value에서는 3을 넣고 있다.


```JS
var value = 0;
var obj = {
	value: 1,
	setValue: function () {
		this.value = 2 // obj의 value 값 변경

		(function () {
			this.value = 3 // 문제. 이때의 this는?
		})()

	}
}
obj.setValue() // 메소드로 호출
console.log(value)
console.log(obj.value)
```
- obj.setValue()
	- **메소드로 호출**했기 때문에, 이때의 this는` . 앞의 객체`!
-	this.value = 2
	- this는 obj이고, 그래서 obj의 value는 2가 된다
- this.value = 3
	- 문제. 이때의 this는?
	- `window`. **window.value가 3**이 된다.
	
**갑자기 window가 왜 나와???**
- 왜냐하면, function은 **method가 아닌 `함수를 바로 실행`**한 것.

함수를 실행했을 때 그 `함수의 this`는 <strong style="color:black;background-color:yellow">전역객체를 보게된다</strong>.

<img src="/assets/images/es6-this.jpeg" /><br/>

=> **결론**<br/>
`method`로 호출했을 때의 this는 `.앞의 객체`를 가리킴<br/>
`함수`로 호출했을 때의 this는 `window`를 가리킴<br/>

## 4-1. 헷갈리는 this를 통일하는 방법

method로 호출한 this와 함수로 호출한 this를 통일하고 싶다...

- 1) **this를 변수에** 담는 방법

```JS
var value = 0;
var obj = {
	value: 1,
	setValue: function () {
		this.value = 2;
		var self = this;
		(function () {
			self.value = 3;
		})()

	}
}
obj.setValue();
console.log(value); // 0
console.log(obj.value); // 3
```


- 2) **call**, 또는 **apply**로 함수 안에 this를 넘겨주는 방법

```JS
var value = 0;
var obj = {
	value: 1,
	setValue: function () {
		this.value = 2;

		var a = function () {
			this.value = 3;
		}
		a.call(this);
		// (function () {
		// 	this.value = 3;
		// }).call(this); 위와 동일

	}
}
obj.setValue();
console.log(value);
console.log(obj.value);
```


근데 이런 방법들을 쓰기가 너무너무 번거롭다!!<br/>

> 🤦‍♀️ 번거로운 사람 : 그냥 내부의 this를 바로 쓰고 싶다... <br/>

그래서 세번째 방법
- 3) `block scope`로 감싸는 방법

```JS
var value = 0;
var obj = {
	value: 1,
	setValue: function () {
		let a = 20;
		this.value = 2;
		{
			let a = 10;
			this.value = 3;
		}
	}
}
obj.setValue();
console.log(value);
console.log(obj.value);
```

**내부에서만** 쓰고자하는 변수가 있어.<br/>
그래서 **외부의 변수와는 *분리된* scope**가 필요하긴 해.<br/>
근데 **this만큼은 *그대로*** 쓰고싶어.<br/>
`block scope`로 감싸주면 간단하게 해결된다<br/>
> 왜?<br/>
<strong style="color:black;background-color:yellow">
block scope 안에서는 this바인딩을 하지 않음! </strong>
하지 않기 때문에 밖에 있는 this를 그대로 쓰는 것.

**함수 scope와의 차이점**
- 함수 scope에서의 this
	- 전역객체를 바라봄
- block scope에서의 this
	- this바인딩을 아예 하지 않음

## 5. 모든 문 형태에 적용되는 block scope

```js
{
  let a = 2
  if (a > 1) {

		// 여기서의 b는
    let b = a * 3
    console.log(b)
		// 이 안에서만 존재함

  } else {
		// else는 아예 실행되지도 않음
    let b = a / 3
    console.log(b)
  }
  console.log(b) //  reference error: b is not defined
}
console.log(a) //  reference error: a is not defined
```


```js
let a = Math.ceil(Math.random() * 3)
switch (a) {
  case 1: {
    let b = 10
    console.log(a + b)
    break
  }
  case 2: {
    let b = 20
    console.log(a + b)
    break
  }
  case 3: {
    let b = 30
    console.log(a + b)
    break
  }
}
console.log(a, b)
```

- 1) a에 0 ~ 1 사이의 숫자를 넣은 다음 3을 곱함.
- 2) 그럼 0 ~ 2.999999의 숫자
- 3) 올림을 해서 나올 수 있는 숫자는 1, 2, 3

그럼 console의 결과는?<br/>
**🚨에러🚨 reference error: b is not defined.**
> 왜? <br/>

a는 밖에 선언됐으니 찾을 수 있음.<br/>
<strong style="color:black;background-color:yellow">
하지만 b는 block scope안에 갇혀있음!
</strong>
⭐️ 너무 당연하게 잘 나올 것 같지만 그렇지 않으니 주의할 것⭐️

**조금 다른 for문**

```js
var sum = 0
for (let i = 1 ; i <= 10 ; i++) {
  sum += i
}
console.log(sum)
console.log(i) // reference error: i is not defined
```
여기서의 i 또한 내부에서만 사용 가능.<br/>
여기서의 i는 인덱싱을 순차증가시키기 위한 목적일 뿐, 밖에서 써야할 필요성 전혀 없음.<br/>

그런데 여기서 만약 i를 var로 선언했다면?
```js
var sum = 0

for (var i = 1 ; i <= 10 ; i++) {
  sum += i
}

for (var i = 1 ; i <= 10 ; i++) {
  sum += i
}

for (var i = 1 ; i <= 10 ; i++) {
  sum += i
}

console.log(sum)
console.log(i)
```
var이기 때문에 밖으로 빠져나간다.<br/>
이미 선언한 변수를 다시 선언해서 중복성을 얻음.<br/>
같은 변수에 다시 할당하고, 다시 할당하고.....<br/>

변수가 for문 밖으로 빠져나가는 것 자체가 for문의 원리 취지와 벗어나게 된다.<br/>

여기까진 동일하지만,

```js
var sum = 0
for (let i = 1 ; i <= 10 ; i++) {
  sum += i
}
console.log(sum)
console.log(i)
```

for문에 있는 { }이 block scope 말고도, 앞에 있는 **( )의 안에서 선언한 변수까지도** `for문 전체의 block scope`에 갇힌다. 

> while도 switch도 ( )는 있지만 선언할 일 없음.