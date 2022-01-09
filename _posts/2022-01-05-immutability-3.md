---
title: "✨Immutability 불변성 ✂️❌ - (3) 변수 할당에 대한 불변함"
# title: "✨Immutability 불변성 ✂️❌ - (3) 변수 할당에 대한 불변함(1. 변수 할당방식의 비교)"
permalink: /cs/immutability3
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
- name : 값의 이름
- `value` : 값 자체

그렇다면 `값`을 어떻게 불변하게 할 것인가?

# 변수 할당에 대한 불변함 - (1) 변수 할당 방식 비교
## 1. 값을 불변하게 유지하는 방법

자바스크립트에서 변수가 어떤 값을 가리킬 때, 어떤 값으로 가리키는지 구체적인 동작 방법을 알아야 불변성을 이해할 수 있다.

### 1-1. 자바스크립트의 데이터 타입

| **Primitive** | **Object** |
| -- | -- |
| number | Object |
| string | Array |
| Boolean | Function |
| Null | -- |
| undefined | -- |
| Symbol | -- |

**Primitive**
- 원시(원자)데이터 타입. 더이상 **쪼갤 수 없는** `최소한의 정보`들.

**Object**
- 서로 **연관된 정보를 `정리정돈`**하는 데에 사용하는 포괄적으로 객체라고 칭하는 것들.
  - **Object**
    - 당연히 `객체`
  - **Array**
    - 객체가 가지고 있는 기능 중, 순서대로 정리정돈하는 기능이 추가된 `객체`
  - **Function**
    - 함수 또한 값으로 사용될 수 있는 `객체`

자바스크립트에서 변수를 통해 어떤 값을 가리킬 때, <br/>
그 값이 `Primitive`인지 `Object`인지에 따라서 동작방법이 완전히 다름.


# 변수 할당에 대한 불변함 - (2) 초기값의 비교

## 1. Primitive 타입의 경우

<img src="/assets/images/primitive-type.jpeg" /><br/>

- 1) 변수에 Primitive 타입인 값을 할당
- 2) 그 값이 메모리 어딘가에 저장
- 3) Primitive 타입인 같은 값을 가진 다른 변수를 선언

**Q.** 이때에 다른 변수는 어디를 기리킬까?<br/>
=> **이미 있는 값**이기 때문에 변수 p2도 **`같은 위치를 가리킴`** <br/>

<strong style="color:white; background-color:black; font-size:18">
p1 === p2의 결과는 <strong style="color:red;">true</strong>
</strong><br/>

> ⭐️ **동등비교 연산자의 연산**에서 참이 나온다는 것은 `같은 값을 가리킨다`는 뜻.<br/>

1은 원시 데이터로 언제나 1이기 때문에, 값을 바꿀 수 없음.<br/>

=> **결론** : `Immutable(불변)하다`



## 2. Object 타입의 경우

<img src="/assets/images/object-type.jpeg" /><br/>

- 1) 변수에 Object 타입인 값을 할당
- 2) 그 값이 메모리 어딘가에 저장
- 3) Object 타입인 같은 값을 가진 다른 변수를 선언

**Q.** 이때에 다른 변수는 어디를 기리킬까?<br/>
=> **별도의 데이터를 새로 생성**. 변수 o2는 **`다른 위치를 가리킴`** <br/>

<strong style="color:white; background-color:black; font-size:18">
o1 === o2의 결과는 <strong style="color:red;">false</strong>
</strong><br/>

### 2-1. 객체는 왜?
객체 안에 여러 `property`가 있고,
이 `property`가 가리키는 값은 계속 바뀐다.<br/>
그래서 **바뀔 수 있는 가능성**이 있음!
=> 이것이 같은 값을 가지는 객체라고 해도 `별도로 생성`해서 `따로따로 보관`하는 이유.

⭐️`const로 선언했어도 마찬가지`!⭐️
선언한 객체의 그 **이름 자체는 바꿀 수 없지만**, 그 객체의 `property의 값`은 얼마든지 `바꿀 수 있음`.

=> **결론** : `mutable(가변)하다`

<img src="/assets/images/primitive-object.png" /><br/>


# 변수 할당에 대한 불변함 - (3) 객체의 가변성

## 1. 값 변경 시 동작 과정
### 1-1. Primitive Type인 값 변경
<img src="/assets/images/primitive-value-change.jpeg" /><br/>

- 1) p3을 생성하고 값을 p1으로 지정<br/>
=> 변수 p3과 p1은 **`같은 위치를 가리킴`**

<img src="/assets/images/primitive-value-change-2.jpeg" /><br/>

- 2) 이때 p3의 값을 2로 변경<br/>
현재 메모리에 없는 값. 메모리 어딘가에 2라는 값을 저장하고, p3는 그 값을 가리킨다.<br/>
=> 변수 p3과 p1은 **`다른 위치를 가리킴`**

**결론 :** <br/>
primitive 값을 가진 `변수의 값`을 또다른 primitive 값을 가진 `변수`로 지정하면?<br/>
=> 값이 **같을 땐 같은 값**을 가리키다가, **값이 달라지면 다른 값**을 가리킨다

### 1-2. Object Type인 값 변경
<img src="/assets/images/object-value-change.jpeg" /><br/>

- 1) o3을 생성하고 값을 o1으로 지정<br/>
=> 변수 o3과 o1은 **`같은 위치를 가리킴`**

<img src="/assets/images/object-value-change-2.jpeg" /><br/>

- 2) 이때 o3의 property name의 값을 변경<br/>
o3가 가리키고 있던 `값이 변경`, 그런데 이 값은 **o1도 참조하는 중**이었음.<br/>
그래서 o3가 바뀌니까, `같은 위치의 값을 참조하던` o1의 값도 **`변경`**!<br/>

=> 변수 p3의 property 값 변경으로 인해 p1의 값도 **`변경되어버림`**<br/>
의도한거라면 좋겠지만, 의도하지 않았다면 🚨 <strong style="color:black;background-color:aliceblue">심각한 버그</strong>가 발생 🚨 <br/>

> 🤦‍♀️ 의도하지 않은 사람: `원본 데이터 건들지않고` o3에 대해서만 수정하게 하고싶다....

**결론 :** <br/>
Object 값을 가진 `변수의 값`을 또다른 Object 값을 가진 `변수`로 지정하면?<br/>
=> **같은 값**을 가리키다가, 값을 변경하면 `그 위치를 참조하고 있던 다른 변수의 값도 변경`되는 문제가 발생.

## 2. 차이점

**차이점**

- **Object**
  - 생성시마다 `새로운 객체`를 만든다
  - property를 통해 **값을 바꿀 수 `있다`** => 여기서 <strong style="color:black;background-color:aliceblue">문제점</strong> 발생
- **Primitive**
  - 필요시까지 `새로 만들지 않는다`
  - **값을 바꿀 수 `없다`**

  그럼 이 문제점을 어떻게 해결할 수 있을까?


# 변수 할당에 대한 불변함 - (4) 객체의 복사

## 1. 객체를 불변하게 다루는 방법

**문제점**
<img src="/assets/images/object-copy-1.jpeg" /><br/>

- 어떻게하면 원본 데이터에 영향을 주지 않을까?
  - 객체 o1을 **불변하게** 만든다.
- 객체 o1을 불변하게 만들려면?
 - 복사한다

o2가 o1을 값으로 가진다면, **o1이 가지는 값을 `복사`**해서 o2가 가지면 된다

**해결방법**
<img src="/assets/images/object-copy-2.jpeg" /><br/>

- 1) **Object.assign**( {} , 복사할 원본 객체)

첫번째 인자인 객체와, 두번째 인자의 객체를 `병합`해서 **하나의 객체**로 만든 후 그 객체로 리턴함.

<img src="/assets/images/object-copy-3.jpeg" /><br/>
- 2) 이제 값을 변경해도 자기 자신만 변경되고, 원본은 변경되지 않음

=> 원본데이터인 o1의 `불변성`을 유지했고, 복제본 o2를 변경시키는 것을 통해 `가변성`을 달성함

<img src="/assets/images/object-assign.png" /><br/>

복사를 했으니 o1과 o2가 가리키는 위치는 `같지 않다.`
이때 겍체 o2의 property name의 값을 변경하면 <br/>
자기 자신만 변경되고, **원본의 데이터는 변경되지 않음**


# 변수 할당에 대한 불변함 - (4) 중첩된 객체의 복사

## 