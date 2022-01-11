---
title: "Java script ES6💫 제대로 알아보기! ✍️ (2) Block Scoped variables"
permalink: /cs/javascriptEs62
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-10
last_modified_at: 2022-01-10
---

![]()

## 1. let

- var와 같은 개념.
- 단, `block scope`에 갇히고
- `TDZ에 제한`된다

**예제**

```js
let a = 1
function f() {
	console.log(a,b,c) // - (A)
	let b = 2
	console.log(a,b,c) // - (B)
	if (true) {
		let c = 3
		console.log(a,b,c) // - (C)
	}
	console.log(a,b,c) // - (D)
}
f()
```

- 1) f를 실행해서 실행 컨텍스트가 열림.
- 2) `(A) console`
	- 같은 컨텍스트 안에 a가 없기 때문에 외부로 나감. **a는 1**
	- 해당 콘솔의 밑에서 b 선언은 함. hoisting되어서 올라갔지만 TDZ에 걸림. **b는 에러! not defined**
	- c는 아예 없음. **c는 에러! not defined**
- 3) `(B) console`
	- 같은 컨텍스트 안에 a가 없기 때문에 위로 찾아 올라감. **a는 1**
	- 같은 컨텍스트 안에 b가 있음. **b는 2**
	- 같은 컨텍스트 안에 b가 있음. **c는 에러! not defined**
- 4) `(C) console`
	- a,b,c 모두 출력됨. **a는 1, b는 2, c는 3**
- 4) `(D) console`
	- a,b는 출력되지만 c는 에러. **a는 1, b는 2, c는 에러! not defined**

**⭐️ 중요 ⭐️**
=> 아무리 선언을 아래에서 했다고 해도, <strong style="color:black;background-color:yellow">실제로 값을 할당하기 전까지는 TDZ에 다 걸려서 어떤 것도 할 수 없음</strong>!

<img src="/assets/images/object-let.jpeg" /><br/>


```js
b = 1
console.log(b)
const b = 2;
```
물론 이것도 ❌<br/>
실제로 값을 할당하기 전에는 그 어떤 것도 불가능.<br/>

🙋‍♀️ : 그럼 아래에서 선언을 해도 에러, 아예 안해도 에러로 똑같은건가?

## 1-1. let 상세
- `재할당`이 가능하다(var처럼)

```js
let a = 1
a = 2
console.log(a)
```

```js
var funcs = []
for (var i = 0; i < 10; i++) {
	funcs.push(function () {
		console.log(i)
	})
}
funcs.forEach(function (f) {
	f()
})
```

- 1) 빈 배열을 만들고
- 2) for 반복문으로 해당 배열에 함수를 push한다
- 3) 다시 forEach 반복문을 돌려서, 각각의 함수를 실행하게 함

=> 결과는 어떻게 나올까? <br/>

- 보기 1번) 0,1,2,3,4,5,6,7,8,9
- 보기 2번) 9,9,9,9,9,9,9,9,9,9

정답은? 둘 다 ❌. **10이 10번** 나온다~ <br/>

🤷🏻‍♀️ : 아니 왜❓❓❓❓<br/>

funcs 배열에는
```js
[
	function () { console.log(i) }
	function () { console.log(i) }
	function () { console.log(i) }
	....
]
```
- 1) 이렇게 함수가 열개 들어간다.
- 2) 그런데 이 함수를 실행하는 건? `for문이 다 돌고 난 후`!

```js
var funcs = []
for (var i = 0; i < 10; i++) {
	funcs.push(function () {
		console.log(i)
	})
}

// 여기서 이미 funcs 배열에 함수 열개가 들어간 뒤 종료되어있음.

funcs.forEach(function (f) {
	f() // 바로 여기서 실행 = 실행컨텍스트 열림!
})
```

<img src="/assets/images/object-var.jpeg" /><br/>


> 실행 컨텍스트는, **`함수를 실행할 때`** 열린다
실행할 때 비로소 변수를 hoisting하고, this를 바인딩하고, 자신에게 없는 변수를 외부에서 찾는다.

forEach안에서 함수를 실행했으니 i를 찾아야하는데, 전체 scope 공간에 i는 for문의 i가 살아있다.




그럼 어떻게 해야할까?<br/>
증가한 i을 나중에 읽어오게 하는게 아니라,<br/>
<strong style="color:black;background-color:yellow">i가 살아있게 해서 각각의 함수에게 넘겨줘야한다</strong>.

- 1) closer를 이용


```js
var funcs = []
for (var i = 0; i < 10; i++) {
	funcs.push(function (v) {
		return function () {
			console.log(v)
		}
	})(i))
}
funcs.forEach(function (f) {
	f()
})
```

즉시실행 함수로 만들어서 i를 넘겨주는 방법.<br/>
실제 호출은 나중에 하게끔 하기 위해서 `closer`로 다시 함수를 리턴해줌.<br/> i를 넘겨줘서 i를 들고있다가 <br/>나중에 호출할 때 그 값을 console.log(v)에서 출력해라.<br/>
그럼 이 `함수가 실행이 된 결과값이 return`되어서<br/> `배열 funcs에 push`가 되는 것.<br/>




- 2) 초간단하게 let을 이용


```js
let funcs = []
for (let i = 0; i < 10; i++) {
	funcs.push(function () {
		console.log(i)
	})
}
funcs.forEach(function (f) {
	f()
})
```
for문 자체가 block scope이니,<br/>for문의 block scope는 각각의 i값마다 별도로 생성이 됨.<br/>
i값이 block scope 내에 존재함!<br/>

즉시실행함수 고민할 필요 없이 간단히 해결.<br/>
closer 안에서 선언된 변수는 메모리에 영원히 있기 때문에, <br/>let을 사용하는 건 메모리 소모를 크게 덜어줌.


## 2. const

**constant variable(상수인 변수)**

- 선언과 동시에 값을 할당해야한다.
- 재할당이 되지 않는다.

```js
const A = 10;
console.log(A)
```
A라는 변수는 상수로 할거야, 그런데 그 값은 10으로 할래.<br/>
=> `선언`과 `값 할당`이 끝나야만 A라는 상수가 된다.

```js
const A;
//error! Missing initializer in const decparation.
```
이렇게 선언만 하면 상수 변수로 사용할 수 없다!

## 2-1. 참조타입 데이터의 경우엔?

const에 객체를 할당한다면?

- 1) 그 객체 자체를 바꾸려고 하는 경우

```js
const OBJ = {
	prop1 : 1,
	prop2 : 2,
}
OBJ = 10; // error! Assignment to constant variable.
```

상수변수에 값을 적용하려고 한다는 오류가 발생. 

- 2) 그 객체의 property의 값을 바꾸려고 하는 경우

```js
const OBJ = {
	prop1 : 1,
	prop2 : 2,
}
OBJ.prop1 = 3; // 3으로 변경
```

에러 발생하지 않음! OBJ라는 `상수변수 자체에 접근한 게` ❌<br/>
OBJ안에 있는 prop1이라는 **property에 접근**함.<br/>
OBJ와 OBJ의 property들은 `다른 공간에 저장`되어있음!<br/>
OBJ는 이 `공간을 참조`하고 있는 것 뿐.
그럼 <strong style="color:black;background-color:yellow">그 객체 자체는 상수가 아니다</strong>

<img src="/assets/images/es6-2-object-const.jpeg" /><br/>

**심화 예제**

<img src="/assets/images/es6-2-object-const-2.jpeg" /><br/>

> 우리가 알고있는 모든 숫자들은 이미 **메모리 어딘가에 저장**되어 있다.<br/>
계속 꺼내서 쓰기 때문에 이러한 **primitive 타입의 값**들이 `immutable`한 것이다!



=> **결론** <br/>
참조형 데이터를 상수변수에 할당할 경우, <br/>
<strong style="color:black;background-color:aliceblue">참조형 데이터 내부에 있는 property들은 상수가 아니다.</strong> <br/>

> 그럼 @30번에 남아있는 값은 언제 사라지지?<br/>
그 값을 참조하는 애들이 사라지면, 그때 가비지 컬렉터의 대상이 되어서 사라진다. 이렇게 메모리 괸리가 이루어짐


<img src="/assets/images/es6-2-object-const-arr.png" /><br/>

이것처럼 배열에서도, 상수변수 그 자체 변경하는 것 빼고 다 된다<br/>
(배열도 primitive 타입이 아닌, Object 타입이기 때문에)<br/>

🙋‍♀️ : 내부의 property도 상수로 만들수는 없나요?<br/>

🅾️ 있습니다!


## 3. 내부의 property도 상수로 만드는 방법

**Object.freeze()**와 **Object.defineProperty()**가 있다.

### 3-1. Object.freeze()
property들을 얼려버린다🧊

```js
const OBJ2 = {
	prop1 : 1
}
Object.freeze(OBJ2)
OBJ2.prop1 = 10;
// es5이기 때문에 친절한 오류는 안나오지만
// 값이 바뀌지는 않음!!
```

단, 여전히 문제는 있다.


```js
const OBJ2 = {
	prop1 : 1,
	prop2 : [1,2,3]
}
Object.freeze(OBJ2)
OBJ2.prop2 = 10; // 에러는 없지만 바뀌지않음
OBJ2.prop2[0] = 10; // 값이 바뀜!
```
OBJ2.prop2는 참조형 데이터이기 때문에,<br/>
이것이 참조하는 얼지 않았다.<br/>

그래서 OBJ2.prop2 자체는 바꿀 수 없지만,<br/>
그것이 참조하는 데이터는 바꿀 수 있는 것!<br/>

그래서 Object.freeze로 property들을 얼리기 위해서는,
- 1) Obj 자체를 얼린다.
- 2) Obj 내부의 property들을 **순회**하면서 혹시 **참조형이면 1을 반복**하라고 `재귀`를 시킨다.(property 안에 property 안에 property가 있을 수 있으니까)

=> 이것이 바로 `Deep Freezing`

#### 3-1-1. Deep Freezing


- Deep Copy `얕은복사`
	- 객체의 property들을 복사 (`depth 1단계`까지만)
- Deep Copy `깊은복사`
	- 객체의 property들을 복사 (`모든 depth`에 대해서)
	- 순서
		- 1) property들을 복사
		- 2) property 중 참조형이 있으면 1번 반복 => 재귀
		
**얕은 복사와 깊은 복사 예제**
- 얕은 복사의 경우
<img src="/assets/images/es6-2-light-copy.jpeg" /><br/>
- 깊은 복사의 경우
<img src="/assets/images/es6-2-deep-copy.jpeg" /><br/>

#### 3-1-2. immutable이란?

- mutable
	- 가변하다
- immutable
	- 불변하다
	- 불변하다는 것은 `매번 새로운 객체를 생성`한다
	- 매번 새로운 객체를 생성하기 위해 늘 `깊은 복사`를 한다

깊은 복사를 해야만 기존 데이터와는 **`별개의 데이터`**가 되기 때문에!

## 4. for문에서의 주의사항

- **`for in`문과 `for of`의 경우**

for in문에서 변수는 `const를 사용할 수 있다`

```js
	var obj = {
	prop1:1,
	prop2:2,
	prop3:3
	}
	for (const prop in obj) {
	console.log(prop)
	}
	// 결과 : prop1, prop2, prop3
```
for문이 반복되면서 const로 선언된 prop이<br/>
prop1이었다가, prop2이었다가, prop3이 된다.<br/>
const인데 이게 왜 되는걸까?<br/>

이게 바로 따로 기억해야할 **for문의 특이점**

위의 코드는 아래와 동일하게 실행된다.

```js
{
let keys = Object.keys(obj);
for(let i = 0; i < keys.lengh ; i ++) {
    const prop = .obj[keys[i]];
    console.log(prop);
    }
}
// for문 반복의 결과는
{
	const prop = .obj[keys[0]];
	console.log(prop);
}
{
	const prop = .obj[keys[1]];
	console.log(prop);
}
{
	const prop = .obj[keys[2]];
	console.log(prop);
}

```

obj 오브젝트에 있는 key들을 배열로 가져와서 keys에 넣는다.<br/>
반복을 하며 i하나마다 한개씩 열려서 <br/>
for문의 block scope가 매번 생긴다.<br/>

for in문의 상수변수 사용은 이런 방식으로 이해하면 됨.

> 물론 let 변수도 사용 가능하다!<br/>

```js
	var obj = {
	prop1:1,
	prop2:2,
	prop3:3
	}
	for (let prop in obj) {
		prop = 10
	console.log(prop)
	}
	// 결과 : 10, 10, 10
```
다만 이렇게 내부에서 변경이 가능한 문제가 있음. <br/>
(이 문제를 const 변수를 쓰면 해결)

- **`for`문의 경우**

for문에서의 변수는 `const를 사용할 수 없다`.
```js
	var obj = {
	prop1:1,
	prop2:2,
	prop3:3
	}
	for (const i = 0; i < obj.length; i ++) {
	console.log(prop)
	}// error! Assignment to constant variable.
```

=> **결론**<br/>
> for문의 가장 기본적인 형태는 let!<br/>

일반적인 `for문` 반복을 할때 변수는 `let`을 쓰면 되고,<br/>
`for in문` 반복을 할때 변수는 `const`로 쓰면 된다.<br/>

## 5. let과 const의 공통사항

var와는 다르게,
- let과 const는 `block scope`, 즉 `유효범위가 있다`
- let과 const는 `TDZ에 걸린다`
- `초기화되기 전 호출`이 `불가능`하다 (hoisting O, undefined 할당X이라 에러를 낸다는 뜻?)
- `재선언(재정의)`이 `불가능`하다
- `전역객체의 property` `불가능`하다


### 5-1. 재선언

- var의 경우

```js
var a = 0;
var a = 1;

console.log(a)
```

위의 코드는 자바스크립트가 아래처럼 처리한다.

```js

var a;
// var a;

a = 0;
a = 1;

console.log(a)
```

변수 a를 hoisting해서 끌어올리고,<br/>
중첩됐으니까 마지막 것만 Cascading(위에서 아래로 흐르다) 함.<br/>

=> 아무 문제없이 처리.

- let과 const의 경우

```js
let a = 0;
let a = 1;

console.log(a) // error! Identifier 'a' has already been declared
```

=> **결론**, var는 잊어라


### 5-2. 전역객체의 property가 불가능함

- var의 경우
```js
var a = 10
console.log(window.a)
console.log(a)
delete a
console.log(window.a)
console.log(a)
```


<img src="/assets/images/es6-var-window-1.jpeg" /><br/>
<img src="/assets/images/es6-var-window-2.jpeg" /><br/>

- let / const의 경우
<img src="/assets/images/es6-2-let-window.jpeg" /><br/>

## 6. let과 const의 차이점

- let
	- 값 자체의 변경이 필요한 `예외적인 경우`
- const
	- 기본으로 생각할 것. 프론트엔드 개발환경에서는 `객체`를 많이 다룬다. 이 객체를 바꿔치기할 일은 많지 않음.
	- const로 선언해도 객체 내부의 property값 변경은 얼마든지 가능하고 훨씬 안전해짐.


	