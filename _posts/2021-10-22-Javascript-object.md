---
title: "# 07. Object 🍱"
permalink: /js1/JavascriptObject
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-22
last_modified_at: 2021-10-22
---

![]()

# Object

- one of the JavaScript's data types.
- a collection of related date and/or functionality.
- Nearly all objects in JavaScript are instances of Object.

```js

function print(name,age) {
  console.log(name);
  console.log(age);
}

```

함수의 parameter에 이렇게 작성할 경우, 인자가 많아지면 추가해야하는 것들이 많아진다.<br/>
로지컬하게 묶어서 생각할 수도 없음!<br/>

이걸 개선하고자 쓰는 것이 Object ⭐️


```js

function print(person) {
  console.log(person.name);
  console.log(person.age);
}
const ellie = { name: 'ellie', age: 4 };
print(ellie);

```


1. Literals and Properties

```js

const obj1 = {}; // 'object literal' syntax
const obj2 = new Object(); // 'object constructor' syntax

``` 
new command를 넣어서 객체를 만들면, Object에서 정의된 constructor가 호출된다!


```js

const ellie = { name: 'ellie', age: 4 };
print(ellie);

ellie.hasJob = true;
console.log(ellie.hasJob); // true
delete ellie.hasJob;
console.log(ellie.hasJob); // undefined

```
JS는 타입이 runtime(프로그램이 동작하고 있을 때)에 결정되는 언어이기 때문에 이런 것도 가능함.
 
2. Computed properties

정확하게 어떤 key가 필요한지 모를때, 즉 runTime에서 결정될 때 사용하는 문법 <br/>
코딩할 때에는 . 문법으로 불러오는 게 맞음!

```js
console.log(ellie.name); // ellie
console.log(ellie['name']); // ellie
ellie['hasJob'] = true;
console.log(ellie['hasJob']); // true
```

object 안에있는 변수의 이름을 string 형태로 받아올 수 있다

- object의 property를 . 문법을 이용해서 접근을 할 수 있고
- 또는 computed properties 문법으로 배열에서 데이터를 받아오듯이 접근할 수 있다

단, computed properties로 받아올 때 key는 항상 string타입을 지정해서 받아와야한다!

<img src="/assets/images/JS_Computed_Properties.jpeg" /><br/>


3. Property value shorthand

key와 value의 이름이 동일하다면 생략할 수 있다.

```js

const Person1 = { name : 'bob', age: 2 };
const Person2 = { name : 'steve', age: 3 };
const Person3 = { name : 'dave', age: 4 };

const Person4 = Person('ellie',30);
console.log(person4);
 
function Person(name, age) {
  return {
    name,
    age
  }
}

```

Person1,2,3처럼 동일한 key와 value를 반복적으로 전달하던 것을<br/>
=> 효율적으로 값만 넣으면 출력되게 변경.<br/>

class template과 동일한 구조. class가 없었을 때는 이렇게 작성했다.<br/>


4. Constructor function

```js
function Person(name, age) {
  // this = {};
  this.name = name,
  this.age = age
  // return this;
}
const Person4 = new Person('ellie',30);

```
이렇게 다른 계산을 하지 않고, 순수하게 object를 생성하는 함수들은 보통 대문자로 시작한다.<br/>
return도 하지 않고 이렇게 class처럼 this를 사용한다.<br/>
호출 시에도 class에서 새로운 object를 만드는 것처럼, new로 호출할 수 있다.


5. in operator : property existance check (key in obj)

: 간단하게 key의 유무를 확인할 수 있는 키워드, 있다면 true, 없다면 false

```js
console.log('name' in ellie); // true
console.log('age' in ellie); // true
console.log('random' in ellie); // false
console.log(ellie.random); // undefined
```

6. for...in vs for...of

- for (key in obj)

```js
for (key in ellie) {
  console.log(key); 
}
```
ellie가 가지고있는 key들이, 블럭을 돌 때마다 <strong style="color:red">key라는 지역변수에 할당</strong>이 된다! <br/>

모든 키들을 받아와서 일을 처리하고 싶을 때 for in 을 사용하면 좋다.


- for (value of iterable)
: 배열과 같은 리스트, 순차적으로 Iterable한 것들을 쓴다.

```js

const array = [1,2,3,4,5];
for(let i = 0; i < array.lenth; i++) {
  console.log(value);
}

```

이것 보다는 훨씬 간단한 for of

```js

for(value of array) {
  console.log(value);
}

```

7. Fun Cloning
: Object.assign(dest, [obj1,obj2,obj3...])

```js

const user = {name: 'ellie', age:'20'};
const user2 = user;

```

* 바꾸지 않고 코딩하는 방법?

1. old way

```js
const user3 = {};
for(let i = 0; i < user.length; i++) {
  user3[key] = user[key];
}
console.log(user3);
```
<img src="/assets/images/JS_object_oldway.jpeg" /><br/>


2. Object.assign

```js

// const user4 = {};
// user4 = Object.assign(user); 빈 객체이기 때문에, 아래처럼 줄일 수 있음

const user4 = Object.assign({ }, user );
console.log( user4 );
```
<img src="/assets/images/JS_object_assign.jpeg" /><br/>

* 다른 예시

```js

const fruit1 = {color : 'red'};
const fruit2 = {color : 'blue', size:'big'};
const mixed = Object.assign({},fruit1, fruit2);

console.log(mixed.color); // blue
console.log(mixed.size); // big

```
앞에 동일한 property가 있다면, 값이 계속 덮어씌워진다



# Array와 API

* array와 object의 차이점!

<img src="/assets/images/JS_array.jpeg" /><br/>
<img src="/assets/images/JS_array_2.jpeg" /><br/>



1. Declaration

```js

const arr1 = new Array();
const arr2 = [1,2];
```

2. Index position

```js
const fruits = ['🍓','🍌'];
console.log(fruits);
console.log(fruits.length);
console.log(fruits[0]); //배열의 첫번째 개체를 찾을 때
console.log(fruits[1]);
console.log(fruits[2]); //undefined
console.log(fruits[fruits.length - 1]); //배열의 마지막 개체를 찾을 때

```

3. Looping over an array

a. for loop

```js
  for(let i = 0; i < fruits.length; i ++){
    console.log(fruits[i]);
  }
```

b. for of loop

```js
for (fruit in fruits) {
  console.log(fruits[fruit])
}

```

c. for Each loop 

```js

fruits.forEach(function(fruit, index, array) {
  console.log(fruit,index,array);
});
// anonymous function은 arrow function으로 축약 가능
fruits.forEach((fruit, index) => {
  console.log(fruit,index);
});

```

<img src="/assets/images/JS_forEach.jpeg" /><br/>

* Performs the specified action for each element in an array.
array에 들어있는 각각의 엘리멘트에 정해진 액션을 수행하는 함수


배열에 들어있는 값 마다 우리가 전달한 액션=콜백함수를 실행한다


4. Addition, deletion, copy

a. push : add an item to the end 끝에 추가

```js
fruits.push('🍓','🍋');
```

b. pop : remove an item from the end 맨 끝의 아이템을 삭제

```js
fruits.pop();
fruits.pop();
```

c. unshift : add an item to the beginning

```js
fruits.unshift('🍓','🍋'); // 배열의 앞에 아이템 추가
```

d. shift : remove an item from the beginning

```js
fruits.shift(); // 배열의 앞에서부터 아이템을 삭제
```

⭐️ 중요 ⭐️<br/>
shift, unshift are slower than pop, push!

<img src="/assets/images/JS_push_pop.jpeg" /><br/>
<img src="/assets/images/JS_shift.jpeg" /><br/>

e. splice : remove an item by index position
splice(index, count)

```js
fruits.push('🍓','🍑','🍋');
console.log(fruits);
fruits.splice(1,1); // 1번 인덱스에서 1개만.
fruits.splice(1); //원하는 인덱스만 지정하고 갯수를 지정하지 않으면, 그 인덱스 뒤의 아이템을 싹 지운다
console.log(fruits);

fruits.splice(1,1,'🍏','🍉');
// 지우고 나서 그자리에 원하는 데이터를 추가할 수 있다.
fruits.splice(1,0,'🍏','🍉');
// 지우지 않고! 그 자리 다음부터 데이터를 추가할 수 있다.

```

f. concat
combine two arrays
새로 묶여진 배열이 합쳐져서 새로 리턴됨.

```js
const fruits2 = ['🍐','🥑'];
const newFruits = fruits.concat(fruits2);

console.log(newFruits);
```


5. Searching

a. indexOf : find the index

```js
console.log(fruits);
console.log(fruits.indexOf('🍎')); // 0
console.log(fruits.indexOf('🍉')); // 3
console.log(fruits.indexOf('🥐')); // -1 해당 인덱스가 없으면 -1을 출력
```

b. includes

```js
console.log(fruits.includes('🍉')); //true
console.log(fruits.includes('🥐')); //false
``` 

c. lastIndexOf
lastIndexOf : 뒤에서부터 검색
indexOf : 앞에서부터 검색

```js
fruits.push('🍎');
console.log(fruits); //['🍎','🍏','🍉','🍑','🍋','🍎'];

console.log(fruits.indexOf('🍎')); // 0
console.log(fruits.lastIndexOf('🍎')); // 5
```