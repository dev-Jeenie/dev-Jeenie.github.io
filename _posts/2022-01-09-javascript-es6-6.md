---
title: "Java script ES6💫 제대로 알아보기! ✍️ (6) spread operator"
permalink: /js2/javascriptEs66
tags:
  - [es6]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-14
last_modified_at: 2022-01-14
---

![]()

## 1. spread operator(펼치기 연산자, 전개 연산자)

<img src="/assets/images/es6-spread-operator.png" /><br/>

## 2. 상세

### 2-1. 배열의 각 인자를 **펼친 효과**

spread operator는 `( , ) 로 나열`할 수 있는 거라면 `모두 가능`하다.<br/>

<img src="/assets/images/es6-spread-operator-2.png" /><br/>




<img src="/assets/images/es6-spread-operator-3.png" /><br/>


> Math.max()<br/>
인자로 넘어온 것들 중 최대 값을 알려준다<br/>
괄호 안에 인자의 갯수를 한정짓지 않고 많이 받음.<br/>

배열의 요소들을 넘겨주고 싶은데, 인자가 몇개이고 뭐가 들어갈지 모르는 상태라 하나하나 다 작성하는 수 밖에 없음.<br/>
이 경우에 최댓값을 찾기 위해서는 apply를 사용.<br/>
apply는 요소들의 집합을 두번째 인자로 받으니, 첫번째 인자로 두번째 인자로 배열을 넘겨준다.<br/>

그런데 `spread operator`를 사용하면 간단히 해결!<br/>

### 2-2. **앞 뒤로 다른 값**들을 함께 사용 가능

`rest parameter`는, **인자를 받는 입장**이었으니 인자의 `맨 뒤에서만` 쓸 수 있었다. <br/>
하지만, `spread operator`는 받는 것이 아닌 `주는 것`!<br/>
내가 갖고있던 것들을 펼쳐서 내 값은 이거이거야~ 하고 알려주는 것.<br/>
그러니까 앞 뒤에 뭐가 오든 아무 상관이 없다.<br/>
`앞, 뒤, 중간` 어디서든 사용 가능.

```js
const values = [3,4,5,6,7,8]
const sum = (...args) => args.reduce((p,c) => p + c)
console.log(sum(1,2, ...values, 9,10))
```

sum이라는 함수는 `인자의 갯수를 상관하지 않고` 모든 요소들을 총합을 구해주는 함수.<br/>
sum을 실행하고 그 인자로써 **1, 2, value의 요소들, 9,10**을 넘겨줬다.<br/>
그래서 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10이 sum의 인자로 들어가서 결과인 55가 출력된 것.

**...은 `rest parameter`일 수도, `spread operator`일 수도 있다**

🙋‍♀️ : 그럼 ...은 어떨 때에는 나머지고, 어떨 때에는 펼치기야? <br/>

- `getter`(받는 입장) : `나머지`
- `setter`(주는 입장) : `펼치기`

<img src="/assets/images/es6-spread-operator-4.jpeg" /><br/>


### 2-4. 모든 iterable한 데이터를 펼칠 수 있다.

- iterable(반복될 수 있는)

반복할 수 있는 모든 데이터는 펼칠 수 있다.


<img src="/assets/images/es6-spread-operator-5.png" /><br/>

### 2-5. push, unshift, concat을 대체할 수 있다

```js
let originalArr = [2, 3]
const preArr    = [-2, -1]
const sufArr    = [6, 7]

originalArr.unshift(1)
originalArr.push(4)
originalArr = [0, ...originalArr, 5] // 새로운 배열을 할당
console.log(originalArr)

const concatArr = preArr.concat(originalArr, sufArr)
const restArr = [...preArr, ...originalArr, ...sufArr]
console.log(concatArr, restArr)

```
<img src="/assets/images/es6-spread-operator-6.png" /><br/>

🤷🏻‍♀️ : 왜 새로 만들어서 메모리를 낭비하지? ❌<br/>

새로 생겼으니까, 이 새로 만든 값을 기존 변수에 대해서 `참조`를 시키면<br/>
**참조를 하지 않는 위치**에 있는 값은 `자동으로 사라지니까`<br/>
새로 만드는게 **전혀 문제가 되지 않는다!**<br/>

오히려 배열의 앞에 값을 집어넣는 unshift가 비용이 더 든다.<br/>


### 2-6. 얕은 복사만을 수행한다

```js
let originalArray = [{
  first: 'Hello,',
  second: 'World!'
}, {
  first: 'Welcome',
  second: 'ES6!'
}]
let copiedArray = [...originalArray]
console.log(originalArray[0].first)

copiedArray[0].first = "Hi,"
console.log(originalArray[0].first)
```
spread operator로 원본배열을 복사했지만,<br/>

왜? 요소만 얕은 복사하고, **참조는 바뀌어있지 않기 때문**.<br/>

그럼 깊은 복사는 어떻게 해?<br/>

`spread operator`로는 **불가능**,<br/>
각각의 객체를 찾아가서 그 안에 property들 다 복사해오고, 그걸 가지고 새 배열로 만들어야한다.


