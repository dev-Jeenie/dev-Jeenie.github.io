---
title: "#12. Promise 🤙"
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
: 비동기를 간단하게 처리할 수 있는 Object<br/>

네트워크에서 데이터를 받아오거나, 파일에서 큰 데이터를 읽어오는 과정은 시간이 꽤 걸린다<br/>
이런 일을 동기적, synchronous로 처리하면 파일을 읽어오고, 네트워크에서 데이터를 받아오는 동안 다음 동작을 수행 못함.<br/>

비동기적인 것을 수행할 때, callback 함수 대신에 유용하게 쓸 수 있다!<br/>
정해진 장시간의 기능을 수행하고 나서, 정상적인 기능이 수행됐다면 성공 메시지와 처리된 결과값을 전달.<br/>
기능 수행중에 문제가 발생히면 에러를 전달한다.<br/><br/>

* 예시
아직 오픈하지 않은 강의, 이메일을 입력해서 미리 등록하면 강의가 오픈됐을 때 메일을 보내줌.

A의 경우

- A가 (생성된)promise에 등록
- 시간이 지난 후 코스가 오픈되면 메일을 받음(promise가 성공적으로 값을 전달함)


B의 경우

- B가 (이미 성공적으로 처리된)promise에 등록
- 이미 오픈되었기 때문에 바로 메일을 받음


<img src="/assets/images/JS_promise.jpeg" /><br/>



 ⭐️ 공부 포인트!
 1. state
 - Promise가 무거운 operation을 수행하고 있는 중인지
 - 아니면 기능수행이 끝나서 성공/실패했는지

 2. producer / consumer의 차이점
 - 우리가 원하는 producer를 producing, 제공하는 사람과
 - 제공된 데이터를 쓰는 사람, 필요로 하는 사람 consumer
<br/><br/>

1-1. state <br/>

⭐️ pending => fulfilled or rejected ⭐️<br/>
(처리중 => 성공 or 실패)<br/>

- pending
: promise가 만들어져서 우리가 지정한 operation이 사용중일 때

- fulfilled
: operation을 성공적으로 다 끝냈을 때

- rejected
: 파일을 찾을 수 없거나, 네트워크에 문제가 생겼을 때


1-2. producer vs consumer <br/>

- producer
: 우리가 원하는 기능을 수행해서 해당하는 data를 만들어내는, promise의 object

- consumer
: 우리가 원하는 data를 소비하는, promise의 object


## 1. producer

: when new promise is created, the excutor runs automatically.
- promise를 만드는 순간,전달한 콜백함수 excutor가 바로 실행된다!

```js
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log("doing something...");
  setTimeout(() => {
    resolve("ellie");
    reject(new Error("no network"));
    // 성공적으로 네트워크에서 받아온, 파일에서 읽어온, 이것들을 가공한 데이터를 콜백함수 resolve를 통해서 전달
  }, 2000);
});
// executor라는 콜백함수를 전달해야함. 그 콜백함수는 또 다른 두가지의 콜백함수를 받는다
```

- => 만약 이 promise안에 네트워크 통신을 하는 코드를 작성했다면, promise가 만들어지는 순간! 네트워크 통신을 수행하게 된다

⭐️ 사용자가 요구했을 때에만(버튼클릭) 네트워크 통신을 해야하는 경우가 있다는 걸 꼭 기억할 것!





## 2. consumers : then, catch, finally

- then : 값이 정상적으로 수행이 된다면!
- catch : 값이 정상적으로 수행이 되지 않았다면!
- finally : 성공하든 실패하든 상관없이 무조건 마지막에 호출


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

  .then은 똑같은 promise를 다시 호출할 수 있다. 그래서 연결해서 쓸 수 있는 것.<br/>
  (array-api에서 똑같은 배열을 리턴하는 map으로 체이닝했던 것처럼)<br/><br/>
  성공했다면 그 값을 받아와서, 원하는 기능을 수행해주는 콜백함수를 작성<br/>

<img src="/assets/images/JS_promise_consumers.jpeg" /><br/>



## 3. Promise chaining promise 연결하기

```js
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});
fetchNumber
  .then((num) => num * 2)
  .then((num) => num * 3)
  .then((num) => { //다른 서버에 보내서 다른 숫자로 변환된 값을 가져온다
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
    setTimeout(() => resolve("🐓"), 1000);
  });
const getEgg = (hen) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${hen} => 🥚`), 1000);
    setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000);
  });
const cook = (egg) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 🍳`), 1000);
  });
getHen()
  .then((hen) => getEgg(hen))
  .then((egg) => cook(egg))
  .then((meal) => console.log(meal));
  ```
<img src="/assets/images/JS_promise_error_handling.jpeg" /><br/>

콜백함수를 전달할 때, 받아오는 value를 다른함수로 바로 호출하는 경우에는, 아래처럼 축약할 수 있다

```js
getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log);
```

- then에서 받아오는 value를 바로 getEgg함수에 넣어서 호출<br/>
- then에서 받아오는 value를 바로 cook함수에 넣어서 호출

```js
getHen() //
  .then(getEgg)
  .catch((error) => {
    return "🐖";
  })
  .then(cook)
  .then(console.log)
  .catch(console.log);
```
중간에 문제가 생겨도 전체적인 promise 체인에 문제가 발생하지 않도록 빵!꾸! 처리를 해준다<br/>
특정부분에서 발생하는 에러를 처리하고 싶을 땐,<br/> 바로 그 다음에 catch를 작성해서 바로 문제를 해결.🔥



## 5. 💩 => ✨✨✨✨ (콜백지옥 개선하기)

### (before) callback으로만 작성한 코드 💩

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

### (after) promise로 변경한 코드! ✨

```js
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      // promise안에서 우리가 원하는 로그인 기능을 수행하는 함수를 넣고
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
  .loginUser(id, password) //loginUser를 호출헤서 id와 psw를 알려줌
  .then((user) => userStorage.getRoles(user)) // 알려주는데 성공하면
  .then((user) => alert(`Hello, ${user.name}, you have a ${user.role} role`)) //출력
  .catch(console.log);

```

