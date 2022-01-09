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

## 1. block scope란?

**용어 정의**

- Scope
	: 범위, 유효공간, 살 수 있는 공간, 허용되던, 허용범위 …

- 함수 스코프
	: 함수에 의해서 생기는 범위, 변수의 유효범위

- 블락 스코프( Block scope)
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



block scope는 중괄호에 의해서 영향을 받는다.
if문, for문, while문, swith-case문 등의 함수에 의한 중괄호 또한 영향을 받는다!

