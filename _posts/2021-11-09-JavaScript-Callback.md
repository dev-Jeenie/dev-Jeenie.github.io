---
title: "#11. Callback (feat.콜백지옥 🔥)"
permalink: /js1/Callback
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-09
last_modified_at: 2021-11-09
---

![]()
"우리가 전달한 함수를 나중에 불러줘"
# CallBack
"우리가 전달한 함수를 나중에 불러줘"

## 1. 동기와 비동기

JavaScript is asynchronous. JS는 동기적이다<br/>
호이스팅 된 이후부터 작성한 순서에 맞춰 코드가 하나씩 동기적으로 실행된다<br/>
Execute the code block by order after hoisting.<br/>

⭐️ hoisting이란?<br/>
var,function declaration이 제일 위로 올라가는 것<br/>
 ⭐️⭐️함수의 선언은 제일 위로!!!!⭐️⭐️<br/>
호이스팅이 된 이후부터, 코드가 나타나는 대로, 자동적으로 실행된다<br/>

## asynchronous 비동기적으로 언제 코드가 실행될지 예측할 수 없는 것
```js
console.log(1);
setTimeout(() => console.log(2), 1000);
console.log(3);
// JS엔진은 코드를 위부터 아래로 실행한다.

function setTimeout(handler: TimerHandler, timeout?: number, ...arguments: any[]): number;
// TimeHandler라는 callback함수와, timeout으로 시간을 지정한다

```
<img src="/assets/images/JS_callback.jpeg" /><br/>

<img src="/assets/images/JS_callback.jpeg" /><br/>

## 1-1. Synchronous callback
: 즉각적, 동기적으로 실행
<br/>

```js
function printImmediately(print) {
  print();
}

// callback함수를 받아서 callback을 바로 실행하는 함수를 만들었다.
// callback함수를 사용하기 위해서, print로 callback함수를 받을 자리를 만들어놓는다.

printImmediately(() => console.log("hello"));
```

- ⭐️ JS엔진이 어떻게 이해했을까? hoisting!
<img src="/assets/images/JS_Synchronous.jpeg" /><br/>

## 1-2. Asynchronous callback
: 나중에,언제될지 알 수 없는 비동기적으로 실행

```js
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}
printWithDelay(() => console.log("async callback"), 2000);
// 우리가 원하는 기능을 동작하는 callback 함수를 전달해야함
```

- ⭐️ JS엔진이 어떻게 이해했을까? hoisting!
<img src="/assets/images/JS_Asynchronous.jpeg" /><br/>

## callback hell example
```js
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    // callback함수를 넣기 위한 자리를 만들어둠.
    // parameter를 그냥 받을 수도있고 callback함수로 받을 수도 있다

    setTimeout(() => {
      if (
        (id === "ellie" && password === "dream") ||
        (id === "coder" && password === "academy")
      ) {
        onSuccess(id); 전달받은 onSuccess를 부르고 id를 전달한다
      } else {
        onError(new Error("not found"));
      }
    }, 2000);
  }

  //역할 받아올 때
  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === "ellie") {
        onSuccess({ name: "ellie", role: "admin" });
        전달받은 onSuccess를 부르고 name과 role을 전달한다
      } else {
        onError(new Error("not access"));
      }
    }, 1000);
  }
}
```

<img src="/assets/images/JS_callback_hell.jpeg" /><br/>
<img src="/assets/images/JS_callback_todo.jpeg" /><br/>


```js
const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
// 사용자의 id, password를 받아오고
userStorage.loginUser(
  id,
  password,
  (user) => {
    userStorage.getRoles(
      user,
      (userWithRole) => {
        alert(`Hello, ${user.name}, you have a ${user.role} role`);
        // 로그인했을 때 user는 id만 있음.
        alert(
          `Hello, ${userWithRole.name}, you have a ${userWithRole.role} role`
        );
      },
        //이게 실행되려면, loginUser 성공 + getRoles 성공
      (error) => {
        onsole.log("error");
      }
    );
  },
  //사용자가 로그인 성공하면, userStorage에서 getRole로 역할을 받아와야함
  (error) => console.log("error")
);
// 로그인을 해야함. userStorage의 loginUser에 받아온 id와 password를 전달
```

<img src="/assets/images/JS_callback_hell_2.jpeg" /><br/>


콜백 함수 안에서 다른것을 호출하고, 그 안에서 또다른 콜백을 전달하고, 호출하고 전달전달....<br/>
=>콜백 지옥!<br/>

이 콜백지옥의 순서!

- 로그인한 다음에(loginUser)
- 그 로그인한 데이터를 이용해서(userStorage)
- 사용자의 역할을 받아오는구나(getRoles)

문제점!
- 가독성이 매우 떨어지고, 위와같은 비즈니스 로직을 이해하는 것도 힘들다
- 에러발생시, 체인이 길수록 디버깅이 힘들다

비동기 함수를 쓰려면 callback지옥을 만들 수 밖에 없는데, 그럼 비동기 코드를 깔끔하게 쓰려면 어떻게 해??<br/>
다음편,Promise에서!<br/>
