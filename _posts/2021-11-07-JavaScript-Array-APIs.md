---
title: "#09. Array APIs ๐"
permalink: /js1/JavaScriptArrayAPIs
tags:
  - [js1]

navigation: true
toc: true
toc_sticky: true

date: 2021-11-07
last_modified_at: 2021-11-07
---

![]()


# Array APIs๋ฅผ ์ด์ ๋ฆฌํด๋ณด์!

๋ชฉ์ฐจ ๊ฒธ ์์ฝ!

- join : ๋ฐฐ์ด์์ ๊ตฌ๋ถ์๋ก ๋๋ ์ string์ผ๋ก
- split : string์์ ๊ตฌ๋ถ์๋ก ๋๋ ์ ๋ฐฐ์ด๋ก
- reverse : ๋ฐฐ์ด์ ๊ฑฐ๊พธ๋ก
- splice : ๋ฐฐ์ด ์์ฒด์์ ๋ฐ์ดํฐ๋ฅผ ์๋ผ๋ด์, ์๋ผ๋ธ ๊ฑธ return (์๋ณธ๋ณ๊ฒฝ)
- slice :  ๋ฐฐ์ด์ ์์์ , ๋์ ์ ์ง์ ํด ์๋ก์ด ๋ฐฐ์ด๋ก return (์๋ณธ์ ์ง)
- find : ๋ฐฐ์ด์์ ์ค callbackํจ์์ ํด๋นํ๋ ์์๋ค๋ง return
- filter : callbackํจ์์ ํด๋นํ๋ ์์๋ค๋ง return
- map : ๋ฐฐ์ด์์๋ฅผ ๋ค๋ฅธ ๋ฐฐ์ด๋ก return
- some : ๋ฐฐ์ด์์ ์ค ์กฐ๊ฑด์ ๋ง์กฑํ๋ ๊ฒ์ด ์์ผ๋ฉด true,์์ผ๋ฉด false๋ฅผ return
- every : ๋ชจ๋  ๋ฐฐ์ด์์๊ฐ ์กฐ๊ฑด์ ๋ง์กฑํด์ผ๋ง true, ์๋๋ฉด false๋ฅผ return
- reduce : ๋ฐฐ์ด์ ๋ชจ๋  ์์๋ค์ ๊ฐ์ ๋์ ํด์ return

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
  const fruits = "๐, ๐ฅ, ๐, ๐";
  const result = fruits.split(",", 2);
  console.log(result);
}
```

## reverse

<img src="/assets/images/JS_array_api_reverse.jpeg" /><br/>
- Q3. make this array look like this: [5, 4, 3, 2, 1]
๊ธฐ์กด์ ๋ฐฐ์ด ์์ฒด์, ๋ฆฌํด๊ฐ๋ ๋ณํ์ํจ๋ค

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
: ๊ธฐ์กด ๋ฐฐ์ด ์์ฒด์์ ๋ฐ์ดํฐ๋ฅผ ์๋ผ๋ด์ ์๋ก์ด ๋ฐฐ์ด์ ๋ฆฌํด


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
: ๊ธฐ์กด ๋ฐฐ์ด์ ์ ์ง, ์ํ๋ ๋ถ๋ถ๋ง ์๋ก์ด ๋ฐฐ์ด๋ก ๋ฆฌํดํ๋ค

```js
{
  //์ ๋ต :
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

predicate ์ฝ๋ฐฑํจ์. this,value,index,obj => value์๋ boolean์ผ๋ก ์ ์๋๋ ํจ์๋ฅผ ์ ๋ฌํด์ฃผ๋ฉด ๋๋๊ตฌ๋<br/>
์ ๋ฌ๋ predicate๊ฐ true์ด๋ฉด, ์ฒซ๋ฒ์งธ๋ก ์ฐพ์์ง ์์๋ฅผ ๋ฆฌํดํ๋ค. ์ฐพ์ง ๋ชปํ๋ฉด undefined๋ฅผ ๋ฆฌํดํ๋ค<br/>
ํธ์ถ๋์ด์ง๋ ์ฝ๋ฐฑ ํจ์๊ฐ, true๋ฅผ ๋ฆฌํดํ๋ฉด, ํจ์๋ฅผ ๋ฉ์ถ๊ณ  true๊ฐ ๋ ๊ทธ ์์๋ฅผ returnํ๋ค<br/>
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

callBackํจ์๋ฅผ ์ ๋ฌํด์, callBackํจ์๊ฐ true์ธ ๊ฒ๋ค๋ง ๋ชจ์์ ์๋ก์ด ๋ฐฐ์ด์ ์ ๋ฌ

```js
{
  const result = students.filter((student) => student.enrolled);
  console.log(result);
}
```

## map


<img src="/assets/images/JS_array_api_map.jpeg" /><br/>

- Q7. make an array containing only the students' scores

๋ฐฐ์ด์์ ๋ค์ด์๋ ์์ ํ๊ฐ์ง ํ๊ฐ์ง๋ฅผ ๋ค๋ฅธ ๊ฒ์ผ๋ก ๋ณํํด์ฃผ๋ API

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
    // map์ผ๋ก student๋ฅผ score๋ก ๋ณํํ์ผ๋, ์ฌ๊ธฐ๋ถํฐ๋ score๊ฐ ์จ๋ค
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