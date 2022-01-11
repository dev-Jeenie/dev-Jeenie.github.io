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
(배열도 primitive 타입이 아닌, Object 타입이기 때문에)