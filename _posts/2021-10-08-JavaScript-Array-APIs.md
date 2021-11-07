---
title: "#09. Array APIs ♨️"
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

// Q1. make a string out of an array
// join(separator?: string): string;

<img src="/assets/images/JS_array_api_join.jpeg" /><br/>



```JS

{
  const fruits = ["apple", "banana", "orange"];
  const result2 = fruits.join("/");
  console.log(result2);
}

```

## split
<img src="/assets/images/JS_array_api_split.jpeg" /><br/>



## reverse

<img src="/assets/images/JS_array_api_reverse.jpeg" /><br/>


## splice
<img src="/assets/images/JS_array_api_splicejpeg" /><br/>



## slice

<img src="/assets/images/JS_array_api_slice.jpeg" /><br/>


## find
<img src="/assets/images/JS_array_api_find.jpeg" /><br/>



## filter


<img src="/assets/images/JS_array_api_filter.jpeg" /><br/>

## map


<img src="/assets/images/JS_array_api_map.jpeg" /><br/>

## some
## every

<img src="/assets/images/JS_array_api_some_every.jpeg" /><br/>





## reduce


<img src="/assets/images/JS_array_api_reduce.jpeg" /><br/>
<img src="/assets/images/JS_array_api_reduce_2.jpeg" /><br/>

