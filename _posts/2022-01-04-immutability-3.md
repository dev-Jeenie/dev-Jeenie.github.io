---
title: "✨Immutability 불변성 ✂️❌ - (3) 변수 할당에 대한 불변함"
# title: "✨Immutability 불변성 ✂️❌ - (3) 변수 할당에 대한 불변함(1. 변수 할당방식의 비교)"
permalink: /cs/immutability3
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-04
last_modified_at: 2022-01-04
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

<img src="/assets/images/primitive-type.png" /><br/>

- 1) 변수에 Primitive 타입인 값을 할당
- 2) 그 값이 메모리 어딘가에 저장
- 3) Primitive 타입인 같은 값을 가진 다른 변수를 선언

**Q.** 이때에 다른 변수는 어디를 기리킬까?<br/>
=> **이미 있는 값**이기 때문에 변수 p2도 **`같은 위치를 가리킴`** <br/>

<strong style="color:white; background-color:black; font-size:18">
p1 === p2의 결과는 <strong style="color:red;">true</strong>
</strong>





## 2. Object 타입의 경우

<img src="/assets/images/object-type.png" /><br/>























<img src="/assets/images/primitive-object.png" /><br/>
