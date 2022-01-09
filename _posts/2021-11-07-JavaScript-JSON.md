---
title: "#10. JSON 🍫"
permalink: /cs/JavaScriptJSON
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-07
last_modified_at: 2021-11-08
---

![]()

브라우저에서 서버와 통신을 할 때는, fetch API를 사용하거나 XMLHttpRequest 오브젝트를 이용.<br/>

JSON(JavaScript Object Notation)<br/>
: JavaScript와 동일하게 key와 object로 이루어져있음.<br/><br/>

<strong>independent programming language and platform</strong><br/><br/>

프로그래밍 언어나 플랫폼에 상관없이 사용 가능.<br/>
JSON으로 serialization된 Object를 다시 그 언어의 특징에 맞게 Object로 변환하고,<br/>
Object를 다시 JSON으로 serialization 해주거나,외부 라이브러리를 통해서 가능하게 됨.<br/><br/>

⭐️ 공부 포인트 ⭐️

<img src="/assets/images/JS_JSON_serialize.jpeg" /><br/>

- object를 어떻게 <strong style="color:#3498db">serialize</strong>해서 JSON으로 변환할지!
- serialize된 JSON을 어떻게 <strong style="color:#3498db">deserialize</strong>해서 object로 변환할지!

# JSON
<img src="/assets/images/JS_JSON.jpeg" /><br/>

## 1. Object to JSON

- stringify(obj)
: object를 JSON으로 변환할 수 있다

<img src="/assets/images/JS_JSON_overloading.jpeg" /><br/>

* interface JSON <br/>

parse()
- JSON에 string 데이터를 넣으면, 어떤 타입의 object로 변환이 된다
- reviver 전달해도 되고 안해도 되는 callback 함수. 결과값을 변환할 수 있다
- reviver함수로 string을 object로 변환할 때, 그 과정을 좀 더 세밀하게 조정할 수 있다

stringify()
- 어떤 타입의 object를 받아와서, string으로 변환
- string으로 만드는 과정에서 좀 더 세밀하게 통제하고 싶다면 replacer callback 함수를 전달하면 됨

```js

let json = JSON.stringify(true);
// boolean 타입의 primitive 타입도 JSON으로 변환이 가능
console.log(json); // true

```

### 배열을 JSON화

```js

json = JSON.stringify(["apple", "banana"]);
console.log(json); //["apple","banana"]

```
### object를 JSON화

```js

const rabbit = {
  name: "tori",
  color: "white",
  size: null,
  // Symbol: Symbol("id"),
  birthDate: new Date(),
  jump: () => {
    console.log(`${this.name} can jump!`);
  },
};
json = JSON.stringify(rabbit);
console.log(json);
```

<img src="/assets/images/JS_JSON_serialize_deserialize.jpeg" /><br/>

- JSON에 jump는 포함되지 않는다. 함수는 object에 포함된 데이터가 아니기 때문에 제외됨
- Symbol같은 JavaScript에만 있는 특별한 데이터도 JSON에 포함되지 않는다

<br/>

JSON으로 변환되는 것을 조금 더 통제하고 싶다면? replacer!

- replacer

a. replacer에 배열로 전달하기

```js
json = JSON.stringify(rabbit, ["name", "color"]);
console.log(json);
// {"name":"tori"} 출력
```
이렇게 내가 원하는 Property명만 골라서 정의를 하면, 해당 Property만 JSON으로 변환된다


b. replacer에 callback 함수로 전달하기

```js

json = JSON.stringify(rabbit, (key, value) => {
  console.log(`key: ${key}, value:${value}`);
  return key == "name" ? "ellie" : value;
  // key가 name이면 ellie로 바꾸고, 아닌것들은 그냥 원래의 value를 써야지
});
console.log(json);
/*
key: , value:[object Object] << rabit object를 싸고있는 제일 최상의 것이 전달된 뒤부터 key와 value들이 전달된다
key: name, value:tori
key: color, value:white
key: size, value:null
key: birthDate, value:2021-11-07T15:32:21.841Z
key: jump, value:() => {
    console.log(`${this.name} can jump!`);
  }
{"name":"tori","color":"white","size":null,"birthDate":"2021-11-07T15:32:21.841Z"}
모든 key와 value들이 callback함수에 전달된다

{"name":"ellie","color":"white","size":null,"birthDate":"2021-11-07T15:32:21.841Z"}
이름만 ellie로 변경됨

*/


```



## 2. JSON to Object

- parse(json)
: JSOND을 object로 변환할 수 있다

```js

console.clear();
json = JSON.stringify(rabbit); //객체를 JSON화 하고
const obj = JSON.parse(json); //JSON을 객체화 한다

```

<br/>

객체로 변환되는 것을 조금 더 통제하고 싶다면? reviver!

- reviver


```js
const obj = JSON.parse(json, (key, value) => {
  console.log(`key: ${key}, value:${value}`);
  return key === "birthDate" ? new Date(value) : value;
  // key가 birthDate라면, 새로운 객체를 만들겠다
});
console.log(obj);

rabbit.jump();
// obj.jump(); // error
```
<img src="/assets/images/JS_JSON_jump.jpeg" /><br/>


```js


console.log(rabbit.birthDate.getDate());
// object birthDate는 Date라는 object임.
// 그래서 Date안에 존재하는 API인 getDate를 쓸 수 있다
console.log(obj.birthDate.getDate());
// JSON으로부터 만든 object는 error가 난다.
//obj.birthDate 는 string이기 때문

```
다시 세밀하게 Date로 변환하고 싶으면, <br/>
parse할 때(객체로 변환할 때) reviver라는 callback함수를 전달할 수 있다

<img src="/assets/images/JS_JSON_object_to_JSON.jpeg" /><br/>


< 참고 >
- JSON data 비교 사이트 http://www.jsondiff.com/ (디버깅시 유용)
- JSON data 깨졌을 때 예쁘게 해주는 사이트 https://jsonbeautifier.org/
- JSON data object형태로 보여주는 사이트 https://jsonparser.org/
- JSON data 유효성 검사 사이트 https://tools.learningcontainer.com/json-validator/
