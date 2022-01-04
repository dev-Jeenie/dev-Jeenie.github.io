---
title: "✨Immutability 불변성 ✂️❌ - (2) 이름에 대한 불변함"
permalink: /cs/immutability2
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-05
last_modified_at: 2022-01-05
---

![]()

# 불변함을 적용할 수 있는 대상
- `name` : 값의 이름
- value : 값 자체

그렇다면 `이름`을 어떻게 불변하게 할 것인가?

## 1. 이름을 불변하게 유지하는 방법
(부제 : 우리는 왜 `var`를 사용하지 않을까?)

### 1-1. var vs const

1. `var`로 작성했을 경우

```JS
var v = 1;
/* 코드 1억 줄 */
/* 코드 1억 줄 */
/* 코드 1억 줄 */
v = 2;
console.log('v :', v);

```

변수 v를 만든 사람은 v의 값은 1일 것이라고 예상했지만,
누군가가 그 사실을 모르고! **v의 값을 변경**해버림.<br/>

=> **결과** : 에러조차 발생하지 않는 🚨 <strong style="color:black;background-color:aliceblue">심각한 버그</strong>가 발생 🚨 <br/>

> 🤦‍♀️ v를 만든 사람: 그 누구도 내 `변수를 바꾸지 못하게` 하고싶다...

2. `const`로 작성했을 경우

```JS
const c = 1;
/* 코드 1억 줄 */
/* 코드 1억 줄 */
/* 코드 1억 줄 */
c = 2;
console.log('v :', v);
// 에러 발생!

```

<img src="/assets/images/const-var.png" /><br/>

상수 변수에 값을 대입하려고 하면 발생하는 에러. <br/>

## 2. 변수의 속성

변수는 원래 그 이름이 가리키는 값이 바뀔 수 있다. <br/>

하지만 `상수 변수`는 한번 값을 가리키게 되면,<br/>
그 이후로는 <strong style="color:black;background-color:aliceblue">상수 변수가 가리키는 값을 변경하는 것이 금지됨</strong><br/>

상수 변수가 가리키는 값을 변경을 시도하면 **`바로`! 🚨에러가 발생**하며 프로그램이 종료됨.<br/>
=> 👍 오히려 좋아! 왜?
- 부주의하게 값을 바꿀 수 없음
- 그런 시도를 했을 때 즉시 문제 파악 가능

소프트웨어가 거대하고 복잡할 수록 (eg.코드 1억줄, 20년 서비스, 오픈소스...) 엄청난 도움이 된다.