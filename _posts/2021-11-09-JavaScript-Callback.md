---
title: "#11. Callback (feat.์ฝ๋ฐฑ์ง์ฅ ๐ฅ)"
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
"์ฐ๋ฆฌ๊ฐ ์ ๋ฌํ ํจ์๋ฅผ ๋์ค์ ๋ถ๋ฌ์ค"
# CallBack
"์ฐ๋ฆฌ๊ฐ ์ ๋ฌํ ํจ์๋ฅผ ๋์ค์ ๋ถ๋ฌ์ค"

## 1. ๋๊ธฐ์ ๋น๋๊ธฐ

JavaScript is asynchronous. JS๋ ๋๊ธฐ์ ์ด๋ค<br/>
ํธ์ด์คํ ๋ ์ดํ๋ถํฐ ์์ฑํ ์์์ ๋ง์ถฐ ์ฝ๋๊ฐ ํ๋์ฉ ๋๊ธฐ์ ์ผ๋ก ์คํ๋๋ค<br/>
Execute the code block by order after hoisting.<br/>

โญ๏ธ hoisting์ด๋?<br/>
var,function declaration์ด ์ ์ผ ์๋ก ์ฌ๋ผ๊ฐ๋ ๊ฒ<br/>
 โญ๏ธโญ๏ธํจ์์ ์ ์ธ์ ์ ์ผ ์๋ก!!!!โญ๏ธโญ๏ธ<br/>
ํธ์ด์คํ์ด ๋ ์ดํ๋ถํฐ, ์ฝ๋๊ฐ ๋ํ๋๋ ๋๋ก, ์๋์ ์ผ๋ก ์คํ๋๋ค<br/>

## asynchronous ๋น๋๊ธฐ์ ์ผ๋ก ์ธ์  ์ฝ๋๊ฐ ์คํ๋ ์ง ์์ธกํ  ์ ์๋ ๊ฒ
```js
console.log(1);
setTimeout(() => console.log(2), 1000);
console.log(3);
// JS์์ง์ ์ฝ๋๋ฅผ ์๋ถํฐ ์๋๋ก ์คํํ๋ค.

function setTimeout(handler: TimerHandler, timeout?: number, ...arguments: any[]): number;
// TimeHandler๋ผ๋ callbackํจ์์, timeout์ผ๋ก ์๊ฐ์ ์ง์ ํ๋ค

```
<img src="/assets/images/JS_callback.jpeg" /><br/>

<img src="/assets/images/JS_callback.jpeg" /><br/>

## 1-1. Synchronous callback
: ์ฆ๊ฐ์ , ๋๊ธฐ์ ์ผ๋ก ์คํ
<br/>

```js
function printImmediately(print) {
  print();
}

// callbackํจ์๋ฅผ ๋ฐ์์ callback์ ๋ฐ๋ก ์คํํ๋ ํจ์๋ฅผ ๋ง๋ค์๋ค.
// callbackํจ์๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํด์, print๋ก callbackํจ์๋ฅผ ๋ฐ์ ์๋ฆฌ๋ฅผ ๋ง๋ค์ด๋๋๋ค.

printImmediately(() => console.log("hello"));
```

- โญ๏ธ JS์์ง์ด ์ด๋ป๊ฒ ์ดํดํ์๊น? hoisting!
<img src="/assets/images/JS_Synchronous.jpeg" /><br/>

## 1-2. Asynchronous callback
: ๋์ค์,์ธ์ ๋ ์ง ์ ์ ์๋ ๋น๋๊ธฐ์ ์ผ๋ก ์คํ

```js
function printWithDelay(print, timeout) {
  setTimeout(print, timeout);
}
printWithDelay(() => console.log("async callback"), 2000);
// ์ฐ๋ฆฌ๊ฐ ์ํ๋ ๊ธฐ๋ฅ์ ๋์ํ๋ callback ํจ์๋ฅผ ์ ๋ฌํด์ผํจ
```

- โญ๏ธ JS์์ง์ด ์ด๋ป๊ฒ ์ดํดํ์๊น? hoisting!
<img src="/assets/images/JS_Asynchronous.jpeg" /><br/>

## callback hell example
```js
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    // callbackํจ์๋ฅผ ๋ฃ๊ธฐ ์ํ ์๋ฆฌ๋ฅผ ๋ง๋ค์ด๋ .
    // parameter๋ฅผ ๊ทธ๋ฅ ๋ฐ์ ์๋์๊ณ  callbackํจ์๋ก ๋ฐ์ ์๋ ์๋ค

    setTimeout(() => {
      if (
        (id === "ellie" && password === "dream") ||
        (id === "coder" && password === "academy")
      ) {
        onSuccess(id); ์ ๋ฌ๋ฐ์ onSuccess๋ฅผ ๋ถ๋ฅด๊ณ  id๋ฅผ ์ ๋ฌํ๋ค
      } else {
        onError(new Error("not found"));
      }
    }, 2000);
  }

  //์ญํ  ๋ฐ์์ฌ ๋
  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === "ellie") {
        onSuccess({ name: "ellie", role: "admin" });
        ์ ๋ฌ๋ฐ์ onSuccess๋ฅผ ๋ถ๋ฅด๊ณ  name๊ณผ role์ ์ ๋ฌํ๋ค
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
// ์ฌ์ฉ์์ id, password๋ฅผ ๋ฐ์์ค๊ณ 
userStorage.loginUser(
  id,
  password,
  (user) => {
    userStorage.getRoles(
      user,
      (userWithRole) => {
        alert(`Hello, ${user.name}, you have a ${user.role} role`);
        // ๋ก๊ทธ์ธํ์ ๋ user๋ id๋ง ์์.
        alert(
          `Hello, ${userWithRole.name}, you have a ${userWithRole.role} role`
        );
      },
        //์ด๊ฒ ์คํ๋๋ ค๋ฉด, loginUser ์ฑ๊ณต + getRoles ์ฑ๊ณต
      (error) => {
        onsole.log("error");
      }
    );
  },
  //์ฌ์ฉ์๊ฐ ๋ก๊ทธ์ธ ์ฑ๊ณตํ๋ฉด, userStorage์์ getRole๋ก ์ญํ ์ ๋ฐ์์์ผํจ
  (error) => console.log("error")
);
// ๋ก๊ทธ์ธ์ ํด์ผํจ. userStorage์ loginUser์ ๋ฐ์์จ id์ password๋ฅผ ์ ๋ฌ
```

<img src="/assets/images/JS_callback_hell_2.jpeg" /><br/>


์ฝ๋ฐฑ ํจ์ ์์์ ๋ค๋ฅธ๊ฒ์ ํธ์ถํ๊ณ , ๊ทธ ์์์ ๋๋ค๋ฅธ ์ฝ๋ฐฑ์ ์ ๋ฌํ๊ณ , ํธ์ถํ๊ณ  ์ ๋ฌ์ ๋ฌ....<br/>
=>์ฝ๋ฐฑ ์ง์ฅ!<br/>

์ด ์ฝ๋ฐฑ์ง์ฅ์ ์์!

- ๋ก๊ทธ์ธํ ๋ค์์(loginUser)
- ๊ทธ ๋ก๊ทธ์ธํ ๋ฐ์ดํฐ๋ฅผ ์ด์ฉํด์(userStorage)
- ์ฌ์ฉ์์ ์ญํ ์ ๋ฐ์์ค๋๊ตฌ๋(getRoles)

๋ฌธ์ ์ !
- ๊ฐ๋์ฑ์ด ๋งค์ฐ ๋จ์ด์ง๊ณ , ์์๊ฐ์ ๋น์ฆ๋์ค ๋ก์ง์ ์ดํดํ๋ ๊ฒ๋ ํ๋ค๋ค
- ์๋ฌ๋ฐ์์, ์ฒด์ธ์ด ๊ธธ์๋ก ๋๋ฒ๊น์ด ํ๋ค๋ค

๋น๋๊ธฐ ํจ์๋ฅผ ์ฐ๋ ค๋ฉด callback์ง์ฅ์ ๋ง๋ค ์ ๋ฐ์ ์๋๋ฐ, ๊ทธ๋ผ ๋น๋๊ธฐ ์ฝ๋๋ฅผ ๊น๋ํ๊ฒ ์ฐ๋ ค๋ฉด ์ด๋ป๊ฒ ํด??<br/>
๋ค์ํธ,Promise์์!<br/>
