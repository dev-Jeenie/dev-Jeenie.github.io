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

# HTTP method란 무엇인가?

<strong>클라이언트에서 서버로 요청을 하고, 서버에서 거기에 대한 응답을 줄 때 사용하는 프로토콜</strong><br/>

이 동작은 클라이언트에서 서버로 요청을 하는 것으로 시작<br/>
요청할때 요청정보 안에는 method 정보가 있다.<br/>
어떤 목적을 가지고 요청을 하는지, 목적이 무엇인지 표시하는 것이 GET, POST<br/>
REST API가 나오기 전에는 이 두가지로도 모든 것을 할 수 있었음.<br/>

# HTTP REQUEST METHOD
:클라이언트(웹 브라우저)에서 서버(tomcat)로 요청 시 데이터 전달 방식

## GET 방식
RUCD 중 READ 에 해당<br/>
요청 URL에 데이터를 붙여서 전송(얻기위함)<br/><br/>


"서버야 나한테 이것 좀 줘, 이걸 얻어야겠어"<br/><br/>
ex) 네이버의 검색

- 요청 URL 길이에 제한이 있음(URL에 데이터를 담아 전송하기 때문에 요청URL의 길이 제한이 있다)
- 전송 데이터 노출에 따른 위험

링크를 클릭할 때, 입력상자에 데이터를 입력하거나 체크박스를 체크할 때 전송되는 값들이 <br/>
URL 뒤에 값을 붙여서 보내는 방식이다<br/>


## POST 방식
RUCD 중 CREATE 에 해당<br/>
HTTP body에 데이터를 담아서 전송(보내기위함)<br/><br/>


"서버야 이것 좀 받아. 이거 가지고 뭐 해"<br/><br/>

- 데이터 전송 길이에 대한 제한이 없음 (body에 데이터를 담아 전송하기 때문에 길이 제한이 없다)
- HTTP REQUEST BODY에 데이터를 담으므로 노출 안됨

<hr />
<strong>★ 보안성과는 전혀 상관없음! </strong>
GET은 주소 뒤에 붙으니까 안전하지 않고, POST는 BODY에 들어가니까 안전하구나 (X)<br/>
이걸 보안이 좋다고 생각하면 안됨. BODY에 들어간 정보들은 공유기나 PC에 연결해서 중간에 가로채면 다 보인다<br/>

그래서 암호화를 할 수 있는 프로토콜이 추가되어야 안전함.<br/>

<b>암호화를 위해 사용하는 것이 https://</b><br/>
http만 가지고 하면 보안이 취약한 사이트. https가 있어야 안전한 사이트다<br/>
톰캣 서버에 secure socket layer(ssl)라는 프로토콜을 연동해야 함.<br/>

=> 
<strong>http 프로토콜 + secure socket layer = https 프로토콜</strong>

<hr />

HTTP 네트워크 프로토콜은, REQUEST를 하든 RESPONSE를 하든<br/>
서버와 클라이언트 간에는 HTTP HEADER와 HTTP BODY를 전송함<br/><br/>
GET같이 요청할 때에는 HTTP HEADER에 요청을 적어서 보내고, (BODY는 비어있음)<br/>
POST같이 데이터를 보낼 때에는 HTTP BODY에 데이터를 담아서 보낸다<br/>

서버에서 처리를 한 뒤에 결과를 RESPONSE 해줄 건데, 그 RESPONSE의 모양도 동일하게
RESPONSE HEADER와 RESPONSE BODY로 이루어져있다<br/>
RESPONSE HEADER에는 응답코드(201, 404, 500 등)과 브라우저에 응답해 줄 추가적인 코드가 들어가고<br/>
RESPONSE BODY에는 브라우저에 보여질 데이터들(html tag, 텍스트 등)이 들어간다

=>
HEADER에는?
- 요청 시 : 요청에 관련된 정보
- 응답 시 : 응답에 관련된 정보

BODY에는?
- 요청 시 : 요청시 줘야하는 것들 (method 방식에 따라서 body를 쓸지말지 결정)
- 응답 시 : 응답할 내용이 있으면 주고 없으면 안줄 수도 있음

## GET과 POST의 차이

<img src="/assets/images/HTTP_example.png" /><br/><br/>
이름과 나이를 입력해서 전송 버튼을 누르는 것이 클라이언트에서 서버로 request를 하는 것.

1. GET의 경우

<img src="/assets/images/GET_example_result.png" /><br/><br/>
요청하는 method 방식과 어디로 요청하는지 정보, 서버에 전달해주고자 하는 값이 들어간다<br/>
이 때에 HTTP REQUEST <b>HEADER에 정보들이 들어간다.</b> HTTP REQUEST BODY에는 표시할 데이터가 없다<br/>
=> 전송버튼을 누르는 것은, BODY와 HEADER라는 HTTP 프로토콜 형식에 맞춰서 데이터를 만들고 서버로 보내는 것이다.

2. POST의 경우

<img src="/assets/images/POST_example_result.png" /><br/><br/>
이 때에 HTTP REQUEST <b>HEADER에 정보들이 들어가지 않는다.</b> 대신 HTTP REQUEST BODY에 정보들이 들어간다 <br/>
=> 전송버튼을 누르는 것은, BODY와 HEADER라는 HTTP 프로토콜 형식에 맞춰서 데이터를 만들고 서버로 보내는 것이다.<br/>


GET은 주소줄에 값이 ?뒤에 쌍으로 이어붙고 POST는 숨겨져서(body안에) 보내진다.<br/>
GET은 URL에 이어붙기 때문에 길이제한이 있어서 많은양의 데이터는 보내기 어렵고 POST는 많은 양의 보내기에도 적합하다.(역시 용량제한은 있지만)<br/>
즉 http://url/bbslist.html?id=5&pagenum=2 같이 하는 것이 GET방식이고 form을 이용해서 submit을 하는 형태가 POST입니다.<br/>




<strong>정리!<strong><br/>
클라이언트에서 서버로 요청 시 (REQUEST) 데이터 전달 개념<br/>
- GET
- POST
이때, 요청과 함께 전달하는 값을 파라미터라고 부른다<br/>

서버에서는 클라이언트 요청으로 전달된 parameter를 꺼내서 사용함.<br/>
강의 참조 https://www.youtube.com/watch?v=aCSryu_emlA&t=263s



## 뒤로가기 클릭 시 만료된 페이지가 뜨는 이유?
뒤로가기 버튼을 눌렀을 때, 해당 페이지를 구성하는 정보 중에서 static하지 않은 정보가 있을 수 있습니다. 즉, 해당 페이지를 보여주기 위해서 API를 통해서 전달받은 데이터가 필요한 경우입니다. API를 통해서 받은 데이터를 모두 다 cache해두면 좋겠지만 브라우저의 보안 정책의 이유로 cache되지 못하는 상황이 발생합니다.

바로 이 때 만료된 문서라는 페이지를 보게됩니다. 페이지를 띄워야해서 데이터가 필요한데, 필요한 데이터가 cache되어 있지 않습니다. 그려면 다시 API 요청을 보내야합니다. 그런데 만약 해당 페이지에 또 다른 데이터를 추가/수정하는 API Call이 포함된 경우 의도치 않은 동작이 발생할 수 있습니다. 이를 막기 위해서 브라우저에서 자체적으로 API 요청을 다시 날릴 것인지 확인하는 페이지를 띄우고 이게 만료된 페이지입니다.

POST를 사용할 때는 중복 요청에 대한 대비가 필요하다Permalink
위에서 언급한 의도치 않은 동작은 POST를 수행할 때의 이야기 입니다. 일반적으로 GET은 데이터를 조회할 때, POST는 수정, 삭제 할 때 사용합니다. 따라서 GET으로 데이터를 조회하는 것은 뒤로가기 버튼 눌러서 다시 수행되어도 큰 문제가 없습니다. POST가 꼭 필요해서 POST를 사용할 때에도, 만료된 문서페이지를 볼 수 있기 때문에, 중복된 POST에 대한 처리를 서비스에 맞게 잘 구현해야 합니다. keyword를 전달해서 이를 기반으로 sort를 하는 경우는 GET으로 수행하는 것이 바람직합니다.




# 그럼 REST API는 뭔데?
https://www.youtube.com/watch?v=PmY3dWcCxXI

웹의 통신규약인 HTTP를 이용하는 API(컴퓨터의 기능을 실행시키는 방법)

<strong>"요청에 명확한 의미를 주자"<strong><br/>
REST API가 나오면서 GET, POST, PUT, DELETE로 사용<br/>



