---
title: "Immutability! 자바스크립트 ✨불변성✨"
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

## 단어의 사전적인 의미
- mutate : 변화
- mutable : 변화 가능한
- mutability
  - 정보의 **원본이** **`변경 가능`**하다 ✂️

- 그럼 `immutability`는?
  - 정보의 **원본이** **`변경 불가능`**하다 ✂️❌
  - 데이터의 `원본이 훼손되는 것을 막는 것`


## 정보처리의 가장 기본적인 단위

CRUD

- **C**reate 생성
- **R**ead 읽기
- **U**pdate 수정
- **D**elete 삭제

가장 중요한 두가지가 있다. 바로 **Create**와 **Read** !

**Create**하지 않으면 **Read**할 수 없고,<br/>
**Read**하지 않을 거라면 **Create**할 필요가 없다.

그렇기 때문에, 모든 정보는 그것이 존재하고 있다면<br/>
**`생성이라는 수단`**과, 그것을 **`읽기 위한 목적`**으로 이루어져있다.

=> 이것을 다른 말로 **origin**. 즉 <strong style="color:white;background-color:black">**원본**</strong>이라고 부른다.<br/>


그렇기 때문에 어떤 정보 시스템을 만났을 때 가장 먼저 해야할 것은 Create / Read 의 방법을 알아내는 것.
이것이 이 분야의 **핵심**
