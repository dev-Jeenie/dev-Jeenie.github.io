---
title: "#09. Array APIs 🍋"
permalink: /cs/JavaScriptArrayAPIs
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-07
last_modified_at: 2021-11-07
---

![]()


# Array APIs를 총정리해보자!

목차 겸 요약!

- join : 배열에서 구분자로 나눠서 string으로
- split : string에서 구분자로 나눠서 배열로
- reverse : 배열을 거꾸로
- splice : 배열 자체에서 데이터를 잘라내서, 잘라낸 걸 return (원본변경)
- slice :  배열의 시작점, 끝점을 지정해 새로운 배열로 return (원본유지)
- find : 배열요소 중 callback함수에 해당하는 요소들만 return
- filter : callback함수에 해당하는 요소들만 return
- map : 배열요소를 다른 배열로 return
- some : 배열요소 중 조건에 만족하는 것이 있으면 true,없으면 false를 return
- every : 모든 배열요소가 조건에 만족해야만 true, 아니면 false를 return
- reduce : 배열의 모든 요소들의 값을 누적해서 return

## join

- Q1. make a string out of an array

<img src="/assets/images/JS_array_api_join.jpeg" /><br/>



```js

{
  const fruits = ["apple", "banana", "orange"];
  const result2 = fruits.join("/");
  console.log(result2);
}

```

## split
<img src="/assets/images/JS_array_api_split.jpeg" /><br/>

- Q2. make an array out of a string

```js
{
  const fruits = "🍎, 🥝, 🍌, 🍒";
  const result = fruits.split(",", 2);
  console.log(result);
}
```

## reverse

<img src="/assets/images/JS_array_api_reverse.jpeg" /><br/>
- Q3. make this array look like this: [5, 4, 3, 2, 1]
기존의 배열 자체와, 리턴값도 변화시킨다

```js
{
  const array = [1, 2, 3, 4, 5];
  const result = array.reverse();
  console.log(result);
}
```
## splice
<img src="/assets/images/JS_array_api_splice.jpeg" /><br/>


- Q4. make new array without the first two elements

splice<br/>
: 기존 배열 자체에서 데이터를 잘라내서 새로운 배열을 리턴


```js
{
  const array = [1, 2, 3, 4, 5];
  const result = array.splice(0, 2);
  console.log("result", result);
  console.log("array", array);
}
```


## slice

<img src="/assets/images/JS_array_api_slice.jpeg" /><br/>

- Q4. make new array without the first two elements

slice<br/>
: 기존 배열은 유지, 원하는 부분만 새로운 배열로 리턴한다

```js
{
  //정답 :
  const array = [1, 2, 3, 4, 5];
  const result = array.slice(2, 5);
  console.log("result", result);
  console.log("array", array);
}
```
## find
<img src="/assets/images/JS_array_api_find.jpeg" /><br/>

```js
class Student {
  constructor(name, age, enrolled, score) {
    this.name = name;
    this.age = age;
    this.enrolled = enrolled;
    this.score = score;
  }
}
const students = [
  new Student("A", 29, true, 45),
  new Student("B", 28, false, 80),
  new Student("C", 30, true, 90),
  new Student("D", 40, false, 66),
  new Student("E", 18, true, 88),
];

```
- Q5. find a student with the score 90

predicate 콜백함수. this,value,index,obj => value에는 boolean으로 정의되는 함수를 전달해주면 되는구나<br/>
전달된 predicate가 true이면, 첫번째로 찾아진 요소를 리턴한다. 찾지 못하면 undefined를 리턴한다<br/>
호출되어지는 콜백 함수가, true를 리턴하면, 함수를 멈추고 true가 된 그 요소를 return한다<br/>
```js
{
  const result = students.find(function (student, index) {
    return student.score === 90;
  });
  console.log(result);
}
```


## filter


<img src="/assets/images/JS_array_api_filter.jpeg" /><br/>

- Q6. make an array of enrolled students

callBack함수를 전달해서, callBack함수가 true인 것들만 모아서 새로운 배열을 전달

```js
{
  const result = students.filter((student) => student.enrolled);
  console.log(result);
}
```

## map


<img src="/assets/images/JS_array_api_map.jpeg" /><br/>

- Q7. make an array containing only the students' scores

배열안에 들어있는 요소 한가지 한가지를 다른 것으로 변환해주는 API

```js
{
  const result = students.map((student) => student.score);
  console.log(result);
}
```


## some / every

<img src="/assets/images/JS_array_api_some_every.jpeg" /><br/>


- Q8. check if there is a student with the score lower than 50

```js
{

  const result = students.some((student) => student.score < 50);
  console.log(result);
  const result2 = students.every((student) => student.score >= 50);
  console.log(result2);
}

```






## reduce

<img src="/assets/images/JS_array_api_reduce.jpeg" /><br/>
<img src="/assets/images/JS_array_api_reduce_2.jpeg" /><br/>

- Q9. compute students' average score

```js
{
  const result = students.reduce((prev, curr) => prev + curr.score, 0);
  console.log(result / students.length);
}

```

## map + filter + join


 Q10. make a string containing all the scores

```js
{
  const result2 = students
    .map((student) => student.score)
    // map으로 student를 score로 변환했으니, 여기부터는 score가 온다
    .filter((score) => score >= 50)
    .join(",");
  console.log(result2);
}
```

## sort

<img src="/assets/images/JS_array_api_sort.jpeg" /><br/>


Bonus! do Q10 sorted in ascending order

```js
{
  const result = students.map((student) => student.score).sort((a, b) => a - b);
  console.log(result);
}
```