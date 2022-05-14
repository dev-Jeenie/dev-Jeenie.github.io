---
published: true
title: "React란 무엇인가?"
permalink: /cs/defaultKnowledge7
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2022-05-06
last_modified_at: 2022-05-06
---
****
![]()

> 들어가기 전 <br/>

https://joshua1988.github.io/web-development/interview/frontend-questions/
<br/>
https://github.com/JaeYeopHan/Interview_Question_for_Beginner
<br/>
https://jbee.io/essay/for_junior_frontend_developer/
<br/>

위의 글들을 참조하여 배경지식을 찬찬히 쌓아보자.<br/>

<!-- 
# React
## useRef

React에서 useRef를 사용하는 경우<br/>

useRef는 **`리렌더링하지 않는다`**. 컴포넌트의 **속성만 조회 & 수정**한다.<br/>

### Ref를 사용해야 할 때

< Ref의 바람직한 사용 사례 > <br/>

- 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때
- 애니메이션을 직접적으로 실행시킬 때
- 서드 파티 DOM 라이브러리를 React와 같이 사용할 때

> **선언적으로 해결될 수 있는 문제**에서는 ref 사용을 지양해야한다





-React 관련 이론들(useEffect, useSate, props, useMemo, useCallback, useRef, Context, useReduce 쓰는 이유 및 정의 및 이론 설명) -->

# React란?

자바스크립트 라이브러리의 하나로서 사용자 인터페이스를 만들기 위해 사용되는 웹 프레임워크. <br/>

facebook에서 제공해주는 프론트엔드 라이브러리<br/>

싱글 페이지 어플리케이션 개발시 토대로 사용한다.<br/>

## 1. 특징

- 컴포넌트의 사용


React는 컴포넌트 기반이기 때문에 스스로 상태를 관리하는 **`캡슐화된 컴포넌트`**를 만들고
이를 조합하여 더 복잡한 UI를 만들 수 있다. 컴포넌트를 잘 활용하면 코드의 재사용성과 유지보수에서 이점을 가진다.

관리가 용이하다.


React는 UI(View)를 여러 컴포넌트(component)를 쪼개서 만듭니다.
한 페이지 내에서도 여러 각 부분을 독립된 컴포넌트로 만들고, 이 컴포넌트를 조립해 화면을 구성합니다.


컴포넌트 단위로 쪼개져 있어 전체 코드를 파악하기 쉽습니다

### 1-1. React에서의 불변성

React의 화면 업데이트와 관련이 있다. <br/>
React는 상태를 감시하고 있다가 변경된 상태에 따라 컴포넌트가 리렌더링 되는데,


- 불변성이란?
(상태를 변경하는데, 상태를 변경하지 않는 것) <br/>
어떠한 값을 직접적으로 변경하지 않고 새로운 값을 만들어내는 것. <br/>

원시타입이 아닌 객체타입의 데이터를 어떠한 변수에 할당하고 그 변수를 다른 변수에 할당하면,<br/>
값 복사가 이루어지는 것이 아니라 두개의 변수가 같은 참조값을 가진다<br/>
그래서 사본을 수정하면 원본도 함께 수정된다.<br/>

- React의 기본 속성
  - react는 기본적으로 부모 컴포넌트가 리 렌더링을 하면 자식 컴포넌트도 리 렌더링을 한다. <br/>
  - 즉, 얕은 비교를 통해 새로운 값인지 아닌지를 판단한 후에 새로운 값일 경우 리 렌더링을 한다 <br/>

> 얕은 비교란? <br/>
객체, 배열, 함수와 같은 참조 타입들을 실제 내부 값까지 비교하지 않고 동일 참조인지(동일한 메모리 값을 사용하는지)를 비교하는 것 <br/>

컴포넌트를 리렌더링해야하는 상황 예시
- 1) 배열인 state를 state.push(1)로 직접 접근해서 요소를 추가한다
- 2) push는 전혀 다른 값이 아님. state라는 값은 ***새로운 참조값이 아니기 떄문에*** 같은 값이라고 인식, 리렌더링하지 않는다


- **state를 바꾸고 DOM을 다시 만들기 위한 올비른 방법**
새로운 객체나 배열을 만들어 새로운 참조값을 만들고, react에게 이 값은 이전과 다른 참조값임을 알린다

> 새로운 상태변경 작업을 해야할 때, 원본을 바꿔버리면 안되니 새로운 배열로 작업해야하는 이유가 여기에 있었다! <br/>
원본 데이터를 수정해버리면 새로운 위치가 아니니까 react는 감지하지 못함.<br/>


- **React가 화면을 업데이트하는 과정**
  - 1) setState호출(혹은 부모로부터 props를 전달받는다)
  - 2) `shouldComponentUpdate`를 실행했는데 false를 리턴하면 멈추고, true를 리턴하면 다음 단계로 이동
  - 3) **가상 DOM과 실제 DOM을 비교**해서 변경사항이 있으면 화면을 다시 그린다

- 여기서 `shouldComponentUpdate`는?
  - 각각의 컴포넌트들은 `shouldComponentUpdate`라는 메소드를 가지고 있고,
  - 이것은 state가 변경되거나 부모 컴포넌트로부터 새로운 props를 전달받을 대 실행된다.
  - React는 이 메소드의 반환 값에 따라서 re-render를 할지에 대한 여부를 결정한다
  - 기본적으로 `shouldComponentUpdate` 메소드는 true를 반환한다.
  - 하지만 React개발자가 re-render를 원하지 않을 경우에, 이 return value를 false로 오버라이드 할 수 있다

- 특정 컴포넌트가 ***업데이트를 할 필요가 없다***라는 것을 어떻게 판단하는가?
컴포넌트가 가지고 있는 데이터(props, state)의 이전 이후 값을 완전히 비교하는 것

=> 데이터의 불변성이 지켜지지 않으면, 객체 내부의 값이 달라져도 React는 감지하지 못한다 <br/>


- Spread operator를 이용한 복사를 이용하면?

전개 연산자를 사용하여 객체나 배열 내부의 값을 복사할 땐 얕은 복사한다.<br/>
즉 **내부의 값이 완전히 새로 복사되는 것이 아니라, 가장 바깥쪽에 있는 값만 복사**된다.<br/>

=> 따라서 내부의 값이 객체라면, 내부의 값 또한 따로 복사를 해야한다!<br/>

내부 요소가 바뀌었을 때에도 state를 바꾸고, DOM을 다시 그리기 위해서는,<br/>
새로운 객체나 배열을 만들어 **새로운 참조값**을 만들고<br/>
React에게 **이 값은 이전과 다른 참조값**임을 알려야한다!<br/>


- 상태변화를 줄 때 deep copy를 해야하는 이유
React 컴포넌트에서는 state 또는 상위 컴포넌트에서 전달받은 props의 값이 변경될 때 리렌더링을 한다 <br/>

객체나 배열같은 참조타입의 자료형은, <br/>
deep copy를 하지 않으면 내부의 값이 변경되었더라도 레퍼런스가 참조하는 곳이 동일하기 때문에 똑같은 값으로 인식한다.<br/>
그래서 리 렌더링을 하지 않는다. <br/>
그래서 **기존 값을 복사해서 새로운 객체나 배열로 만들어줘야한다**. <br/>
그래야 레퍼런스 주소가 바뀐 것을 인지하고 리 렌더링을 한다 <br/>


- 새로운 값을 반환하는(deep copy가 가능한) 배열 메소드
  - concat()
  - map()
  - filter()
  - slice()
  - spread 문법(...)


상태값을 변화시켜 리랜더링을 의도할 때에는 push(), pop(), shift(), unshift() 등의 가변성 있는 함수 사용하면 안됨 <br/>
사용하더라도 해당 배열을 spread나 slice등으로 복제한 뒤에 사용해야한다. <br/>

하지만 이러한 방법도 결국엔 얕은 복사에 해당한다. <br/>
1계층, 2계층 더 들어갈 수록 복사를 하려면 하나하나 깊이 해주어야 한다. 사실상 불가능에 가깝다.<br/>
이를 도와주기 위해 `immer`라는 라이브러리가 있다.<br/>



### 1-1-1. 불변성을 지키면서 state 바꾸기 <br/>

배열에 추가
```jsx
setUsers(state.array.concat(user));
```


배열에서 삭제
```jsx
const onRemove = id => {
  // user.id 가 id 인 것을 제거
  setUsers(users.filter(user => user.id !== id));
};
```

배열에서 수정
```jsx
const onToggle = id => {
  setUsers(
    users.map(user =>
      user.id === id ? { ...user, active: !user.active } : user
    )
  );
};
```

객체에서 추가
```jsx
setState(state => {...state, key: value})
```

객체에서 제거
```jsx
setState(state => {..._.omit(state, 'deleteKey')})
```


객체에서 수정
```jsx
setState(state => {...state, key: newValue})
```


- 위처럼 배열 혹은 객체를 바꾸면 불변성을 유지하면서 변경이 가능하다. <br/>
그러나 immer.js를 이용하면 일반 객체 또는 배열을 다루듯 사용하면 immer가 불변성을 유지시켜줌<br/>


```jsx
import produce from "immer";

const baseState = [
  {
    todo: "Learn typescript",
    done: true
  },
  {
    todo: "Try immer",
    done: false
  }
];

const nextState = produce(baseState, draftState => {
  draftState.push({ todo: "Tweet about it" });
  draftState[1].done = true;
});
```
immer에서 사용할 함수는 오직 produce만 알면 된다. <br/>
2가지의 파람을 가져오고 첫번째는 **`수정하고 싶은 객체/배열`**, 두번째는 **`첫번째 파라미터에 할당된 객체/배열을 바꾸는 함수`**. <br/>



- Redux에서의 immer

  - immer 쓰기 전 reduce 코드

```jsx
const initialState = [{ name: "nkh", address: { city: "seoul" } }];

export default function auth(state = initialState, action) {
  switch (action.type) {
    case SET_INFO:
      return {
        ...state,
        name: "kkkk",
        address: {
          ...state.address,
          city: "kkkk"
        }
      };
    default:
      return state;
  }
}
```

  - immer 쓴 reduce 코드

```jsx
const initialState = [{ name: "nkh", address: { city: "seoul" } }];

export default function auth(state = initialState, action) {
  produce(state, draft => {
    switch (action.type) {
      case SET_INFO:
        draft[0].name = action.data.name;
        draft[0].address.city = action.data.city;
        break;
      case ADD_INFO:
        draft.push({ name: "hhh", address: { city: "zzz" } });
      default:
        return draft;
    }
  });
}
```





### 1-2. JSX 문법 사용

**JSX(JavaScript XML)란?**

JavaScript XML로 JavaScript에 XML을 추가해 확장한 문법.

리액트 개발 시에 사용되므로 공식적인 자바스크립트 문법은 아니다

JSX로 작성된 문법을 babel이 일반적인 자바스크립트 형태의 코드로 변환시킨다

JSX 문법 사용으로 인해 가독성과 편의성을 높일 수 있다

- JSX문법을 사용하지 않았을 때


```js
render() {
    return (
      React.createElement(View, {style: styles.container},
        React.createElement(Text, {style: styles.welcome}, 'Welcome to React Native!'),
        React.createElement(Text, {style: styles.instructions}, 'To get started, edit App.js'),
        React.createElement(Text, {style: styles.instructions}, instructions)
      )
    );
  }
```

위처럼 **`React.createElement()`** 로 직접 DOM 요소를 조작하듯이 컴포넌트를 생성해야한다. <br/>


- 사용했을 때

```js
render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>Welcome to React Native!</Text>
        <Text style={styles.instructions}>To get started, edit App.js</Text>
        <Text style={styles.instructions}>{instructions}</Text>
      </View>
    );
  }
```


JSX 내부에서도 자바스크립트 표현식을 넣을 수 있다 <br/>
JSX 내부에서 코드를 {}로 감싸면 된다


## React의 생명주기 (Life Cycle)

컴포넌트의 생명주기<br/>

React는 컴포넌트 기반의 View 를 중심으로 한 라이브러리<br/>

그래서 각 컴포넌트에는 **`컴포넌트의 생명주기`**가 있다<br/>

컴포넌트의 수명은<br/>

**렌더링되기 전인 준비 과정 ~ 페이지에서 사라질 때** 끝이 난다<br/>


세가지 유형이 있다.
- `Mount`(생성될 때)
  - DOM이 생성되고 웹 브라우저 상에 나타나는 것
- `Update`(업데이트할 때)
  - props가 바뀔 때
  - state가 바뀔 때
  - 부모 컴포넌트가 리렌더링 될 때
  - this.forceUpdate로 강제로 렌더링을 트리거할 때
- `Unmount` (제거할 때)
  - DOM이 제거되는 것


### Class, Hooks 각각에서의 생명주기

컴포넌트 라이프 사이클 메소드는 클래스형 컴포넌트에서느 직접 사용이 가능하지만 <br/>
함수형 컴포넌트에서 Hooks 기능을 이용해서 사용할 수 있다


### 1-1. 마운트 과정의 라이프사이클 메소드

1. constructor

컴포넌트를 만들 때 처음으로 실행

```js
// class
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
}

// Hooks
const Example = () => {
    const [count,setCount] = useState(0);
}
```

클래스 문법에서는 초기 state를 정할 때 constructor를 사용해야한다.<br/>
하지만 훅에서는 useState로 간편하게 초기상태를 지정할 수 있다


2. render

컴포넌트를 랜더링 할 때 필요한 필수적인 메서드
함수형 컴포넌트에서는 render를 쓰지않고 컴포넌트를 랜더링할 수 있다


```js
// Class
class Example extends React.Component {
  render() {
    return <div>컴포넌트</div>
  }
}

// Hooks
const example = () => {
  return <div>컴포넌트</div>
}
```


3. componentDidMount




### 1-2. 업데이트 과정의 라이프사이클 메소드

컴포넌트에 변경사항이 발생될 때 업데이트를 실시

- props의 변경
- state의 변경
- 부모 컴포넌트의 리렌더링
- this.forceUpdate()를 통한 강제 렌더링


- getDerivedStateFromProps
- shouldComponentUpdate
- render
- getSnapshotBeforeUpdate
- componentDidUpdate



### 1-3. 언마운트 과정의 라이프 사이클 메소드

언마운트는 DOM에서 컴포넌트를 제거하는 과정입니다. <br/>
당연하지만 삭제과정은 컴포넌트를 삭제하는 것이라 **삭제하기 직전만이 컴포넌트를 제어**할 수 있습니다.<br/>


- componentWillUnmount


### 1-4. 라이프사이클 메소드 사용

```jsx
import React from 'react';

class ComponentLifeCycle extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            destroyed: false,
        };

        console.log("constructor() 메소드 호출");
    }

    static getDerivedStateFromProps() {
        console.log("getDerivedStateFromProps() 메소드 호출");

        return {};
    }

    componentDidMount() {
        console.log("componentDidMount() 메소드 호출");

        this.setState({updated: true});
    }

    shouldComponentUpdate() {
        console.log("shouldComponentUpdate() 메소드 호출");

        return true;
    }

    getSnapshotBeforeUpdate() {
        console.log("getSnapshotBeforeUpdate() 메소드 호출");

        return {};
    }

    componentDidUpdate() {
        console.log("componentDidUpdate() 메소드 호출");
    }

    componentWillUnmount() {
        console.log("componentWillUnmount() 메소드 호출")
    }

    render() {
        console.log("render() 메소드 호출");

        return null;
    }
}

export default ComponentLifeCycle;
```
결과 <br/>

- constructor() 메소드 호출
- getDerivedStateFromProps() 메소드 호출
- render() 메소드 호출
- componentDidMount() 메소드 호출
- getDerivedStateFromProps() 메소드 호출
- shouldComponentUpdate() 메소드 호출
- render() 메소드 호출
- getSnapshotBeforeUpdate() 메소드 호출
- componentDidUpdate() 메소드 호출

삭제까지 한다면 제일 마지막에 componentWillUnMount가 호출됨.

<!-- 


### 1-1. 정의




### 1-2. 쓰는 이유

### 1-3. 이론
 -->

# 2.  React Hooks

- 기본 Hook
  - `useState`
  - `useEffect`
  - `useContext`

- 추가 Hooks
  - `useReducer`
  - `useCallback`
  - `useMemo`
  - `useRef`
  - `useImperativeHandle`
  - `useLayoutEffect`
  - `useDebugValue`


## 2-1. useState

리액트 컴포넌트에서 동적인 값을 상태(state)라고 한다. <br/>

그런데 그 상태가 동적으로 바뀔 경우에는 상태를 관리하는 것이 필요하다.<br/>

React Hooks가 나오기 전에는 class 기반의 class 컴포넌트로 작성을 해야했는데,
간단한 상태값도 constructor를 만들어서 고나리해야했으니 복잡해 유지보수가 힘들었다.<br/>

React Hooks가 도입되면서 함수형 컴포넌트에서도 상태를 관리할 수 있게 되었다.<br/>
그 Hooks 중 useState() 함수가 있는데, 이것으로 상태를 관리할 수 있다.<br/>


### 2-1-1. setState의 비동기적 특성

setState는 비동기적으로 동작한다


```jsx
import React, {useState} from 'react';

const Counter2 = () => {
    const [count, setCount] = useState(0);

    const onClick = () => {
        setCount(count+1);
        console.log('click');

        setCount(count+1);
        console.log('click');
    }

    return (
        <div>
            <h1>{count}</h1>
            <button onClick={onClick}>+</button>
        </div>
    );
}

export default Counter2;
```
setCount를 두번 했으니 누를 때마다 2씩 증가할 것 같지만, <br/>
버튼을 누르면 **count는 1만 증가한다**. 로그는 두 번 찍혔는데 왜일까?<br/>

```jsx
    const onClick = () => {
        setCount(count+1);
        console.log('click');

        setCount(count+0);
        console.log('click');
    }
```
이벤트를 이렇게 수정해도 마찬가지로 로그만 두번 찍히고 count는 증가하지 않는다! <br/>


왜? <br/>

setState가 비동기적으로 동작하기 때문에. <br/>
리액트가 효율적으로 렌더링하기 위해 여러 개의 상태 값 변경 요청을 일괄 처리 처리하기 때문이다.(성능이슈)<br/>

setState는 변경된 사항을 기억하지 않기 때문에 마지막 업데이트만 적용되어 렌더링에 쓰이게 된다.

count에 1을 더했다가 다시 0을 더하는 이 이상한 코드를, **상태 변경 시점에 각자 랜더링을 한다면** 굉장히 비효율적일 것. <br/>
그렇기 때문에 setState는 **모든 주문(명령 코드)를 받은 후**에 가장 **`최신의 결과를 렌더링`**한다. <br/>



공식문서에서는 이러한 특성을 아래와 같이 간단하게 설명을 하고 있다.<br/>

> 다음 리렌더링 시에 useState를 통해 반환받은 첫 번째 값은 항상 갱신된 최신 state가 됩니다<br/>


### 2-1-2. 그럼 setState를 동기적으로 동작하게 하려면? <br/>

**`함수형 업데이트`**를 해야한다. <br/>

함수형 업데이트란? <br/>
어떠한 값을 바로 주는 것이 아니라 **함수를 통해서 전달**하는 방식

```jsx
//이전 코드
    const onClick = () => {
        setCount(count+1);
        console.log('click');

        setCount(count+1);
        console.log('click');
    }
    
//함수형 업데이트 코드
    const onClick = () => {
        setCount(count => count+1);
        console.log('click');

        setCount(count => count+1);
        console.log('click');
    }
```

이렇게 함수형 업데이트를 시키면, 1이 증가한 것을 렌더링하고 바로 1을 증가한 것을 한 번 더 렌더링한다. <br/>

이렇게 기존 값을 업데이트하는 함수를 넣어 값을 업데이트할 수 있다. <br/>





## 2. useEffect

리액트 컴포넌트가 렌더링될 때마다 특정 작업(side effect)를 실행할 수 있는 React Hook. <br/>
여기서 Side effect는 component가 렌더링 된 이후에 비동기로 처리되어야 하는 부수적인 효과들을 뜻합니다. 이러한 기능으로 인해 함수형 컴포넌트에서도 클래스형 컴포넌트에서 사용했던 생명주기 메서드를 사용할 수 있게 되었습니다.


컴포넌트가 마운트, 언마운트, 업데이트 되었을 때 할 작업을 설정할 수 있는 Hook.

> React의 class 생명주기 메서드에 친숙하다면, useEffect Hook을 componentDidMount와 componentDidUpdate, componentWillUnmount가 합쳐진 것으로 생각해도 좋습니다.<br/>

출처 : <a href="https://ko.reactjs.org/docs/hooks-effect.html">리액트 공식문서</a>


의존성 배열을 비운채로 두면 componentDidMount와 동일하게 동작한다.<br/>
컴포넌트가 처음 나타날 때에만 useEffect에 등록된 함수가 호출된다.<br/>


특정한 값을 의존하게 시키면 컴포넌트가 mount 될 때, 지정한 값이 업데이트될 때 useEffect를 실행합니다.<br/>




간단하게 말해 라이프사이클을 대체하는 Hook.




## 3. useContext

필요한 props를 글로벌하게 사용할 수 있게 도와주는 메소드 <br/>

- 왜 props를 글로벌하게 사용해야할까?

부모 => 자식으로 바로 전달하는 props이라면 그냥 props를 넘겨주면 되겠지만,<br/>
그 자식의 자식의 자식으로 넘겨받아야 한다면(하위 컴포넌트가 수십 개라면) 수정해야할 일이 생겼을 때 매우 번거롭고 힘들어진다.<br/>

하위 컴포넌트가 수십개라면, 중간 단계의 컴포넌트는 props를 넘겨주고 또 넘겨주는 중간다리의 역할을 해야한다.<br/>
(이게 바로 prop drilling) <br/>


하지만 Context를 사용하면 전역적으로 데이터를 공유하기 때문에, 중간 다리 역할만 하는 컴포넌트들을 건너뛰고<br/>
데이터가 **필요한 컴포넌트에서 바로 사용이 가능**하게 된다. <br/>

리액트 Hook인 useContext는 이러한 Context를 좀 더 편하게 사용할 수 있게 해주는 역할
어디서나 이 특정 값을 사용하고 변경할 수 있도록 사용하는 것이 **`useContext`**<br/>


### Context API 사용법!

- 1) createContext() 함수 사용해서 context 만들기
- 2) 최상위 컴포넌트에서 Provider로 감싸기
- 3) 하위 컴포넌트에서 context API 설정
  - useContext hook을 불러오기
  - 설정한 context를 import하기



### 3-1. 주요 개념

- `createContext(initialValue)`
  - context 객체 생성
  - createContext 함수 호출 시 ***Provider***와 ***Consumer*** 컴포넌트 반환
  - initialValue는 Provider를 사용하지 않았을 때 적용될 초기값을 의미

- `Context.Provider`
  - 생성한 context를 하위 컴포넌트에 전달하는 역할<br/>
  - 해당 context의 데이터가 필요한 컴포넌트를 감싸야 한다

- `Context.Consumer`
  - (사용 시) const data = **`useContext(Context)`**
  - context의 변화를 감시하는 컴포넌트
  - 설정한 상태를 불러올 때 사용





## 3. useMemo & useCallback


## 3-0. 미리 알아야하는 Memoization

기존에 수행한 연산의 **결과값을 어딘가에 저장해두고**, ***`동일한 입력`***이 들어오면 **`재활용`**하는 프로그래밍 기법을 말한다. <br/>

따라서 이 memoization을 적절히 활용하면 중복 연산을 피할 수 있기 때문에, <br/>
메모리를 조금 더 쓰더라도 어플리케이션의 성능을 ***`최적화`***시킬 수 있다. <br/>

### 3-1. React의 리렌더링

React가 리렌더링을 하는 조건은 3가지이다.

- 자신의 state가 변경
- 부모 컴포넌트로부터 전달받은 props가 변경될 때
- 부모 컴포넌트가 리렌더링될 때



리렌더링이 발생되면 해당 컴포넌트의 모든 객체들은 다시 생성된다.(함수도 객체) <br/>
javascript에서 **객체는 `참조타입`**으로<br/>
완전히 동일한 값을 가지고 있더라도 **참조하는 주소가 다르면 서로 다른 객체로 취급**된다.<br/>


컴포넌트가 리랜더링 되면 새로운 함수(객체)를 생성한다<br/>
객체 = 참조형 데이터<br/>
동일한 데이터가 아니라는 판단 == 변경되었다고 판단해 React.memo로도 계속 리랜더링을 하는 것.<br/>

상황에 따라 스타일을 변경하려고 내부 컴포넌트의 props로 style을 넘겨주면,<br/>
해당 style은 객체이고,<br/>
객체는 참조형 데이터라 자바스크립트는 동일하지 않다고 판단을 하고,<br/>
그래서 계속 불필요한 랜더링을 한다.<br/>

이것을 해결하기 위해서는?<br/>

=> useCallback 또는 useMemo를 사용해 메모이제이션을 해야함.<br/>


useCallback과 useMemo는 메모이제이션 된 값을 반환한다. <br/>
차이점은 **`useCallback`은 `함수`를 메모이제이션**하고, **`useMemo`는 `값`을 메모이제이션**한다.<br/>



### 3-2. useCallback()

React에 함수를 저장해서 매 실행마다 재생성하지 않도록 한다. <br/>
메모리 내에 동일한 위치 중 하나에 저장되므로 동일한 함수(객체)인지 비교가 가능하다. <br/>


- 예시

```js
const add = () => x + y;
```
어떤 컴포넌트 안에 함수가 선언되어 있다면, 이 함수는 해당 컴포넌트가 랜더링될 때마다 **새로운 함수가 생성된다**.


```js
const add = useCallback(() => x + y);
```

하지만 **useCallback()**을 사용하면, 해당 컴포넌트가 랜더링 되더라도<br/>
그 함수가 의존하는 값이 바뀌지 않는 한 **`기존의 함수`를 계속 반환**한다.<br/>

즉 위의 예제에서 x와 y의 **값이 바뀐다면** ***`새로운 함수가 생성`***되어서 변수 add에 할당되고,<br/>
x와 y의 **값이 동일하다면** 다음 랜더링 때에 이 함수를 ***`재사용`***한다.<br/>



### 3-3. useMemo()

useCallback과 동일한 방식으로 사용하면 된다

Button이 공통컴포넌트이고 상황에 따라 style을 커스텀 할 수 있게 props로 style을 넘겨준다.

```jsx
function App() {
  ...
  return (
      <div className="App">
        <div className="num" onClick={()=>{setNumber(number+1)}}>{number}</div> 
        <Button onClick={onClick} style={{backgroundColor: 'darkseagreen'}}/>
      </div>
    );
    ...
}

```

Button에 인라인으로 객체를 넣으면,리랜더링될 때마다 새로운 객체 {backgroundColor: 'darkseagreen'}가 생성된다. <br/>
따라서 Button은 계속 리랜더링 된다


```jsx
function App() {
  ...
	const buttonStyle = useMemo(() => ({backgroundColor: 'darkseagreen'}), []);

  return (
    <div className="App">
      <div className="num" onClick={()=>{setNumber(number+1)}}>{number}</div> 
      <Button onClick={onClick} style={buttonStyle}/>
    </div>
  );
  ...
  
 }
 ```

이렇게 useMemo를 사용해서 객체를 메모이제이션 해주면 style prop에 대한 ***`동일한 참조를 제공`***한다.<br/>
따라서 Button 컴포넌트는 랜더링되지 않는다.<br/>



## 5. useRef

useRef는 리랜더링하지 않는다. 컴포넌트의 속성만 조회하고 수정한다.

### 5-1. 사용예시

<!-- - 컴포넌트에 focus를 위치시킬 필요가 있는 경우
- 속성 값을 초기화할 필요가 있는 경우
- useRef로 컴포넌트 안의 변수 관리하기 -->

- 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때
- 애니메이션을 직접적으로 실행시킬 때
- 서드 파티 DOM 라이브러리를 React와 같이 사용할 때

단 선언적으로 해결할 수 있는 문제에서는 ref사용을 지양한다. <br/>
예를 들어, 컴포넌트에서 open()과 close() 메서드를 두는 대신, isOpen이라는 prop을 주는 것이 좋다.<br/>


## 6. useReducer

상태관리를 할 때, Context API와 useReducer를 함께 쓰는 경우가 많다. <br/>

React에서 컴포넌트의 상태 관리를 위해 가장 많이 쓰이는 hook은 setState() 함수이다. <br/>

하지만 좀 더 복잡한 로직과 상태 관리가 필요한 컴포넌트에서는 **`setReducer()`** hook 함수를 사용할 수 있다.<br/>


useReducer는 일반적으로 2개의 argument(reducer함수, initialState(초기값))를 갖는다.















## 8. props

props란?

React가 컴포넌트로 작성한 엘리먼트를 발견하면
JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달한다.
이 객체를 props(properties)라고 한다.

=> 즉, **부모 컴포넌트에서 *자식 컴포넌트로 전달해주는 객체***!


### 8-1. props의 특성

- props는 읽기 전용

함수 컴포넌트든, 클래스 컴포넌트이든 컴포넌트 자체의 props를 수정해서는 안된다! <br/>
모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 한다.

> 순수함수란? <br/>
부수효과를 발생시키지 않고 입출력이 순수한 함수 <br/>
부수효과가 없는 함수. 어떤 함수에 동일한 인자를 주었을 때 `항상 같은 값을 리턴하는` 함수 및 `외부 상태를 변경하지 않는` 함수 <br/>

(부수효과는 사이드이펙트, 곧 원본을 변경되어버리는 것을 뜻함)

### 8-2. props와 state의 차이

props와 state 모두 일반 javaScript 객체이다.<br/>
두 객체 모두 랜더링 결과물에 영향을 주는 정보를 가지고 있다.<br/>

둘 다 JS 객체이다
props와 state 모두 변경시 render를 trigger한다

중요한 차이점은 **관리되는 위치** <br/>


| -- | -- | -- |
| -- | props | state |
| 상위 구성요소에서 초기 값을 가져올 수 있다 | O | O |
| 상위 컴포넌트로 변경할 수 있다 | O | X |
| 컴포넌트 내에서 기본값을 설정할 수 있다 | O | O |
| 컴포넌트 내부에서 변경할 수 있다 | X | O |
| 자식 컴포넌트의 초기값을 설정할 수 있다 | O | O |
| 자식 구성 요소에서 변경할 수 있다 | O | X |

> 구성요소가 동일한 props 및 state 조합에 대해 다른 출력을 하는 경우 잘못된 작업을 수행하고 있다는 뜻




## 9. React 에서의 상태관리
- 상태관리 라이브러리 이론 및 정의(Redux 쓰는 이유, Redux의 사이클 원리 및 이해 설명)

Redux란?

리액트의 상태관리는
Context API
Redux
등이 있으며, Context API 보다 Redux를 사용하는 이유는
대규모 개발이나 유지보수성을 높이기 위해서이다.

리액트 최근 버전에서는 Context API가 개선되어서 사용하기가 매우 좋아졌다.

react-redux에서는 규칙이 있는데
단일 스토어여야할 것
읽기 전용 상태일것( 기존 객체 건드리지 않고 새로운 객체 생성해서 사용할 것 )
리듀서는 순수함수여야할 것( 파라미터 외의 값에 의존하지 않음 )

만드는 순서

액션 타입을 정하고
액션 생성 함수를 만들고
이 액션들을 사용하는 리듀서 함수를 만들고
스토어를 만들어 provider로 스토어를 props로 전달해준다.


<!-- 

## 10. React에서의 불변성을 지켜야하는 이유

- 불변성이란?

어떠한 값을 직접적으로 변경하지 않고 새로운 값을 만들어내는 것. <br/>

원시타입이 아닌 객체타입의 데이터를 어떠한 변수에 할당하고 그 변수를 다른 변수에 할당하면,<br/>
값 복사가 이루어지는 것이 아니라 두개의 변수가 같은 참조값을 가진다<br/>
그래서 사본을 수정하면 원본도 함께 수정된다.<br/>

- **React가 화면을 업데이트하는 과정**
  - 1) setState호출(혹은 부모로부터 props를 전달받는다)
  - 2) `shouldComponentUpdate`를 실행했는데 false를 리턴하면 멈추고, true를 리턴하면 다음 단계로 이동
  - 3) **가상 DOM과 실제 DOM을 비교**해서 변경사항이 있으면 화면을 다시 그린다

- 여기서 `shouldComponentUpdate`는?
  - 각각의 컴포넌트들은 `shouldComponentUpdate`라는 메소드를 가지고 있고,
  - 이것은 state가 변경되거나 부모 컴포넌트로부터 새로운 props를 전달받을 대 실행된다.
  - React는 이 메소드의 반환 값에 따라서 re-render를 할지에 대한 여부를 결정한다
  - 기본적으로 `shouldComponentUpdate` 메소드는 true를 반환한다.
  - 하지만 React개발자가 re-render를 원하지 않을 경우에, 이 return value를 false로 오버라이드 할 수 있다

- 특정 컴포넌트가 ***업데이트를 할 필요가 없다***라는 것을 어떻게 판단하는가?
컴포넌트가 가지고 있는 데이터(props, state)의 이전 이후 값을 완전히 비교하는 것

=> 데이터의 불변성이 지켜지지 않으면, 객체 내부의 값이 달라져도 React는 감지하지 못한다


### 10-1. Spread operator를 이용한 복사

전개 연산자를 사용하여 객체나 배열 내부의 값을 복사할 땐 얕은 복사한다.<br/>
즉 **내부의 값이 완전히 새로 복사되는 것이 아니라, 가장 바깥쪽에 있는 값만 복사**된다.<br/>

=> 따라서 내부의 값이 객체라면, 내부의 값 또한 따로 복사를 해야한다!<br/>

내부 요소가 바뀌었을 때에도 state를 바꾸고, DOM을 다시 그리기 위해서는,<br/>
새로운 객체나 배열을 만들어 **새로운 참조값**을 만들고<br/>
React에게 **이 값은 이전과 다른 참조값**임을 알려야한다!<br/>

### 10-2. 해결법
 -->









## 9. 데이터를 저장하는 방법

상태관리 라이브러리 사용 <br/>

앱에서 나오는 데이터를 어디에 저장해야할까?

### 5-1. Redux

- 엄청 간단한 중앙 저장소
- RAM 같은 존재
- 앱 꺼지면 날아간다 (따라서 안전함)
- 데이터를 불러올 때 성능이 가장 좋다




### 5-2. AsyncStorage / EncryptStorage

껐다켜도 저장되어야하는 데이터를 넣는다

AsyncStorage
- 암호화되지 않음
- 누구나 열어볼 수 있어서 위험하다
- 따라서 보안에 민감하지 않은, 계속 유지되어야하는 데이터

EncryptStorage
- 암호화됨
- 보안에 민감한 데이터
- AsyncStorage와 사용방법 동일

### 5-3. react-native-config

개발 환경별로 달라지는 값은 react-native-config


### 5-4. 요약

- 보안에 민감하다면?
  - 앱을 꺼도 저장되어야한다면 encrypted-storage
  - 앱을 끄면 날아가도 된다면 redux
- 개발 환경별로 달라지는 값이라면?
  - react-native-config에 저장(암호화 안 됨)
- 그 외 유지만 되면 되는 데이터들
  - async-storage에 저장(npm install @react-native-async-storage/async-storage)













## 10. 프로세스와 스레드


프로세스와 스레드의 차이 

프로세스는 운영체제로부터 자원을 할당받는 작업의 단위이고 스레드는 프로세스가 할당받은 자원을 이용하는 실행 단위이다. 멀티프로세싱보다 멀티스레딩을 하는 이유는 운영체제로부터 자원을 할당 하는 프로세싱 작업을 많이 하는 것 보다 스레딩을 여러개 하는것이 훨씬 더 시스템 자원을 효율적으로 관리할 수 있다.


## 11. CSR, SSR

CSR과 SSR의 차이?

CSR의 과정 :
  - 서버가 브라우저에게 응답을 보냄 -> 브라우저는 JS를 다운 받음 -> 브라우저는 리액트를 실행 -> 페이지가 보여지고 상호작용 함
SSR의 과정 :
 - 서버가 브라우저에게 HTML 응답 랜더링하기 위한 준비가 되었다고 보냄 -> 브라우저가 페이지랜더링, 페이지가 보여지고 브라우저는 JS 다운받음 -> 브라우저 리액트 실행 -> 페이지 상호작용 가능

CSR은 마지막 단계 전까지 화면에 보여지지가 않고 로딩중 / SSR은 미리 페이지가 보여진다.
즉, CSR은 초기로딩속도가 느리긴하지만, 화면전환에 있어서 클라이언트에서 이루어져서 빠른 전환이 가능
SSR은 초기로딩속도가 빨라서 사용자가 느끼기엔 좋지만, 동작은 하지않음. 그리고 화면전환에 있어서 서버에 요청해야하므로 서버에 부담을 줄 수 있음. 
어떤게 더 좋다보다 서비스마다 사용자의 요구마다 다름.



## 12. 자바스크립트

다른언어에는 int float 와 같은 다양한 숫자 타입이 있지만 자바스크립트에는 number 하나만 있다.

### 12-1. 타입

원시타입

number
string
boolean
null
undefined
symbol

(undefined는 선언하고 값을 미할당 - 자료형이 없음, 선언하고 빈 값 할당)


### 12-2. 실행컨텍스트

자바스크립트 코드들이 실행되기 위한 환경
전역 컨텍스트와 함수 컨텍스트가 존재
전역 컨텍스트 생성 후에 함수 호출시마다 함수 컨텍스트가 생성
컨텍스트 생성 후 함수가 실행될때 사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프체인을 따라 올라가며 찾는다


자바스크립트는 실행 컨텍스트가 활성화되는 시점에 선언된 변수를 상단으로 끌어 올리고 (호이스팅), 외부 환경 정보를 구성하고, this 값을 설정하는 등의 동작을 수행하는데 이 과정에서 다른 언어에선 볼 수 없는 현상들이 발생합니다.


자바스크립트는
실행 컨텍스트가 활성화되는 시점에 선언된 변수를 상단으로 끌어올리고(호이스팅)
외부 환경 정보를 구성하고, this 값을 설정하는 등의 동작을 수행합니다.

자바스크립트의 코드가 실행되기 위해서는 변수객체, 스코프체인, this 정보들을 담고 있는 곳을 실행컨텍스트



### 12-3. 호이스팅

변수를 선언하고 초기화 했을 때 선언부분이 최상단으로 끌어올려지는 현상


### 12-4. 클로저

내부함수가 자신이 선언됬을때의 환경인 스코프를 기억하여
그 환경 밖에서 호출되어도 그 환경에 접근할 수 있는 함수, 자신이 생성될때의 환경을 기억하는 함수 

### 12-5. 가비지 컬렉터

할당된 메모리를 추적하고 해당 메모리 영역이 필요하지 않은 영역일 경우를 판단해서 회수하는 것

자바스크립트에서 변수는 직접 참조 값을 가지고있지 않고, 해당 값을 메모리 상에 저장한다
만약 더이상 참조할 것이 없을 때 가비지 컬렉터가 동작해서 메모리가 반환됨.



이벤트 루프에 대해서 설명, 동시성 모델에 대해서 설명

자바스크립트는 싱글 스레드 기반 언어이다. 함수를 실행하면 함수 호출이 스택에 순차적으로 쌓이고 스택의 맨위에서부터 아래로 한번에 하나의 함수만 처리 할 수 있다.  
하지만, 자바스크립트에는 이벤트 루프라는것을 통해 동시성을 지원한다. (동시에 일어나는 것이 아니라 동시에 일어나는 것처럼 보이게 하는것이다!) 
이벤트 루프는 콜 스택에서 실행 중인 게 있는지 확인하고, Event queue에 작업이 있는지 확인해서 콜스택이 비어있다면 이벤트큐 내의 작업이 콜스택으로 이동되어서 실행된다. 

### 12-6. 자바스크립트 동작 원리





## 13. 객체지향과 함수형

객체지향 프로그래밍은 코딩 패러다임 중 하나로
데이터를 추상화 시켜서 상태와 행위를 가진 객체를 만들고,
그 객체들 간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법

- 장점
한 번 작성한 코드를 다시 사용할 수 있어서 코드 재사용성이 좋다
만들어진 객체를 발전시킬 수 있어 유지보수가 쉽다


## 14. 프로토타입

- 정의
 1. 생성자 함수(constructor)가 있을때,
 2. new 연산자를 써서 instance 를 만들면,
 3. 생성자 함수의 prototype 이라고 하는 프로퍼티가
 4. instance 의 __proto__ 라고 하는 프로퍼티에 전달된다. => 생성자 함수의 prototype과 instance 의 __proto__ 라고 하는 프로퍼티는 같은 객체를 참조하게 된다.****
 5. __proto__ 는 내부 프로퍼티에 접근할 때 이 단어를 생략할 수 있다.


객체는 프로퍼티를 가질 수 있는데 prototype이라는 프로퍼티는 그 용도가 약속되어 있는 특수한 프로퍼티다. prototype에 저장된 속성들은 생성자를 통해서 객체가 만들어질 때 그 객체에 연결된다.

## 15. Babel

Babel이란?
babel은 컴파일러 인가 ? 트랜스파일러인가?
트랜스파일러이다. 컴파일은 한 언어로 작성된 소스 코드를 다른 언어로 바꾸는것(C-> 어셈블리어)
트랜스파일러는 한언어로 작성된 소스코드를 비슷한 수준의 추상화를 가진 다른 언어로 변환
(C++>C, ES6->ES5)


## 16. es6에서 추가된 것은?

let, const, rest parameter, class, arrow function...

let, const, 화살표함수, 클래스, 프로미스, 스프레드 연산자 등

let, const, arrow function, Symbol, rest parameter, 스프레드 연산자, 


### 16-1. var 와 let, const의 차이점은 무엇인가 (function scope와 block scope의 개념에서)

var은 함수 레벨 스코프를 지원, let,const는 블록레벨 스코프를 지원한다.

var는 블록 스코프의 영향을 받지 않는다
let, const에서만 동작한다


let, const에 대해서 실제로 

선언보다 이른 호출은 참조 에러를 띄웁니다.
하지만 var로 선언한 변수는 undefined를 할당해 오류가 나지 않음





- 함수 스코프, 실행 컨텍스트 (function scope, execution context)
  - 스코프(scope) : 변수의 유효범위
  - 실행 컨텍스트(execution context) : 실행되는 코드덩어리 (추상적 개념)

  - 둘의 가장 큰 차이는 발생 시점
    - >> 스코프는 함수가 '정의' 될 때 결정된다.
    - >> 실행 컨텍스트는 함수가 '실행' 될 때 생성된다.

  - 실행 컨텍스트에는 호이스팅 후의 함수 본문 내용과 this가 무엇인지에 대한 정보가 담긴다.
  - 즉, 실행 컨텍스트는 사용자가 함수를 호출했을 때에 내부적으로 해당 함수를 실행하기 위해 불러 모은 집합체.











<!-- 





- 브라우저의 렌더링 과정

- OOP

OOP에 특징에 대해 설명해달라(상속, 캡슐화 등등...)
현실에 상황을 예로 들어 OOP의 개념으로 설계과정을 설명해달라
ex) 축구를 게임으로 만든다거나, 기타 어떠한 상황이라도 좋다


- 함수형 프로그래밍(Function Programming)
  - 함수형 프로그래밍에 대해 설명해달라
  - 함수형 프로그래밍에 개념에서 순수함수란 무엇인가
  - OOP와 함수형 프로그래밍의 가장 큰 차이점은 무엇인가
- 비동기 프로그래밍(Asynchronous)
  - AJAX란 무엇인가
  - Promise란 무엇이며 코드가 어떻게 구성되어있는가
  - Promise와 Callback의 차이점은 무엇이며 각각의 장단점에 대해 설명해달라
  - Async, Await가 무엇이며, 사용해본 경험이 있는가
- Vue.js
  - 면접관을 Vue.js 비사용자라고 가정하고 Vue.js에 설명하고 장단점을 말해달라
  - Vue.js의 Life-cycle에 대해 아는대로 말해달라
  - Vue.js 에서 DOM은 어느 시점에 생성되나
  - Computed와 Methods의 차이점은 무엇인가
  - 가상돔(Virtual DOM) 개념은 무엇이며, DOM과의 차이점 가상돔의 개념이 사용되게된 배경은 무엇인가
  - 최근의 프레임워크를 사용할때 외부 라이브러리와의 결합시에 더 나은 코드 작성법을 고민해본적이 있는가
  - DOM을 직접 조작하는 D3.js 같은 라이브러리와의 결합시에 예상되는 문제점이 있는가


- 타입스크립트를 사용해본 경험이 있는가, 타입스크립트에 대한 본인의 생각과 도입시의 장점을 말해달라
- 자바스크립트의 원시 타입(Primitive Data Type)은 몇가지이며, 전부 말해달라
  - Number, String, Boolean, Null, Undefined, (Symbol)
  - 자바스크립트의 Number Type은 다른 언어들과 차이점이 무엇인가, 왜 하나만 존재하는가
- 실행 컨텍스트(Execution Context)에 대해 설명해달라
- 자바스크립트의 호이스팅(Hoisting)은 어떻게 이루어져 있는가
- 클로저(Closure)란 무엇이며, 왜 이러한 패턴을 사용하는가
- This
  자바스크립트에서 This는 몇가지로 추론 될수 있는가, 아는대로 말해달라
  Call, Apply, Bind 함수에 대해 설명해달라
- ES6
  - 크롬 정도의 브라우저를 제외하곤 ES6 스펙에 대한 지원이 완벽하지 않다. 해결방법은 무엇인가
  - Babel의 기능을 한 단어로 말해달라
  - ES6 에서 추가된 스펙에 대해 아는대로 다 말해달라(let, const, rest parameter, class, arrow function...)
  - var 와 let, const의 가장 큰 차이점은 무엇인가 (function scope와 block scope의 개념에서)
  - Class 는 무엇이고, Prototype, fucntion의 ES5 스펙만으로 Class를 구현할수 있는가
- 자료구조(Data Structure)
  - 자료구조에 대해 공부한 적이 있는가
  - Binary Search Tree 에 대해 알고 있는가, 설명해달라
  - Graph 에서 다른 노드를 참조하는 구조를 코드로 구현 할수 있는가
- RESTful API 가 무엇인가, 아는대로 다 말해달라
- 클라이언트 개발시 보안 관련 이슈
  - 보안은 서버쪽에서 많이 신경쓰고 있지만, 프론트엔드 개발에서 보안관련 이슈는 어떠한 것들이 있는가
  - Wireshark 에 대해 알고 있는가
  - HTTP 통신의 문제점에 대해서 아는대로 말해달라
  - CORS(Cross-Origin Resource Sharing)는 무엇인가 왜 이러한 방법이 정의 되었으며, 본인이 코드를 작성하면서 CORS와 관련하여서 경험하였던 이슈는 무엇인가
  - 간단한 데이터를 클라이언트로만 관리 할수 있는가, 이와 관련해서 브라우저 에서 어떠한 것들을 지원하고 있는가, 예를 들면 소셜 로그인같은 것들에 대한 브라우저 종료시 발생하는 문제에 대응 경험이 있는가
 -->


  > 참조

  https://bamtory29.tistory.com/entry/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0

  https://www.daleseo.com/react-hooks-use-memo/

  