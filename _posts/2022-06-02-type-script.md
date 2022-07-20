---
published: true
title: "✨ Type Script"
permalink: /js/typeScript
tags:
  - [js]

navigation: true
toc: true
toc_sticky: true

date: 2022-06-02
last_modified_at: 2022-06-02
---
****
![]()

# 나는 전혀 타입하고 있지 않아

<a href='https://velog.io/@gomjellie/You-dont-know-type'>
타입스크립트 타입 레벨 프로그래밍</a>을 기반으로 작성되었습니다. <br/>

## 1. Type Script란?

Java Script + Type 문법 = "**JavaScript SuperSet**" <br/>

- Java Script는 Dynamic Typing이 가능하다.
```js
5 - '3'
// 2
```
원래는 숫자 - 숫자만 가능하지만 JS가 알아서 숫자로 변환해준다. <br/>
매우 편리하지만, 코드가 길어지만 `자유도`와 `유연성`은 단점으로 작용한다. <br/>

`Java Script`는 에러 메시지가 추상적인 반면, `Type Script`는 에러 메시지도 명확하다. <br/>


- 주의할 점
브라우저는 반드시 Java Script 파일만 읽을 수 있다. <br/>
TS를 JS로 변환을 해야하는데, 이 과정을 컴파일이라고 한다. <br/>
그래서 tsconfig.json 파일을 만들어서 컴파일 시 옵션 설정이 가능하다.

```ts
{   
  "compilerOptions" : {     
    "target": "es5",     
    "module": "commonjs",  
  } 
}
```

- object 타입 지정

```ts
let name:{ name?: string } = { name: '이름' }
```

- union 타입 지정

```ts
let name: string | number = 123;
```

- 타입을 변수에 담을 수 있다
**`type alias`**

```ts

type Name = number;
let name: Name = 123;

```

- 함수에 타입 지정 가능
  - 리턴 값이 어떤 값인지 미리 체크할 수 있다
```ts

function a (x:number):number {
  return x * 2
}

```

- array에 쓰는 **`tuple`** 타입

```ts
type Member = [number, boolean]
let john: Member = [2, true]
```

- object에 지정해야할 타입이 너무 많으면
  - **모든 object 속성**

```ts
type Member = {
  [key:string]: string,
}
let john: Member = { name: 'kim', age: 25 }
```

string으로 들어오는 모든 object 속성들이 <br/>

"글자로 된 모든 object 속성의 타입은 반드시 **string**" <br/>

- Class 타입 지정 가능

```ts
class User {
  name:string;
  constructor(name: string) {
    this.name = name;
  }
}


```

string으로 들어오는 모든 object 속성들이 <br/>

"글자로 된 모든 object 속성의 타입은 반드시 **string**" <br/>


# Type Script와 HTML

HTML 조작과 변경을 위해 나온 것이 JS. 따라서 TS도 HTML 조작과 변경이 가능하다.