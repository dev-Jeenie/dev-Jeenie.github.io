---
title: "# 05.Arrow Function 🍿"
permalink: /cs/JavascriptArrowFunction
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-17
last_modified_at: 2021-10-17
---

![]()

# 5. Arrow function

6. sub-program<br/>

모든 프로그램이 각각의 기능이 있는건 모두 다른 function을 사용하기 때문.<br/>
프로그램 안에서 작은 기능들을 수행하는 것이 function이다<br/>

Input으로 parameter를 받아서 처리하고,<br/>
Output으로 return을 하는 것이 function<br/>

그래서, 언어 자체에 존재하는 function을 쓰거나<br/>
API(application programming Interface)를 쓸 때, function의 이름을 보고 그 기능을 예상할 수 있음<br/>
전달해야하는 파라미터 값이 뭔지, 어떤 값이 return되기를 기대할 수 있는지 이런 Interface를 보면서 예상할 수 있다<br/>

그래서 Input과 output이 중요하고, function의 이름이 중요한 것!

## function
프로그램을 구성하는 기본적인 빌딩블럭<br/>
sub program이라고도 불리며, 여러번 재사용이 가능하다<br/>
한가지의 task나, 어떤 값을 계산하기 위해 쓰여짐<br/>

 ## 1. function declaration
함수를 정의하는 방법!<br/>

```JS

function name (param1,param2) { body... return; }

```
function 키워드 입력<br/>
name 이름 지정<br/>
parameters 나열<br/>
body 함수의 기본적 비즈니스 로직 작성<br/>
return<br/><br/><br/>

- 하나의 함수는 한가지의 일만.
- 변수 네이밍이 명사이듯이 함수 네이밍은 doSomething형태, command 형태, verb 형태로
* 만약 이름짓는게 너무 어렵다면? 너무 많은 일을 하고있지는 않는지 생각! *
e.g. createCardAndPoint -> createCard, createPoint로 세분화<br/><br/>

- function은 JS에서 object로 간주된다
그래서 변수에 할당할 수 있고, parameter로 전달이 되고, 함수를 return할 수 있는 것.<br/>

Type Script )

function log(message:string) {
    console.log(message);
}

TS에서는 parameter나, return의 타입을 지정하지 않으면 오류가 뜬다.
- parameter의 타입은 (message:string) 이렇게
-return의 타입은 (message:string):number이렇게

타입을 명시해줘야함

* 이 TS는,

- 규모있는 프로젝트
- 여러 개발자와 협업을 할 때
- 우리가 작성한 것을 API형태로 라이브러리로 제공해야할 때

위와 같은 상황에서 개발을 원활하게 만들어준다!

: 함수의 인터페이스만 봐도, 이 함수가 뭘 하는 함수이고 어떤 파라미터를 전달해야하고 어떤 데이터 타입인지, 어떤 값이 리턴되는지를 명확하게 알 수 있기 때문에.


 ## 2. Parameters

function에 전달되는 이 parameters는
- Premitive parameters: passed by value
: 메모리에 그대로 저장되기 때문에, value가 전달된다

- object parameters: passed by reference
: reference가 저장되기 때문에 reference가 전달된다

```JS

 function changeName(obj) {
   obj.name = 'coder';
 }
 //전달된 객체 안의 name을 변경하는 함수
 const ellie = { name: 'ellie'};
 changeName(ellie);
 console.log(ellie); //ellie

 ```

object는 reference로 저장됨. 아래는 예시
<img src="/assets/images/JS_object.png" /><br/>

object는 reference로 전달되기 때문에,<br/>
함수 안에서 객체의 값을 변경하게 되면 변경된 사항이 그대로 메모리에 적용된다


## 3. Default parameters (added in ES6)
default 값을 미리 지정할 수 있는 default parameters

* 기존의 방식

```JS
function showMessage(message, from) {
  if(from == undefined) {
    from = 'unknown';
  }
  console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```
기존에는 이렇게, undefined일 경우를 대비해서 조건문을 작성해야했지만

* ES6의 방식

```JS
function showMessage(message, from = 'unknown') {
  console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```

사용자가 parameter값을 전달하지 않을때, 값이 이렇게 기본값으로 대체되어서 사용된다

4. Rest parameters (added in ES6)

```JS
function printAll(...args) {
  for(let i = 0; i < args.length; i++) {
    console.log(arg[i]);
  }
}
printAll('dream','coding','ellie'); //인자로 세개의 값을 전달
```
... 이렇게 전달하면 배열 형태로 전달이 된다!<br/>
'dream','coding','ellie' 이렇게 전달받은 값은 세개의 값이 담긴 배열이 된다<br/>

```JS
function printAll(...args) {
    for(const arg of args) {
    console.log(arg);
  }
}
printAll('dream','coding','ellie'); //인자로 세개의 값을 전달
```
for문보다 간단한 for of문으로 작성할 수도 있음 <br/>
arg에 있는 모든 값들이, 차례대로 하나씩 arg로 지정이 되면서 출력하게 된다

```JS
function printAll(...args) {
    args.forEach((arg) => console.log(arg));
  }
}
printAll('dream','coding','ellie'); //인자로 세개의 값을 전달
```


## 5. Local scope

참조) closer, LexicalEnvironment <br/>

* 밖에서는 안이 보이지 않고, 안에서만 밖을 볼 수 있다

이것이 scope의 개념

```JS
let globalMessage = 'global'; // global variable 전역변수
function printMessage() {
  let message = 'hello';
  console.log(message); // lacal variable 지역변수
  console.log(globalMessage);

  function printAnother() {
    let childMessage = 'hello';
  }
  // console.log(childMessage) //error
}
printMessage();
```

자식은 부모에게서 정의된 메시지를 확인할 수 있다지만 <br/>
자식 안에 정의된 childMessage를 부모에서 볼 수 없음

* 중첩된 함수에서 자식의 함수가, 부모 함수에 정의된 변수에 접근이 가능한 것들이 바로 closer.



## 6. Return a value

```JS
function sum(a, b) {
  return a + b;
  }
  const result = sum(1,2); //3
  console.log(`sum: ${sum(1,2)}`);
```

parameters로 값을 전달 받아서, 계산된 값을 return할 수 있다

```JS
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

아까 봤던, 이렇게 return이 없는 함수들은 return undefined가 된 것과 같다<br/>
모든 함수는 return undefined이거나, 값을 Return할 수 있다


## 7. Early return, early exit

* 나쁜 예!

```JS
Function upgraderUser(user) {
  if(user.point > 10) {
    //long upgrade logic
  }
}
```
해당 조건일 때에만 무언가 작동하는 로직이 있다. block안에서 로직을 많이 작성하면 가독성이 떨어진다.

* 좋은 예!

```JS
Function upgraderUser(user) {
  if(user.point <= 10) {
    return;
  }
    //long upgrade logic
}
```
if else를 번갈아서 쓰는 구조보다는, 조건이 맞지 않을 때 이렇게 빨리 return 시켜버리고!<br/> 
조건이 맞을 때만 그 다음으로 와서 필요한 로직들을 쭉 실행하는 구조가 좋다.

- 조건이 맞지 않는 경우
- 값이 undefined인 경우
- 값이 -1인 경우




