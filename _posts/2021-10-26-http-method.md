---
title: "HTTP method"
permalink: /cs/httpmethod
tags:
  - [CS]

navigation: true
toc: true
toc_sticky: true

date: 2021-10-26
last_modified_at: 2021-10-28
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
RUCD 중 READ 에 해당
요청 URL에 데이터를 붙여서 전송(얻기위함)


"서버야 나한테 이것 좀 줘, 이걸 얻어야겠어"
ex) 네이버의 검색

- 요청 URL 길이에 제한이 있음(URL에 데이터를 담아 전송하기 때문에 요청URL의 길이 제한이 있다)
- 전송 데이터 노출에 따른 위험

링크를 클릭할 때, 입력상자에 데이터를 입력하거 나 체크박스를 체크할 때 전송되는 값들이 URL 뒤에 값을 붙여서 보내는 방식이다

  ## POST 방식
RUCD 중 CREATE 에 해당
HTTP body에 데이터를 담아서 전송(보내기위함)


"서버야 이것 좀 받아. 이거 가지고 뭐 해"

- 데이터 전송 길이에 대한 제한이 없음 (body에 데이터를 담아 전송하기 때문에 길이 제한이 없다)
- HTTP REQUEST BODY에 데이터를 담으므로 노출 안됨
★ 보안성과는 전혀 상관없음! 이걸 보안이 좋다고 생각하면 안됨. BODY에 들어간 정보들은 공유기나 PC


HTTP 네트워크 프로토콜은, REQUEST를 하든 RESPONSE를 하든
서버와 클라이언트 간에는 HTTP HEADER와 HTTP BODY를 전송함
GET같이 요청할 때에는 HTTP HEADER에 요청을 적어서 보내고, (BODY는 비어있음)
POST같이 데이터를 보낼 때에는 HTTP BODY에 데이터를 담아서 보낸다

서버에서 처리를 한 뒤에 결과를 RESPONSE 해줄 건데, 그 RESPONSE의 모양도 동일하게
RESPONSE HEADER와 RESPONSE BODY로 이루어져있다
RESPONSE HEADER에는 응답코드(201, 404, 500 등)과 브라우저에 응답해 줄 추가적인 코드가 들어가고
RESPONSE BODY에는 브라우저에 보여질 데이터들(html tag, 텍스트 등)이 들어간다

=>
HEADER에는?
요청 시 : 요청에 관련된 정보
응답 시 : 응답에 관련된 정보

BODY에는?
요청 시 : 요청시 줘야하는 것들 (method 방식에 따라서 body를 쓸지말지 결정)
응답 시 : 응답할 내용이 있으면 주고 없으면 안줄 수도 있음



### REST API
 "요청에 명확한 의미를 주자"
REST API가 나오면서 GET, POST, PUT, DELETE로 사용