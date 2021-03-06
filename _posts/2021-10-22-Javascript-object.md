---
title: "# 07. Object ๐ฑ"
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

ํจ์์ parameter์ ์ด๋ ๊ฒ ์์ฑํ  ๊ฒฝ์ฐ, ์ธ์๊ฐ ๋ง์์ง๋ฉด ์ถ๊ฐํด์ผํ๋ ๊ฒ๋ค์ด ๋ง์์ง๋ค.<br/>
๋ก์ง์ปฌํ๊ฒ ๋ฌถ์ด์ ์๊ฐํ  ์๋ ์์!<br/>

์ด๊ฑธ ๊ฐ์ ํ๊ณ ์ ์ฐ๋ ๊ฒ์ด Object โญ๏ธ


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
new command๋ฅผ ๋ฃ์ด์ ๊ฐ์ฒด๋ฅผ ๋ง๋ค๋ฉด, Object์์ ์ ์๋ constructor๊ฐ ํธ์ถ๋๋ค!


```js

const ellie = { name: 'ellie', age: 4 };
print(ellie);

ellie.hasJob = true;
console.log(ellie.hasJob); // true
delete ellie.hasJob;
console.log(ellie.hasJob); // undefined

```
JS๋ ํ์์ด runtime(ํ๋ก๊ทธ๋จ์ด ๋์ํ๊ณ  ์์ ๋)์ ๊ฒฐ์ ๋๋ ์ธ์ด์ด๊ธฐ ๋๋ฌธ์ ์ด๋ฐ ๊ฒ๋ ๊ฐ๋ฅํจ.
 
2. Computed properties

์ ํํ๊ฒ ์ด๋ค key๊ฐ ํ์ํ์ง ๋ชจ๋ฅผ๋, ์ฆ runTime์์ ๊ฒฐ์ ๋  ๋ ์ฌ์ฉํ๋ ๋ฌธ๋ฒ <br/>
์ฝ๋ฉํ  ๋์๋ . ๋ฌธ๋ฒ์ผ๋ก ๋ถ๋ฌ์ค๋ ๊ฒ ๋ง์!

```js
console.log(ellie.name); // ellie
console.log(ellie['name']); // ellie
ellie['hasJob'] = true;
console.log(ellie['hasJob']); // true
```

object ์์์๋ ๋ณ์์ ์ด๋ฆ์ string ํํ๋ก ๋ฐ์์ฌ ์ ์๋ค

- object์ property๋ฅผ . ๋ฌธ๋ฒ์ ์ด์ฉํด์ ์ ๊ทผ์ ํ  ์ ์๊ณ 
- ๋๋ computed properties ๋ฌธ๋ฒ์ผ๋ก ๋ฐฐ์ด์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ฏ์ด ์ ๊ทผํ  ์ ์๋ค

๋จ, computed properties๋ก ๋ฐ์์ฌ ๋ key๋ ํญ์ stringํ์์ ์ง์ ํด์ ๋ฐ์์์ผํ๋ค!

<img src="/assets/images/JS_Computed_Properties.jpeg" /><br/>


3. Property value shorthand

key์ value์ ์ด๋ฆ์ด ๋์ผํ๋ค๋ฉด ์๋ตํ  ์ ์๋ค.

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

Person1,2,3์ฒ๋ผ ๋์ผํ key์ value๋ฅผ ๋ฐ๋ณต์ ์ผ๋ก ์ ๋ฌํ๋ ๊ฒ์<br/>
=> ํจ์จ์ ์ผ๋ก ๊ฐ๋ง ๋ฃ์ผ๋ฉด ์ถ๋ ฅ๋๊ฒ ๋ณ๊ฒฝ.<br/>

class template๊ณผ ๋์ผํ ๊ตฌ์กฐ. class๊ฐ ์์์ ๋๋ ์ด๋ ๊ฒ ์์ฑํ๋ค.<br/>


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
์ด๋ ๊ฒ ๋ค๋ฅธ ๊ณ์ฐ์ ํ์ง ์๊ณ , ์์ํ๊ฒ object๋ฅผ ์์ฑํ๋ ํจ์๋ค์ ๋ณดํต ๋๋ฌธ์๋ก ์์ํ๋ค.<br/>
return๋ ํ์ง ์๊ณ  ์ด๋ ๊ฒ class์ฒ๋ผ this๋ฅผ ์ฌ์ฉํ๋ค.<br/>
ํธ์ถ ์์๋ class์์ ์๋ก์ด object๋ฅผ ๋ง๋๋ ๊ฒ์ฒ๋ผ, new๋ก ํธ์ถํ  ์ ์๋ค.


5. in operator : property existance check (key in obj)

: ๊ฐ๋จํ๊ฒ key์ ์ ๋ฌด๋ฅผ ํ์ธํ  ์ ์๋ ํค์๋, ์๋ค๋ฉด true, ์๋ค๋ฉด false

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
ellie๊ฐ ๊ฐ์ง๊ณ ์๋ key๋ค์ด, ๋ธ๋ญ์ ๋ ๋๋ง๋ค <strong style="color:red">key๋ผ๋ ์ง์ญ๋ณ์์ ํ ๋น</strong>์ด ๋๋ค! <br/>

๋ชจ๋  ํค๋ค์ ๋ฐ์์์ ์ผ์ ์ฒ๋ฆฌํ๊ณ  ์ถ์ ๋ for in ์ ์ฌ์ฉํ๋ฉด ์ข๋ค.


- for (value of iterable)
: ๋ฐฐ์ด๊ณผ ๊ฐ์ ๋ฆฌ์คํธ, ์์ฐจ์ ์ผ๋ก Iterableํ ๊ฒ๋ค์ ์ด๋ค.

```js

const array = [1,2,3,4,5];
for(let i = 0; i < array.lenth; i++) {
  console.log(value);
}

```

์ด๊ฒ ๋ณด๋ค๋ ํจ์ฌ ๊ฐ๋จํ for of

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

* ๋ฐ๊พธ์ง ์๊ณ  ์ฝ๋ฉํ๋ ๋ฐฉ๋ฒ?

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
// user4 = Object.assign(user); ๋น ๊ฐ์ฒด์ด๊ธฐ ๋๋ฌธ์, ์๋์ฒ๋ผ ์ค์ผ ์ ์์

const user4 = Object.assign({ }, user );
console.log( user4 );
```
<img src="/assets/images/JS_object_assign.jpeg" /><br/>

* ๋ค๋ฅธ ์์

```js

const fruit1 = {color : 'red'};
const fruit2 = {color : 'blue', size:'big'};
const mixed = Object.assign({},fruit1, fruit2);

console.log(mixed.color); // blue
console.log(mixed.size); // big

```
์์ ๋์ผํ property๊ฐ ์๋ค๋ฉด, ๊ฐ์ด ๊ณ์ ๋ฎ์ด์์์ง๋ค



# Array์ API

* array์ object์ ์ฐจ์ด์ !

<img src="/assets/images/JS_array.jpeg" /><br/>
<img src="/assets/images/JS_array_2.jpeg" /><br/>



1. Declaration

```js

const arr1 = new Array();
const arr2 = [1,2];
```

2. Index position

```js
const fruits = ['๐','๐'];
console.log(fruits);
console.log(fruits.length);
console.log(fruits[0]); //๋ฐฐ์ด์ ์ฒซ๋ฒ์งธ ๊ฐ์ฒด๋ฅผ ์ฐพ์ ๋
console.log(fruits[1]);
console.log(fruits[2]); //undefined
console.log(fruits[fruits.length - 1]); //๋ฐฐ์ด์ ๋ง์ง๋ง ๊ฐ์ฒด๋ฅผ ์ฐพ์ ๋

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
// anonymous function์ arrow function์ผ๋ก ์ถ์ฝ ๊ฐ๋ฅ
fruits.forEach((fruit, index) => {
  console.log(fruit,index);
});

```

<img src="/assets/images/JS_forEach.jpeg" /><br/>

* Performs the specified action for each element in an array.
array์ ๋ค์ด์๋ ๊ฐ๊ฐ์ ์๋ฆฌ๋ฉํธ์ ์ ํด์ง ์ก์์ ์ํํ๋ ํจ์


๋ฐฐ์ด์ ๋ค์ด์๋ ๊ฐ ๋ง๋ค ์ฐ๋ฆฌ๊ฐ ์ ๋ฌํ ์ก์=์ฝ๋ฐฑํจ์๋ฅผ ์คํํ๋ค


4. Addition, deletion, copy

a. push : add an item to the end ๋์ ์ถ๊ฐ

```js
fruits.push('๐','๐');
```

b. pop : remove an item from the end ๋งจ ๋์ ์์ดํ์ ์ญ์ 

```js
fruits.pop();
fruits.pop();
```

c. unshift : add an item to the beginning

```js
fruits.unshift('๐','๐'); // ๋ฐฐ์ด์ ์์ ์์ดํ ์ถ๊ฐ
```

d. shift : remove an item from the beginning

```js
fruits.shift(); // ๋ฐฐ์ด์ ์์์๋ถํฐ ์์ดํ์ ์ญ์ 
```

โญ๏ธ ์ค์ โญ๏ธ<br/>
shift, unshift are slower than pop, push!

<img src="/assets/images/JS_push_pop.jpeg" /><br/>
<img src="/assets/images/JS_shift.jpeg" /><br/>

e. splice : remove an item by index position
splice(index, count)

```js
fruits.push('๐','๐','๐');
console.log(fruits);
fruits.splice(1,1); // 1๋ฒ ์ธ๋ฑ์ค์์ 1๊ฐ๋ง.
fruits.splice(1); //์ํ๋ ์ธ๋ฑ์ค๋ง ์ง์ ํ๊ณ  ๊ฐฏ์๋ฅผ ์ง์ ํ์ง ์์ผ๋ฉด, ๊ทธ ์ธ๋ฑ์ค ๋ค์ ์์ดํ์ ์น ์ง์ด๋ค
console.log(fruits);

fruits.splice(1,1,'๐','๐');
// ์ง์ฐ๊ณ  ๋์ ๊ทธ์๋ฆฌ์ ์ํ๋ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐํ  ์ ์๋ค.
fruits.splice(1,0,'๐','๐');
// ์ง์ฐ์ง ์๊ณ ! ๊ทธ ์๋ฆฌ ๋ค์๋ถํฐ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐํ  ์ ์๋ค.

```

f. concat
combine two arrays
์๋ก ๋ฌถ์ฌ์ง ๋ฐฐ์ด์ด ํฉ์ณ์ ธ์ ์๋ก ๋ฆฌํด๋จ.

```js
const fruits2 = ['๐','๐ฅ'];
const newFruits = fruits.concat(fruits2);

console.log(newFruits);
```


5. Searching

a. indexOf : find the index

```js
console.log(fruits);
console.log(fruits.indexOf('๐')); // 0
console.log(fruits.indexOf('๐')); // 3
console.log(fruits.indexOf('๐ฅ')); // -1 ํด๋น ์ธ๋ฑ์ค๊ฐ ์์ผ๋ฉด -1์ ์ถ๋ ฅ
```

b. includes

```js
console.log(fruits.includes('๐')); //true
console.log(fruits.includes('๐ฅ')); //false
``` 

c. lastIndexOf
lastIndexOf : ๋ค์์๋ถํฐ ๊ฒ์
indexOf : ์์์๋ถํฐ ๊ฒ์

```js
fruits.push('๐');
console.log(fruits); //['๐','๐','๐','๐','๐','๐'];

console.log(fruits.indexOf('๐')); // 0
console.log(fruits.lastIndexOf('๐')); // 5
```