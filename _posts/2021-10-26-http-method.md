---
title: "HTTP method"
permalink: /cs/httpmethod
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-26
last_modified_at: 2021-10-26
---

![]()

HTTP method란?

클라이언트에서 서버로 요청을 하고, 서버에서 거기에 대한 응답을 줄 때 사용하는 프로토콜

이 동작은 클라이언트에서 서버로 요청을 하는 것으로 시작
요청할때 요청정보 안에는 method 정보가 있다. 어떤 목적을 가지고 요청을 하는지, 목적이 무엇인지 표시하는 것이 GET, POST
REST API가 나오기 전에는 이 두가지로도 모든 것을 할 수 있었음.

# HTTP REQUEST METHOD
:클라이언트(웹 브라우저)에서 서버(tomcat)로 요청 시 데이터 전달 방식

  ## GET 방식
= 얻기 위한 것
RUCD 중 READ 에 해당

  ## POST 방식
= 보내기 위한 것
RUCD 중 CREATE 에 해당


### REST API
 "요청에 명확한 의미를 주자"
REST API가 나오면서 GET, POST, PUT, DELETE로 사용
