---
title: "#13. async & await 🍭"
permalink: /cs/asyncawait
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-09
last_modified_at: 2021-11-09
---

![]()

# async / await이란?

: promise를 좀 더 간편하고 동기적으로 실행되는 것처럼 보이게 만들어주는 것.<br/>

동기식으로 코드를 순서대로 작성하는 것처럼, 간편해진다✨

* syntactic sugar
덧붙여진, 그럴싸해 보이는<br/>
async / await은 새로운게 추가된 게 아닌, promise 위에 API를 제공한 것.<br/>

=> 이렇게 기존에 존재하는 것 위에, 또는 감싸서 간편하게 쓸 수 있게 제공하는 것이 syntactic sugar!(e.g. class)



## 1. async

### 1-1. 비동기처리 안했을 경우

```JS
function fetchUser() {
do network request in 10 secs ...
  return "ellie";
}

const user = fetchUser();
console.log(user);
```
<img src="/assets/images/JS_async_await.jpeg" /><br/>


### 1-2. promise로 비동기처리 했을 경우

```JS
function fetchUser() {
  return new Promise((resolve, reject) => {
    resolve("ellie");
  });
}
const user = fetchUser();
user.then(console.log);
console.log(user);
```
promise는?<br/>
"내가 언제 데이터를 받아올지는 모르겠지만, 이 Promise라는 object만 가지고있으면,<br/>
then이라는 콜백함수만 등록해놓으면, 데이터가 준비되는 대로 너가 준비한 콜백함수를 불러줄게!"<br/>

resolve, reject를 호출하지 않고 return하면 Promise가 계속 진행중이라고 남아있음.<br/>
=> 그래서 promise안에는 꼭 resolve, reject를 이용해서 완료를 해줘야함!<br/>

### 1-3. promise에 async까지 붙인 경우


```JS
async function fetchUser() {
  return "ellie";
}
const user = fetchUser();
user.then(console.log);
console.log(user);
```
async를 함수 앞에 쓰면, 코드블럭이 자동적으로 Promise로 바뀐다!<br/>
async는 promise를 감싸고있는, promise를 조금 더 간편하게 쓸 수 있는 키워드<br/>





## 2. await

```JS
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(3000);
  return "🍎";
}

async function getBanana() {
  await delay(3000);
  return "🍌";
}
```
await은 async가 붙은 함수 안에서만 사용할 수 있다!<br/>
함수 delay는, 정해진 ms가 지나면 resolve를 호출하는 promise를 return한다<br/>

=> getApple에서는 3초를 전달했으니 3초 뒤에 resolve를 호출!<br/><br/>

await을 쓰면, delay 끝날 때까지 기다려준다<br/>
동기적인 코드를 짜는 것처럼<br/><br/>

getBanana를 async가 아닌 promise만으로 쓴다면? 체이닝을 해야한다.<br/>
```JS
function getBanana() {
  return delay(3000).then(() => "🍌");
}
```

* 두개의 promise를 한번에 써야한다면? <br/>

```JS
function pickFruits() {
  return getApple().then((apple) => {
    return getBanana().then((banana) => `${apple} + ${banana}`);
  });
}
pickFruits().then(console.log);
```

promise도 너무 이렇게 중첩적으로 chaining을 하게되면 콜백지옥과 비슷한 문제가 발생.

```JS
async function pickFruits() {
  const apple = await getApple();
  const banana = await getBanana();
  return `${apple} + ${banana}`;
}

pickFruits().then(console.log);
```

async로 하니까 짱편하다!

```JS
async function pickFruits() {
  try {
    const apple = await getApple();
    const banana = await getBanana();
  } catch {}
}
return `${apple} + ${banana}`;

pickFruits().then(console.log);
```

에러처리 또한 이런식으로 try catch로 할 수 있다.

## 4. async 병렬처리 ⭐️⭐️

사과에 1초, 바나나에 1초... 순차적으로 진행하는건 비효율적!<br/>
서로 연관이 되어있지 않기 때문에, 서로 기다릴 필요가 전혀 없다<br/>

```JS
async function pickFruits() {
  const applePromise = getApple();
  const bananaPromise = getBanana();
  const apple = await applePromise;
  const banana = await bananaPromise;
  return `${apple} + ${banana}`;
}

pickFruits().then(console.log);
```

promise는 만드는 순간, 그 안에 들어있는 코드블럭이 실행된다!!!<br/>
이렇게 만들자마자 promise를 실행시키고, 각 apple과 banana에는 이미 실행시킨 promise를 넣으면 병렬적으로 일어남!<br/>
이젠 1초 걸림<br/>




## 5. useful Promise APIs

### 5-1. Promise.all
: promise 배열을 전달하게 되면, 모든 promise들이 병렬화됨. 다 받을 때까지 모아준다<br/>
⭐️⭐️⭐️ 사과를 가져오는데에 바나나가 필요없고, 바나나를 가져오는데 사과가 필요없는 이러한 병렬적인 구조에서 사용이 가능한 API.<br/>

```JS
function pickAllFruits() {
  return (
    Promise.all([getApple(), getBanana()])
      // 이 promise배열이 다 받아지면!
      .then((fruits) => fruits.join("+"))
    // 다 받아진 배열이 다시 전달이 된다
    // 그 배열을 구분자로 나눠 string으로 묶어라
  );
}

pickAllFruits().then(console.log);
```

### 5-2. Promise.race
: promise 배열을 전달하게 되면, 딱 하나만 먼저 수행되는 것이 전달되면 걔를 출력한다

```JS
function pickOnlyOne() {
  return Promise.race([getApple(), getBanana()]);
}
pickOnlyOne().then(console.log);
```

## 6. 숙제!

```JS
const userStorage = new UserStorage();
const id = prompt("enter your id");
const password = prompt("enter your password");
userStorage
  .loginUser(id, password) //loginUser를 호출헤서 id와 psw를 알려줌
  .then((user) => userStorage.getRoles(user)) // 알려주는데 성공하면
  .then((user) => alert(`Hello, ${user.name}, you have a ${user.role} role`))
  .catch(console.log);
```
이 부분을 async await을 이용해서 깔끔하게 작성해오기!
