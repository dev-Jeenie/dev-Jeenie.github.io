---
title: "React란? 리덕스!"
permalink: /cs/ReactProgrammingRedux
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-12-02
last_modified_at: 2021-12-02
---

![]()

# 리덕스

상태관리 라이브러리

- 컴포넌트 코드로부터 상태 관리 코드를 분리할 수 있따

- 미들웨어를 활용한 다양한 기능 추가
  - 강력한 미들웨어 라이브러리(리덕스 사가 등)
  - 로컬스토리지에 데이터 저장하기 및 불러오기
- SSR시 데이터 전달이 간편 (서버사이드랜더링)
- 리엑트 콘텍스트보다 효율적인 렌더링 가능

하나의 객체로 표현가능. 이 객체 하나만 보내면 편리하게 관리할 수 있음

## context API와 Redux의 랜더링 성능 비교

context API에서는, 하나의 객체로 감싸진 상태값 두개 중 하나만 변경되어도
해당 객체를 사용하는 모든 컴포넌트가 랜더링된다.

Redux에서는, 하나의 객체로 감싸진 상태값 두개 중 하나만 변경되면
다른 처리를 할 필요 없이 해당 객체 중 변경된 상태값을 사용하는 컴포넌트가 랜더링된다.


## 리덕스 구조

- 액션
  - 타입 속성값을 가진 객체

  store.dispatch({type:'', title:'', priority:''})
  타입속성값은 유니크해야하기 때문에 프리픽스

- 디스패치
  액션이 발생했다는 것을 리듀서에게 알려주는 함수

  
데이터는 리듀서에서 바아서 처리
리듀서는 순수함수

```JS

export const ADD = 'todo/ADD';
//리듀서에서도 쓸테니까 상수변수로 만드는게좋음

  export function addTodo({title,priority}) {
    return ({type:ADD,title,priority})
  }

  store.dispatch(addTodo{type:'', title:'', priority:''})
```
액션 객체의 구조를 일관성있게 만들기 위해서 액션 생성자함수를 사용.
치면서 틀릴 수도 있고 문서로써의 역할도 함. 개발 생산성 향상

안쓰고 작성하면 
  store.dispatch({type:'', title:'', priority:''})
그냥 막 치다가 틀릴 수 있음.

- 미들웨어
const myMiddleware = store => next => 

스토어와 넥스트


액션이 발생하면 미들웨어부터 실행됨.
처음 실행을 시키면 처음 한번 디스패치 실행

미들웨어1 실행
미들웨어2 실행
리듀서 실행
미들웨어2 끝
미들웨어1 끝

미들웨어의 활용 예시 )

맨처음 스토어가 뷰한테 상태값 변경을 알려주니까,
그 스토어를 선언할때, 
첫번째 매개변수로 리듀서(상태값과 액션을 받는)를 넣고
두번째로는 미들웨어를 넣고(갯수에 따라 인자로 1,2,3으로 집어넣을 수 있다)



- 리듀서
  - 상태값은 액션이 발생했을 때 새로운 상태값을 만드는 함수

  리덕스에서 상태값을 바꾸는 유일한 방법
    : 액션객체와 함께 디스패치 메소드를 호출하는 것. 그 외엔 불가!
  상태값은 불볍객체로 관리해야한다



객체를 불변 객체로 관리하기 위해서
immer 라이브러리 추천
첫번째 매개변수로 상태값을 넣고, 두번째 매개변수로는 상태값을 변경하는 로직


리듀서는 순수함수로(부수효괍없어야(외부상태 참조가 없는것))




- 스토어

create 스토어, 안에 리듀서를 넣어서 만ㄷ르어주면 스토어가 만들어짐
스토어는 상태값 저장하는 역할, 액션 처리가 끝났다는 것을 외부에 알려주는 역할.

액션처리끄ㅌ낫다는 것을 알려주기 위해서는
스토어의 subscribe메서드를 호출해서
함수를 입력한다.
그럼 액션발생시 액션처리가 끝나면 그 함수가 호출됨
이전저장, 이전과 현재생성된 값 비교해서 저장하는 함수


## react reducer 없이 직접 구현하기

데이터가 변경됐을 때만 컴포넌트가 랜더링되게 하는 것이 reac-redux 사용의 중요 역할 중 하나.



Provider

루트에서 전체를 감싸주게 사용.
<Provider.store={store}>를 입력하면

- Provider
리액트에서 액션을 처리했을 때,
이벤트 받아서 하위에 있는 다른 컴포넌트가 다시 랜더링 될 수 있도록 도와준다.
그럼 상태값 비교 로직 작성이 필요없음.

리덕스에서 데이터를 가져올 때는?
- useSelector(선택자)
액션처리될때마다 선택자함수가 실행되게 함.
상태값이 매개변수로 넘어오고, 우리가 사용하려고 하는 데이터를 가져오면 됨

const friends = useSelector(state => state.friend.friends)

선택자로는 상태값이 매개변수가 넘어오고, 우리가 사용하려고 하는 데이터를 가져오면 됨.
우리가 사용하고자하는 상태값이 그대로 반환된다.

useSelector 훅은 리덕스에서 액션이 처리되면
여기서 반환하는 값의 이전값을 기억했다가
그 값이 변경되었을 때 이 컴포넌트를 다시 랜더링해준다.

- 여러개의 상태값을 가져오고싶을 때는?
1. 여러개의 useSelector 사용
2. useSelector를 배열로 반환하기
  - const [friends,friends2] = useSelector(state => [state.friend.friends,state.friend.friends2])

  - 근데 배열의 둘 중 리덕스에서 액션 처리될 때마다 불필요하게 랜더링될수있음.
  - 그래서 나온 해결방법 두번째 매개변수로 shallowEqual. 이 두 값이 변경되었을 때만 컴포넌트를 변경한다

=> 이것도 번거롭기때문에 커스텀훅을 사용

커스텀훅을 사용할 때는 값을 하나만 반환하더라도, 배열로 반환하는 게 좋다.
1,2,3이 있을 때 3만 변경되어도 전체를 다 비교함.
그런데 이때 3의 반환값을 배열로 감싸면 비교하는 연산을 줄일 수 있다! 배열로 감싸면 안에있는 것만 비교하기 때문.

- useDispatch

훅으로 가져온다는건 값이 변할수도 있다는 얘기.



## reselect로 선택자함수 만들기
다양한 형식으로 가공을 해야한다.
리덕스에 모든 경우의 수를 다 넣어둘 수는 없으니, 필터연산은 컴포넌트에서 하는 방법이 있음

actionCreator


# 리덕스 사가

리덕스에서 비동기 처리가 필요할 때

- redux-thunk
  - 비동기 로직 간단

- redux-observable
  - 비동기 코드 많을 때
  RxJS 패키지 기반으로 만들어짐 (리액티브 프로그래밍 공부 필요)

- redux-saga
  - 비동기 코드 맣을 때
  - 제너레이터 적극 활용
  - 테스트 코드 작성이 쉽다


put call all 부수효과(effects)
첫째 매개변수로 액션의 타입

## 제너레이터

redux-saga

```JS
function* f1() {
  yield 10;
  yield 20;
  return 'finished';
}
const gen = f1();

console.log(gen.next())
console.log(gen.next())
console.log(gen.next())

```


iterable? Symbol.iterator?



제너레이터는 실행을 멈추고 협업이 가능하다

funtion minsu() {
  const myMsgList = [
    '1',
    '2',
    '3'
  ]
  for() {
    console.log()
  }
}

funtion suji() {
  const myMsgList = [
    '',
    '4',
    '5'
  ]
  for() {
    console.log()
  }
}

함수끼리 협력이 가능하다
사가함수와 사가 미들웨어가 협력할 수 있다


하나의 사가함ㄴ수가 두개의 액션을 처리할 수 있다

function* loginFlow() {
  while(true) {
    const {id,password} = yield take(로그인액션 기다리고)
    yield take(로그아웃 액션 기다리고)
  }
}


짧은시간 같은이벤트가 발생할때, 첫번째나 마지막 것만 사용하는 `debounce`

이때 debounce라는 부수효과함수를 사용

debountce(500, type.타입이름, 실행할 함수)

테스트 코드는 단위별로 작성을 하는 것.
하나의 프로그램을 QA로 잡을 때는 너무 방대함. 그러니까 한번에 잡지 않고
기능이 생길 때마다 테스트를 하는 것.

테스트 작성 범위


