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
: JavaScript와 동일하게 key와 object로 이루어져있음.<br/></br>

<strong>independent programming language and platform</strong></br></br>

프로그래밍 언어나 플랫폼에 상관없이 사용 가능.</br>
JSON으로 serialization된 Object를 다시 그 언어의 특징에 맞게 Object로 변환하고,</br>
Object를 다시 JSON으로 serialization 해주거나,외부 라이브러리를 통해서 가능하게 됨.</br></br>

⭐️ 공부 포인트 ⭐️

- object를 어떻게 serialize해서 JSON으로 변환할지!
- serialize된 JSON을 어떻게 deserialize해서 object로 변환할지!

# JSON

## 1. Object to JSON

```JS
JSON.
  parse(text: string, reviver?: (this: any, key: string, value: any) => any): any;
  // JSON에 string 데이터를 넣으면, 어떤 타입의 object로 변환이 된다
  // reviver 전달해도 되고 안해도 되는 callback함수. 결과값을 변환할 수 있다
  // reviver함수로 string을 object로 변환할 때, 그 과정을 좀 더 세밀하게 조정할 수 있다

  stringify(value: any, replacer?: (this: any, key: string, value: any) => any, space?: string | number): string;
  // 어떤 타입의 object를 받아와서, string으로 변환
  // string으로 만드는 과정에서 좀 더 세밀하게 통제하고 싶다면 replacer callback함수를 전달하면 됨

```
<img src="/assets/images/JS_JSON.jpeg" /><br/>



## 2. JSON to Object