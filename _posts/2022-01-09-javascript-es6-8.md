---
title: (8) Arrow Functions"
permalink: /es6/javascriptEs68
tags:
  - [es6]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-18
last_modified_at: 2022-01-18
---

![]()

## 1. Arrow Function

```js
var a = function() {
  return new Date()
}

var a = () => {
  return new Date()
}
```

위와 아래는 동일하다.<br/>

여기서 더 축약할 수 있음!

```js
var a = () => new Date()
```
> a라는 함수는, <br/>
어떤 것을 받을 건데, <br/>
걔가 => 뒤의 내용으로 될 거야.<br/>

함수내부의 내용이 **반환값(return)** 밖에 없으면,<br/>
**중괄호**와 **return**까지 없애서 그 `자체가 return`이 되게 가능함.<br/>


```js
var b = a => a * a;
```
**인자가 하나인 경우**엔 `괄호`도 **생략 가능**.<br/>

```js
var d = (a,b) => {
  console.log(a * b)
}
```

return할 것이 없으면 더이상 축약하지 못함.<br/>


**여기서 예외!**

```js
var e = function (x) {
  return {
    x: x
  }
}
// 아래와 같이 축약 가능

var e =  x => ({ x })

```
객체를 **즉시 반환**을 해야하는 경우에는,<br/>
return 생략했다고 { x: x} 이렇게 쓸 수 없음.<br/>
(arrow function의 스코프로 인식하기 때문)<br/>
**객체임을 명시**하기 위해서 `괄호로 묶어줘야함`.<br/>

해석하자면,<br/>
함수 e에 들어온 x가,<br/>
x property를 key와 value로 하는 객체로 만들어져서 반환될 거야.<br/>



```js

var f = function (a) {
  return function (b) {
    return a + b;
  }
}

// 아래와 같이 변환 가능

var f = a => b => a + b;
var z = f(1)(2);

```

위 예제는 closer.<br/>
a를 받은 것을 실행한 결과를 가지고 다시 b로 보냄.<br/>

함수 f를 실행할 때 1을 넘겨 준것이 a에 들어가고, <br/>
다시 2를 넘겨준게 b에 들어간다.

### 1-1. 상세


- 1) (매개변수) => { 본문 }

- 2) 매개변수가 하나뿐인 경우 괄호 생략 가능

- 3) 매개변수가 없을 경우엔 괄호 필수
  - (아예 안쓰겠다는 확신이 있다면 ` _ ` 도 가능)

- 4) 본문이 `return [식 or 값]` 뿐인 경우 `{ }`와 `return` 키워드 생략 가능

- 5) 위 4) 에서 return할 값이 `객체`인 경우엔 괄호 필수

- 6) 실행컨텍스트 생성시 ⭐️ **`this 바인딩`을 `하지 않음`** ⭐️

⭐️ 중요 ⭐️<br/>


### 1-2. arrow function의 this 바인딩

arrow 함수는,<br/>
기존 함수의 기능을 문법적으로 보기 편하게, 직관적으로 표시하게끔 만든 것만은 ❌<br/>

`함수를 가볍게` 가져가기 위해서!<br/>

- 기존의 경우

```js
const obj = {
  a () {
    console.log(this) // - (1)

    const b = function () {
      console.log(this) // - (2)
    }

    b()
  }
}
obj.a()
```

<img src="/assets/images/es6-8-arrow-function.png" /><br/>


(1)의 this는 `obj`<br/>
메소드로 호출했기 때문에, 당연히 ` . `의 앞인 obj<br/>

(2)의 this는 `window`<br/>
함수라는 것 자체가 `실행되는 순간`에 **`this를 바인딩`**한다.<br/>
this를 찾는데, 바인딩할 this가 없으니까 자동으로 `전역객체인 window`를 바인딩한 것.<br/>




- arrow function의 경우

```js
const obj = {
  a () {
    console.log(this) // - (1)

    const b = () => {
      console.log(this) // - (2)
    }

    b()
  }
}
obj.a()
```

<img src="/assets/images/es6-8-arrow-function-2.png" /><br/>



(1)의 this는 `obj`<br/>

(2)의 this는 `obj`<br/>

arrow function은 실행되어서 실행 컨텍스트가 생성될 때,<br/>
<strong style="color:black;background-color:yellow">
this바인딩 자체를 하지 않는다.</strong>

b는 this를 들고있지 않으니, **`외부 스코프의 this`**를 그대로 가져와서 쓰는 것.<br/>

> this 바인딩을 하지 않는 것은 또 뭐가 있었지?<br/>
`block scope`!<br/>
block scope도 함수 scope와는 다르게 this 바인딩을 하지 않고 외부의 this를 가져옴.<br/>

🤷🏻‍♀️ : 그럼 arrow function이 block scope인 거야?<br/>

=> **답 :** ❌

**예제**

```js

const a = () => {
  var x = 10;
}
a();

console.log(x);

```

- 1) arrow function == `block scope` 라면?

arrow function이 block scope라면,<br/>
**var는 block scope의 영향을 받지 않고** `외부 변수로 인식`하니까 x가 출력 될거야.


- 2) arrow function == `함수 scope` 라면?

arrow function이 함수 scope라면,<br/>
**var로 선언한 변수는 함수 scope안에 `갇혀서`** 밖에서는 x를 찾지 못할 거야.<br/>

=> 결과

<img src="/assets/images/es6-8-arrow-function-3.png" /><br/>


=> arrow function이 block scope인 것이 ❌<br/>
arrow 함수는 기존 함수와 동일하게 `함수 scope`임!<br/>


| this 바인딩의 유무 |
| -- | -- |
| 한다 | 안한다 |
| function scope | block scope |
| function | arrow function |


arrow function는
- `함수 스코프`를 생성
- 단, 실행 컨텍스트 생성시 this 바인딩❌


```js
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {
    this.total = 0 // 여기서의 this는 obj
    this.grades.forEach(function(v) {//여기도 obj
      this.total += v
      // 여기는 forEach가 돌려주는 콜백함수.
      // 콜백함수 안에서 this는, 그냥 함수 실행이기 때문에 window
      // 그래서 window.total의 v가 증가
    })
  }
}
obj.getTotal()
console.log(obj.total)
console.log(total) // NaN. 처음에 아무것도 없었으니,
// undefined + 80 + 90 + 100 이 됐으니 숫자가 아님
```

```js

var total = 0;
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {
    this.total = 0;
    this.grades.forEach(function(v) {
      this.total += v;
    })
  }
}
obj.getTotal();

console.log(total) // 270

obj.total // 0
```
여기서 obj.total가 0이 찍히는 이유?<br/>
forEach 콜백함수 안에 this가 전달되지 않았기 때문.<br/>

- 1) 직접 this를 지정해주는 방법
(forEach argument의 뒤에는 `this argument 인자`가 들어옴.)

```js

var total = 0;
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {
    this.total = 0;
    this.grades.forEach(function(v) {
      this.total += v;
    },this)
  }
}
obj.getTotal();

obj.total // 270
```

- 2) arrow function을 사용하는 방법

```js

var total = 0;
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {
    this.total = 0;
    this.grades.forEach(function(v) {
      this.total += v;
    },this)
  }
}
obj.getTotal();

obj.total // 270
```
this 바인딩을 하지 않는 arrow function을 써버리면 간단.<br/>

🙋‍♀️ : arrow function은 this 바인딩 안하니까 너무 좋은거구나!<br/>

❌ 좋지만은 않다.<br/>
#### 1-2-1. 단점

- 1) this 변경 불가

```js
const a = () => {
  console.log(this)
}

a()
```

이때의 this는 window.<br/>

```js
a.call( {} )
```

call의 첫번째 인자는 this니까, 새로운 this를 지정해줘도 ❌<br/>

콜백이 아닌 일반 함수였다면?<br/>

```js
const c = function () {
  console.log(this)
}
c()
```
이때의 this는 마찬가지로 window.<br/>

```js
c.call( {} )
```
undefined 출력.<br/>
함수실행시에 this를 {} 인 채로 실행하라고 줬으니까!<br/>
그래서 this 바인딩한 상태에서 실행하는 것.<br/>


=> 그렇다고 arrow function에서의 call이 제 기능을 못하는 건 아님.<br/>

> call 본연의 기능<br/>
첫번째 인자로 this인자를 넘겨주고, 뒤에 실행할 argument들(인자들)을 넘겨줌.

**call 비교 예제**

```js
function sum (...arg) {
  console.log(this);
  return arg.reduce((p,c) => p + c);
}
sum(1,2,3,4,5);
sum.call({},1,2,3,4,5);
```

<img src="/assets/images/es6-arrow-function-this.png" /><br/>


this 변경 O, call 전달 O


```js
const sum2 = (...arg) => {
  console.log(this);
  return arg.reduce((p,c) => p + c);
}
sum2(1,2,3,4,5);
sum2.call({},1,2,3,4,5);
```

<img src="/assets/images/es6-arrow-function-this-2.png" /><br/>

this 변경 X, call 전달 O


=> **결론**<br/>
this 바인딩만 안될 뿐, call은 제역할을 한다<br/>



### 1-3. 생성자 함수


- 기존 함수

```js
function sum (...arg) {
  console.log(this);
  return arg.reduce((p,c) => p + c);
}
console.dir(sum)
```
prototype이 존재 = `생성자함수`로 사용 **가능**

- arrow function

```js
const sum2 = (...arg) => {
  console.log(this);
  return arg.reduce((p,c) => p + c);
}
console.dir(sum2)

```
prototype이 없음 = `생성자함수`로 사용 **불가능**


```js

const b = new sum()
// sum { }

const c = new sum2()
//error! sum2 is not a constructor

```

> concise method와 arrow function
- 공통점
  - prototype 프로퍼티가 X => 생성자함수로 X
  - arguments, callee => hidden. invoke해야만 값을 얻을 수 있다
- 차이점
  - concise method
    - method는 method로만. 함수로 사용불가
  - arrow function
    - method는 함수로만.(내부함수로써는 method로 가능)


```js

const b = {
  name: '하하',
  bb () {
    return this.name;
  },
  a: x => {
    return this.name;
  }
}

b.bb(); // '하하'
b.a(); // ''

```
여기서 b.a는 왜 아무것도 나오지 않을까?<br/>
b.a는 `arrow function`이라 this를 **바인딩하지 않기 때문**.<br/>
근데 왜 빈문자열이 나오지?<br/>

=> **window.name**이 이미 있기 때문에.<br/>

```js
window.name = '안뇽';

b.a(); // '안뇽'
```

b.a는 메소드로써의 기능❌, 함수로써의 기능<br/>
this가 객체를 가리키게 할 수 없다.<br/>


🤷🏻‍♀️ : 그럼 arrow 함수를 언제 써야 method로써의 의미가 있지??<br/>

메소드 안에서 같은 this를 가지고 써야할 때(내부함수로 쓸 때)<br/>
아래처럼

```js
const b = {
  name: '하하',
  bb () {
    const b = x => {
      return this.name;
    }
    console.log(b());
  },
}
b.bb(); // '하하'
```