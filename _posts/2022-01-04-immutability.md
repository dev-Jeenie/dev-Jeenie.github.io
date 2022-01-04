---
title: "✨Immutability 불변성 ✂️❌ - (1) 불변성이란?"
permalink: /cs/immutability
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-01-04
last_modified_at: 2022-01-04
---

![]()

# Immer란 무엇인가?

먼저 짚고 넘어가야할 개념인 자바스크립트의 `**불변성**`

리액트에서 객체나 배열을 업데이트 해야 할 때에는 직접 수정해서는 안됨!
`불변성`을 지켜주면서 업데이트를 해야함.

> https://react.vlpt.us/basic/23-immer.html velopert님 게시글 참조

## 1. 단어의 사전적인 의미
- mutate : 변화
- mutable : 변화 가능한
- mutability
  - 정보의 **원본이** **`변경 가능`**하다 ✂️

- 그럼 `immutability`는?
  - 정보의 **원본이** **`변경 불가능`**하다 ✂️❌
  - <strong style="color:black;background-color:aliceblue">데이터의 `원본이 훼손되는 것을 막는 것`<strong>

## 2. 원본 훼손을 왜 막아야할까?
사실 컴퓨터는 수정 삭제의 불편함을 개선하기 위해서 출발함.<br/>
그런데 이것이 너무 자유롭다보니 사건 사고가 생김<br/>
=> immutability에 대한 요구⬆️⬆️

## 3. 정보처리의 가장 기본적인 단위

CRUD

- **C**reate 생성
- **R**ead 읽기
- **U**pdate 수정
- **D**elete 삭제

### 3-1. Create와 Read

가장 중요한 두가지, **Create**와 **Read** !<br/>

**Create**하지 않으면 **Read**할 수 없고,<br/>
**Read**하지 않을 거라면 **Create**할 필요가 없다.<br/>

그렇기 때문에, 모든 정보는 그것이 존재하고 있다면<br/>
**`생성이라는 수단`**과, 그것을 **`읽기 위한 목적`**으로 이루어져있다.<br/>

=> 이것을 다른 말로 **origin**. 즉 <strong style="color:black;background-color:aliceblue">**원본**</strong>이라고 부른다.<br/>


그렇기 때문에 어떤 정보 시스템을 만났을 때 가장 먼저 해야할 것은 Create / Read 의 방법을 알아내는 것.<br/>
이것이 이 분야의 **핵심** <br/>


### 3-2. Update와 Delete

그 후로 중요한 작업은 **Update**와 **Delete** <br/>
#### 3-2-1. 수정과 삭제가 안되는 정보 시스템이 있긴 한가?
- 📚 한번 인쇄되어서 배포까지 된 종이책 => 불가능
- 🏛 역사에서의 수정과 삭제 => 도덕적 지탄
- 💵 회계에서의 수정과 삭제 => 법적인 제제
- ⛓ 블록체인과 같은 최신 기술
  - 복제된 정보를 분산해서 보관함으로써 `분산된 네트워크 형성`.
  - 악의적으로 정보가 변경되는 것을 막기 위함.

이렇듯이, `수많은 정보가 불변`하거나, `불변을 추구`한다.<br/>

무질서한 수정 삭제로 원본이 변경되는 것을 막는 방법을 찾는다.

원본에 가해지는 변화를 막는 방법을 찾는다면
사고 방지 가능.

## 4. 그럼 가변성은 나쁜건가?
❌ 가변성은 디지털의 특권! 좋은 것.<br/>
단 어플리케이션에서 <strong style="color:black;background-color:aliceblue">움직일 필요가 없는 부분을<br/>
🧊냉동🧊 시켜둔다면</strong> <br/>

훨씬 안전하게 `변화`에 도전할 수 있다.

## 5. 결과적으로 추구하는 것
**불변성과 가변성**을 이상적으로 ➕`합성`해서
<strong style="color:black;background-color:aliceblue">견고하면서도 유연한 어플리케이션</strong>을 만들어내는 것!