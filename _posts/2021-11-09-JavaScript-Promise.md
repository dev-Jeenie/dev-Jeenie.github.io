---
title: "#12. Promise ๐ค"
permalink: /js1/Promise
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-09
last_modified_at: 2021-11-09
---

![]()


# Promise

: Promise is a JavaScript object for asynchronous operation. <br/>
: ๋น๋๊ธฐ๋ฅผ ๊ฐ๋จํ๊ฒ ์ฒ๋ฆฌํ  ์ ์๋ Object<br/>

๋คํธ์ํฌ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๊ฑฐ๋, ํ์ผ์์ ํฐ ๋ฐ์ดํฐ๋ฅผ ์ฝ์ด์ค๋ ๊ณผ์ ์ ์๊ฐ์ด ๊ฝค ๊ฑธ๋ฆฐ๋ค<br/>
์ด๋ฐ ์ผ์ ๋๊ธฐ์ , synchronous๋ก ์ฒ๋ฆฌํ๋ฉด ํ์ผ์ ์ฝ์ด์ค๊ณ , ๋คํธ์ํฌ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ ๋์ ๋ค์ ๋์์ ์ํ ๋ชปํจ.<br/>

๋น๋๊ธฐ์ ์ธ ๊ฒ์ ์ํํ  ๋, callback ํจ์ ๋์ ์ ์ ์ฉํ๊ฒ ์ธ ์ ์๋ค!<br/>
์ ํด์ง ์ฅ์๊ฐ์ ๊ธฐ๋ฅ์ ์ํํ๊ณ  ๋์, ์ ์์ ์ธ ๊ธฐ๋ฅ์ด ์ํ๋๋ค๋ฉด ์ฑ๊ณต ๋ฉ์์ง์ ์ฒ๋ฆฌ๋ ๊ฒฐ๊ณผ๊ฐ์ ์ ๋ฌ.<br/>
๊ธฐ๋ฅ ์ํ์ค์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ๋ฉด ์๋ฌ๋ฅผ ์ ๋ฌํ๋ค.<br/><br/>

* ์์
์์ง ์คํํ์ง ์์ ๊ฐ์, ์ด๋ฉ์ผ์ ์๋ ฅํด์ ๋ฏธ๋ฆฌ ๋ฑ๋กํ๋ฉด ๊ฐ์๊ฐ ์คํ๋์ ๋ ๋ฉ์ผ์ ๋ณด๋ด์ค.

A์ ๊ฒฝ์ฐ

- A๊ฐ (์์ฑ๋)promise์ ๋ฑ๋ก
- ์๊ฐ์ด ์ง๋ ํ ์ฝ์ค๊ฐ ์คํ๋๋ฉด ๋ฉ์ผ์ ๋ฐ์(promise๊ฐ ์ฑ๊ณต์ ์ผ๋ก ๊ฐ์ ์ ๋ฌํจ)


B์ ๊ฒฝ์ฐ

- B๊ฐ (์ด๋ฏธ ์ฑ๊ณต์ ์ผ๋ก ์ฒ๋ฆฌ๋)promise์ ๋ฑ๋ก
- ์ด๋ฏธ ์คํ๋์๊ธฐ ๋๋ฌธ์ ๋ฐ๋ก ๋ฉ์ผ์ ๋ฐ์


<img src="/assets/images/JS_promise.jpeg" /><br/>



 โญ๏ธ ๊ณต๋ถ ํฌ์ธํธ!
 1. state
 - Promise๊ฐ ๋ฌด๊ฑฐ์ด operation์ ์ํํ๊ณ  ์๋ ์ค์ธ์ง
 - ์๋๋ฉด ๊ธฐ๋ฅ์ํ์ด ๋๋์ ์ฑ๊ณต/์คํจํ๋์ง

 2. producer / consumer์ ์ฐจ์ด์ 
 - ์ฐ๋ฆฌ๊ฐ ์ํ๋ producer๋ฅผ producing, ์ ๊ณตํ๋ ์ฌ๋๊ณผ
 - ์ ๊ณต๋ ๋ฐ์ดํฐ๋ฅผ ์ฐ๋ ์ฌ๋, ํ์๋ก ํ๋ ์ฌ๋ consumer
<br/><br/>

1-1. state <br/>

โญ๏ธ pending => fulfilled or rejected โญ๏ธ<br/>
(์ฒ๋ฆฌ์ค => ์ฑ๊ณต or ์คํจ)<br/>

- pending
: promise๊ฐ ๋ง๋ค์ด์ ธ์ ์ฐ๋ฆฌ๊ฐ ์ง์ ํ operation์ด ์ฌ์ฉ์ค์ผ ๋

- fulfilled
: operation์ ์ฑ๊ณต์ ์ผ๋ก ๋ค ๋๋์ ๋

- rejected
: ํ์ผ์ ์ฐพ์ ์ ์๊ฑฐ๋, ๋คํธ์ํฌ์ ๋ฌธ์ ๊ฐ ์๊ฒผ์ ๋


1-2. producer vs consumer <br/>

- producer
: ์ฐ๋ฆฌ๊ฐ ์ํ๋ ๊ธฐ๋ฅ์ ์ํํด์ ํด๋นํ๋ data๋ฅผ ๋ง๋ค์ด๋ด๋, promise์ object

- consumer
: ์ฐ๋ฆฌ๊ฐ ์ํ๋ data๋ฅผ ์๋นํ๋, promise์ object


## 1. producer

: when new promise is created, the excutor runs automatically.
- promise๋ฅผ ๋ง๋๋ ์๊ฐ,์ ๋ฌํ ์ฝ๋ฐฑํจ์ excutor๊ฐ ๋ฐ๋ก ์คํ๋๋ค!

```js
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log("doing something...");
  setTimeout(() => {
    resolve("ellie");
    reject(new Error("no network"));
    // ์ฑ๊ณต์ ์ผ๋ก ๋คํธ์ํฌ์์ ๋ฐ์์จ, ํ์ผ์์ ์ฝ์ด์จ, ์ด๊ฒ๋ค์ ๊ฐ๊ณตํ ๋ฐ์ดํฐ๋ฅผ ์ฝ๋ฐฑํจ์ resolve๋ฅผ ํตํด์ ์ ๋ฌ
  }, 2000);
});
// executor๋ผ๋ ์ฝ๋ฐฑํจ์๋ฅผ ์ ๋ฌํด์ผํจ. ๊ทธ ์ฝ๋ฐฑํจ์๋ ๋ ๋ค๋ฅธ ๋๊ฐ์ง์ ์ฝ๋ฐฑํจ์๋ฅผ ๋ฐ๋๋ค
```

- => ๋ง์ฝ ์ด promise์์ ๋คํธ์ํฌ ํต์ ์ ํ๋ ์ฝ๋๋ฅผ ์์ฑํ๋ค๋ฉด, promise๊ฐ ๋ง๋ค์ด์ง๋ ์๊ฐ! ๋คํธ์ํฌ ํต์ ์ ์ํํ๊ฒ ๋๋ค

โญ๏ธ ์ฌ์ฉ์๊ฐ ์๊ตฌํ์ ๋์๋ง(๋ฒํผํด๋ฆญ) ๋คํธ์ํฌ ํต์ ์ ํด์ผํ๋ ๊ฒฝ์ฐ๊ฐ ์๋ค๋ ๊ฑธ ๊ผญ ๊ธฐ์ตํ  ๊ฒ!





## 2. consumers : then, catch, finally

- then : ๊ฐ์ด ์ ์์ ์ผ๋ก ์ํ์ด ๋๋ค๋ฉด!
- catch : ๊ฐ์ด ์ ์์ ์ผ๋ก ์ํ์ด ๋์ง ์์๋ค๋ฉด!
- finally : ์ฑ๊ณตํ๋  ์คํจํ๋  ์๊ด์์ด ๋ฌด์กฐ๊ฑด ๋ง์ง๋ง์ ํธ์ถ


```js
promise
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => console.log("finally"));
  ```

  .then์ ๋๊ฐ์ promise๋ฅผ ๋ค์ ํธ์ถํ  ์ ์๋ค. ๊ทธ๋์ ์ฐ๊ฒฐํด์ ์ธ ์ ์๋ ๊ฒ.<br/>
  (array-api์์ ๋๊ฐ์ ๋ฐฐ์ด์ ๋ฆฌํดํ๋ map์ผ๋ก ์ฒด์ด๋ํ๋ ๊ฒ์ฒ๋ผ)<br/><br/>
  ์ฑ๊ณตํ๋ค๋ฉด ๊ทธ ๊ฐ์ ๋ฐ์์์, ์ํ๋ ๊ธฐ๋ฅ์ ์ํํด์ฃผ๋ ์ฝ๋ฐฑํจ์๋ฅผ ์์ฑ<br/>

<img src="/assets/images/JS_promise_consumers.jpeg" /><br/>



## 3. Promise chaining promise ์ฐ๊ฒฐํ๊ธฐ

```js
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});
fetchNumber
  .then((num) => num * 2)
  .then((num) => num * 3)
  .then((num) => { //๋ค๋ฅธ ์๋ฒ์ ๋ณด๋ด์ ๋ค๋ฅธ ์ซ์๋ก ๋ณํ๋ ๊ฐ์ ๊ฐ์ ธ์จ๋ค
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000);
    });
  })
  .then((num) => console.log(num));
```


<img src="/assets/images/JS_promise_chaining.jpeg" /><br/>


## 4. Error Handling

```js
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve("๐"), 1000);
  });
const getEgg = (hen) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${hen} => ๐ฅ`), 1000);
    setTimeout(() => reject(new Error(`error! ${hen} => ๐ฅ`)), 1000);
  });
const cook = (egg) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => ๐ณ`), 1000);
  });
getHen()
  .then((hen) => getEgg(hen))
  .then((egg) => cook(egg))
  .then((meal) => console.log(meal));
  ```
<img src="/assets/images/JS_promise_error_handling.jpeg" /><br/>

์ฝ๋ฐฑํจ์๋ฅผ ์ ๋ฌํ  ๋, ๋ฐ์์ค๋ value๋ฅผ ๋ค๋ฅธํจ์๋ก ๋ฐ๋ก ํธ์ถํ๋ ๊ฒฝ์ฐ์๋, ์๋์ฒ๋ผ ์ถ์ฝํ  ์ ์๋ค

```js
getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log);
```

- then์์ ๋ฐ์์ค๋ value๋ฅผ ๋ฐ๋ก getEggํจ์์ ๋ฃ์ด์ ํธ์ถ<br/>
- then์์ ๋ฐ์์ค๋ value๋ฅผ ๋ฐ๋ก cookํจ์์ ๋ฃ์ด์ ํธ์ถ

```js
getHen() //
  .then(getEgg)
  .catch((error) => {
    return "๐";
  })
  .then(cook)
  .then(console.log)
  .catch(console.log);
```
์ค๊ฐ์ ๋ฌธ์ ๊ฐ ์๊ฒจ๋ ์ ์ฒด์ ์ธ promise ์ฒด์ธ์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ์ง ์๋๋ก ๋นต!๊พธ! ์ฒ๋ฆฌ๋ฅผ ํด์ค๋ค<br/>
ํน์ ๋ถ๋ถ์์ ๋ฐ์ํ๋ ์๋ฌ๋ฅผ ์ฒ๋ฆฌํ๊ณ  ์ถ์ ๋,<br/> ๋ฐ๋ก ๊ทธ ๋ค์์ catch๋ฅผ ์์ฑํด์ ๋ฐ๋ก ๋ฌธ์ ๋ฅผ ํด๊ฒฐ.๐ฅ



## 5. ๐ฉ => โจโจโจโจ (์ฝ๋ฐฑ์ง์ฅ ๊ฐ์ ํ๊ธฐ)

### (before) callback์ผ๋ก๋ง ์์ฑํ ์ฝ๋ ๐ฉ

```js
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    setTimeout(() => {
      if (
        (id === "ellie" && password === "dream") ||
        (id === "coder" && password === "academy")
      ) {
onSuccess(id);
      } else {
        onError(new Error("not found"));
      }
    }, 2000);
  }

  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === "ellie") {
        onSuccess({ name: "ellie", role: "admin" });
      } else {
        onError(new Error("not access"));
      }
    }, 1000);
  }
}

const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
userStorage.loginUser(
  id,
  password,
  (user) => {
    userStorage.getRoles(
      user,
      (userWithRole) => {
        alert(
          `Hello, ${userWithRole.name}, you have a ${userWithRole.role} role`
        );
      },

      (error) => {
        onsole.log("error");
      }
    );
  },
  (error) => console.log("error")
);
```

### (after) promise๋ก ๋ณ๊ฒฝํ ์ฝ๋! โจ

```js
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      // promise์์์ ์ฐ๋ฆฌ๊ฐ ์ํ๋ ๋ก๊ทธ์ธ ๊ธฐ๋ฅ์ ์ํํ๋ ํจ์๋ฅผ ๋ฃ๊ณ 
      setTimeout(() => {
        if (
          (id === "ellie" && password === "dream") ||
          (id === "coder" && password === "academy")
        ) {
          resolve(id);
        } else {
          reject(new Error("not found"));
        }
      }, 2000);
    });
  }

  getRoles(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === "ellie") {
          resolve({ name: "ellie", role: "admin" });
        } else {
          reject(new Error("not access"));
        }
      }, 1000);
    });
  }
}

const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
userStorage
  .loginUser(id, password) //loginUser๋ฅผ ํธ์ถํค์ id์ psw๋ฅผ ์๋ ค์ค
  .then((user) => userStorage.getRoles(user)) // ์๋ ค์ฃผ๋๋ฐ ์ฑ๊ณตํ๋ฉด
  .then((user) => alert(`Hello, ${user.name}, you have a ${user.role} role`)) //์ถ๋ ฅ
  .catch(console.log);

```

