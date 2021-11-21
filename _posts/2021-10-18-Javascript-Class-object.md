---
title: "# 06.Class vs Object ☕️"
permalink: /cs/JavascriptClassObject
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-18
last_modified_at: 2021-10-18
---

![]()

# 6. First-class function
- function are threated like any other variable
함수는 다른 변수처럼 사용된다
- can be assigned a value to variable
다른 변수에 할당이 된다
- can be passed as an argument to other functions.
함수의 parameter로 전달이 되며
- can be returned by another function
return값으로도 return이 된다

1. Function expression

function declaration / function expression

- a function declaration can be called earlier than it is defined. (hoisted)

: function declaration은 hoisting이 된다. 정의하기도 전에 호출이 가능함!<br/>
(JS엔진이 선언된 것을 제일 위로 올려주기 때문)

- a function expression is created when the execution reaches it.

function expression은 할당된 다음부터 호출이 가능함.


```JS
// const print = function print () { // named function 
const print = function () { // anonymous function
  console.log('print');
};
print(); //호출, 'print' 출력
const printAgain = print; //'print' 출력
printAgain();
const sumAgain = sum; //위에서 만든 sum함수를 넣어도 가능
console.log(sumAgain(1,3));

```

2. Callback function using function expression


```JS

function randomQuiz(answer, printYes, printNo) {
  if(answer === 'love you') {
    printYes();
  } else {
    printNo();
  }
}

const printYes = function () {
  console.log('yes!')
}


// named function
// better debugging in debugger's stack traces
// recursions

const printNo = function print () {
  console.log('no!')
}

randomQuiz('wrong', printYes, printNo); // 정답이 아니라면 no, 맞으면 yes를 출력해라
randomQuiz('love you', printYes, printNo); // 정답이 아니라면 no, 맞으면 yes를 출력해라

```

이렇게 함수를 전달해서<br/>
<strong style="backgroud-color:blue, color:white" >상황이 맞으면, 전달된 함수를 불러"</strong><br/>
라고 하는 것을 Callback function이라고 한다!<br/>

두가지의 callback functions가 parameter로 전달 <br/>

printYes에는 anonymous function을, printNo에는 named function을, 쓴 이유? <br/>

- debugging의 stack trace에 함수 이름이 나오게 하기 위해
- 함수 안에서 자신 스스로 또다른 함수를 호출할 때 (Recursions)



3. Arrow function
: always anonymous

```JS

const simplePrint = function () {
  console.log('simplePrint!');
}

const simplePrint = () => console.log('simplePrint!');
const add = (a,b) => a + b;

const simpleMultiply = (a,b) => {
  // do something more
  return a * b;
}

```

4. IIFE : Immediately Invoked Function Expression

: 선언과 동시에 호출

```JS
function hello() {
  console.log('IFFE')
hello();
```
이렇게 함수를 따로 호출하지 않고

```JS
(function hello() {
  console.log('IFFE');
})();
```
괄호로 묶어서 함수를 호출해주면, 선언과 동시에 호출이 가능하다

* Quiz!

```JS
// function calculate(command, a, b)
// command: add, substract, divide, multiply, remainder
function calculate(command, a, b) {
  switch (command) {
    case 'add':
    return a + b;
    case 'substract':
    return a - b;
    case 'divide':
    return a / b;
    case 'multiply':
    return a * b;
    case 'remainder':
    return a % b;
    default:
    throw Error('unknown command');
  }
}
console.log(caculate('add',2,3));


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




# 7. class와 object의 차이점

## class란?
: 연관있는 데이터를 한데 묶어놓은, 컨테이너 같은 개념

```JS
class person {
  name; // property
  age; // property
  speak(); // function
}
```
class안에는 <br/>
이렇게 name, age 같은 속성(field)와, speak 같은 행동(method)가 들어있다

* => class는 fields와 methods가 종합적으로 묶여있는 것을 말함!

(간혹 methods없이 fields만 들어있는 경우도 있다= data class) <br/>

class 안에서도 내부적으로 보여지는 변수와, 밖에서 보이는 변수를 나눈다 (캡슐화 captualation)

* 이런 모든 것들이 가능한 것이 바로 객체 지향언어! 



1. Class declarations


```JS

class Person {
    // constructor 생성자
    constructor (name, age) {
        // fields
        this.name = name;
        this.age = age;
    }
    // method
    speak() {
        console.log('${this.name}, Hello!');
    }
}

```

생성자를 만들어서, 나중에 object를 만들 때 필요한 data를 전달
전달받은 데이터를 class에 존재하는 두가지 field인 name과 age에 바로 할당한다

* 이 class를 이용해서 object 만들기!

```JS

const ellie = new Person('ellie', 20);

console.log(ellie.name); // ellie
console.log(ellie.age); // 20

ellie.speak();

```
<img src="/assets/images/JS_class.jpeg" /><br/>


2. static properties and methods

<img src="/assets/images/JS_static.jpeg" /><br/>

```JS
class Article {

  static publisher = 'Dream Coding';
  consturctor(articleNumber) {
    this.articleNumber = articleNumber;
  }
  
  static printPublisher() {
    console.log(Article.publisher);
  }
}

const article1 = new Article(1);
const article2 = new Article(2);
console.log(article1.publisher); // undefined
console.log(Article.publisher); // Dream coding

Article.publisher();

```

위처럼 static으로 선언된 변수는 object마다 할당되어지는 것이 아니라,<br/>
Class 그 자체에 할당되어지는 것.<br/>

그래서 static을 호출할 때도 class이름으로 호출해야 한다.
<strong style="color:blue">
들어오는 데이터에 상관없이 공통적으로 쓸 수 있는 거라면 모두! <br/>
static과 static method를 이용해서 작성하는 것이 메모리 사용을 줄여주는 방법!
</strong>


3. Inhrritance
a way for one class to extend another class.

```JS

class Shape {
  constructor(width, height,color) {
    this.width = width;
    this.height = height;
    this.color = color;
  } // fields

  draw() {
    console.log(`drawing ${this.color} color of`);
  } // method

  getArea() {
    return width * this.height;
  } // method
}

class Rectangle extends Shape {}
class Triangle extends Shape {
  draw() {
   super.draw(); // 부모의 method도 출력되고, 여기서 정의한 method도 호출됨 
   console.log('삼각형입니다');
 }
  getArea() {
   return this.width * this.height;
 }
}
// extends로 연장만 하면 Shape에서 정의한 fields와 method가 자동적으로 Rectangle에 포함된다

const rectangle = new Rectangle(20,20,'blue');
rectangle.draw();
rectangle.getArea();

const triangle = new Triangle(20,20,'blue');
triangle.draw();
triangle.getArea();

```

- 공통되는 것들을 일일이 작성하지 않고, extends를 이용해 계속 재사용할 수 있다
- 그래서 잘못된 부분이 있을 때, class에서만 수정하면 모두 반영된다

* 다양성이 빛을 발휘하는 순간!
- triangle은 너비를 구하는 공식이 다르다 (너비*높이)/2를 해야함.
 
*  필요한 함수만 재정의해서 쓸 수 있다!

<img src="/assets/images/JS_class_extends.jpeg" /><br/>


이게 바로 <strong color="blue">오버 라이딩</strong>!


4. Class checking: instanceOf

```JS
console.log(rectangle instanceOf Rectangle); //true
console.log(triangle instanceOf Rectangle); // false
console.log(triangle instanceOf Triangle); //true
console.log(triangle instanceOf Shape); //true
console.log(triangle instanceOf Object); //true 
console.log(triangle.toString()); // [Object Object]

```

어떤 object든지, 공통적으로 존재하는 method를 쓸 수가 있다!

```JS
class Triangle extends Shape {
  draw() {
   super.draw();
   console.log('삼각형입니다');
 }
  getArea() {
   return this.width * this.height;
 }
 toString() {
   return `Triangle: color: ${this.color}`
 }
}
```

Object에 공통적으로 존재하는 method도 오버라이딩을 할 수 있다.

* JavaScript내부에 포함되어있는 Object
참조) https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
