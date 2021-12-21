---
layout: single
title: "HTTP 정리(작성중)"
---

HTTP 정리하려고 한다.

  <br/>
  <br/>
  
# HTTP 란

HTTP(Hyper Text Transfer Protocol)로 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜이다.

80번 포트를 사용하며 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며 클라이언트는 80번 포트로 요청을 보내게 된다.

Stateless와 Connectionless 의 특징을 가진다.

  <br/>
  <br/>
  
# HTTP 메세지 구조

<img src= "https://user-images.githubusercontent.com/58356031/146863335-eae94fce-8a18-47c3-8906-f85b633c6476.png" width="500">


  <br/>
  <br/>
  

### Request 메세지 구조
- Start line(시작라인)

  간단한 예시 : GET/login HTTP/1.1
  
  HTTP Method/Request target/ HTTP Version 형식으로 쓰인다.
  
  HTTP Method 종류로 GET, POST, DELETE가 많이쓰며 Request target 은 해당 request가 전송되는 목표 url이고 HTTP Version은 사용되는 HTTP 버전을 의미한다.
  
- Header(헤더)

  해당 요청에 대한 추가 정보(메타 데이터)를 담고 있느 부분이다.
  
  Host: 요청이 전송되는 목표의 주소(웹사이트의 기분주소) ex)`www.google.com`
  
  User-Agent: 요청을 보내는 클라이언트의 대한 정보(웹브라우저와 버전) ex)chrome, firefox
  
  Accept:  해당 요청이 받을 수 있는 응답 타입 ex) image/gif, image/jpeg, */*
  
  Content-Type: 해당 요청이 보내는 메세지 body의 타입 ex)application/json
  
  Content-Length: body 내용의 길이
  
  Authorization: 회원의 인증/인가를 처리하기 위한 로그인 토근을 담는다.

- Message body(메시지 본문)

  해당 요청의 실제 내용으로 Body를 사용하는 메소드는 대부분 POST이다.
  
  ex) 로그인 시 서버에 보낼 요청의 내용
  Body:{
     "user_email": "`bob@naver.com`"
     "user_password": "alice"
  }
  
  
  <br/>
  <br/>
  
  
### Response 메세지 구조

- Start line(시작라인)

  간단한 예시 : HTTP/1.1 200 OK
  
  Response의 상태를 간략하게 나타내며 HTTP 버전, status code, status text으로 이루어져있다.
  

  
- Header(헤더)

  응답에 대한 추가 정보(메타 데이터)를 담고 있는 부분이다.
  
  Date나 Content-length 등등 똑같이 사용할 수 있지만 응답에서만 사용되는 사용되는 헤더의 정보들이 있다. ex) 요청하는 브라우저의 정보가 담긴 User-Agent 대신 Server 헤더
  
  Server: 웹서버 정보를 나타낸다
  
  Set-Cookie: 서버측에서 클라이언트에게 세션 쿠키 정보를 설정
  
- Message body(메시지 본문)

  요청의 메소드에 따라 body가 존재하지 않을수도 있다. 가장 많이 사용되는 데이터 타입은 JSON이다
  
  ex) 로그인 요청에 대해 성공했을 때 응답의 내용
  Body: {
      "message": "SUCCESS"
      "token": "kldiauahsajm@9df0asmzm" (암호화된 유저의 정보)
  }

  <br/>
  <br/>
  
# HTTP 상태 코드
  
  HTTP요청이 성공적으로 이루어 졌는지의 상태를 코드로 알려준다.
  
  - 1xx : 요청을 받았으며 프로세스를 계속함

    - 100(Continue): 요청의 시작 부분이 받아졌으며 클라이언트는 계속 이어서 보내야 함
    - 101(Switching Protocol): 요청 헤더의 Update 필드 중 하나로 서버가 프로토콜을 변경함
    - 102(Processing): 서버가 요청을 수신하고 이를 처리하고 있으나 제대로 된 응답을 알려줄 수 없음    
    
  <br/>
  <br/>
  

  - 2xx : 요청을 성공적으로 받았으며 인식하고 수용함
  
    - 200(OK): 요청의 시작 부분이 받아졌으며 클라이언트는 계속 이어서 보내야 함
    - 201(Created): 성공적으로 생성에 대한 요청을 받았으며 서버가 새 리소스를 작성함(POST,PUt 일때)
    - 202(Accepted): 요청을 접수했지만 아직 처리하지 않음    
    - 203(Non-Authoritative Information): 요청을 성공적으로 처리했지만 다른 소스에서 수신된 정보를 제공함, 검증되지 않은 상태
    - 204(No Content): 서버가 요청을 성공적으로 처리했지만 제공할 컨텐츠는 없음
    - 205(Reset Content): 서버가 요청을 성공적으로 처리했지만 새로운 내용을 확인해야 함을 알려줌
    - 206(Partial Content): 서버가 GET 요청의 일부만 성공적으로 처리함
    - 207(Multi Status): 여러 개의 리소스가 여러 status code를 갖고 있는 상황에서 적절한 정보 전달

  <br/>
  <br/>
  
  - 3xx : 클라이언트의 요청에 대해 적절한 위치를 제공하거나 대안의 응답을 제공
  
    - 300(Multiple Choice): 클라이언트가 동시에 여러 응답이 가능한 요청을 보냈을 경우 클라이언트의 선택지를 반환
    - 301(Moved Permanently): 요청한 리소스의 URI가 변경됨 -> 변경된 URI에 대한 정보와 함께 응답
    - 302(Found): 요청한 리소스의 URI가 일시적으로 변경된 것이므로 원래 요청했던 URI로 요청해야 함
    - 303(See Other): 클라이언트가 요청한 작업을 하기 위해서는 다른 URI에서 얻어야 할 떄 클라이언트에게 줌
    - 304(Not Modified): 이전의 요청과 비교하여 달라진 것이 없음(캐시를 목적으로 사용)
    - 305(Use Proxy): proxy를 통해 요청되어야 함
    - 306(Unused): 지금은 사용하지 않는 코드
    - 307(Temporary Redirect): 302와 동일하나 클라이언트가 보낸 HTTP 메소드도 변경하면 안됨
    - 308(Permanent Redirect): 요청한 리소스가 영구적으로 다른 URI에 위치하고 있음, 301과 동일하나 HTTP 메소드도 변경하지 말 것

  <br/>
  <br/>
  
  - 4xx : 클라이언트의 잘못된 요청
    - 400(Bad Request): 잘못된 문법으로 요청을 보내고 있어 서버가 이해할 수 없음
    - 401(Unauthorized): 요청을 위해 권한 인증이 필요함
    - 403(Forbidden): 클라이언트가 요청한 컨텐츠에 대해 접근할 권리가 없음
    - 404(Not Found): 요청한 URI를 찾을 수 없음
    - 405(Method Not Allowed): 클라이언트가 보낸 메소드가 해당 URI에서 지원하지 않음
    - 406(Not Acceptable): 클라이언트의 요청에 대해 응답할만한 컨텐츠가 없음
    - 407(Proxy Authentication Required): 401과 동일하나 proxy를 통해 인증해야 함
    - 408(Request Timeout): 요청에 응답하는 시간이 오래 걸려 요청을 끊음
    - 409(Conflict): 클라이언트의 요청이 서버의 상태와 충돌이 발생할 수 있음
    - 410(Gone): 요청한 URI가 더이상 사용되지 않고 사라짐
    - 411(Length Required): 요청 헤더에 Content-length가 포함되어야 함
    - 412(Precondition Failed): 요청 헤더의 조건이 서버의 조건에 적절하지 않음
    - 413(Payload Too Large): request payload가 너무 길어서 처리할 수 없음
    - 414(URI Too Long): 요청된 URI가 너무 길어서 처리할 수 없음
    - 415(Unsupported Media Type): 서버가 지원하지 않는 미디어 포맷을 요청함
    - 416(Requested Range Not Satisfiable): 요청 헤더에 있는 Range 필드가 잘못됨
    - 417(Expectation Failed): 요청 헤더에 있는 Expect 필드가 적절하지 않음
    - 451(Unavailable For Legal Reasons): 클라이언트가 요청한 것은 정부에 의해 검열된 불법적인 리소스임


  <br/>
  <br/>
  
  - 5xx : 서버 오류
    - 500(Internal Server Error): 서버의 문제로 응답할 수 없음
    - 501(Not Implemented): 서버가 지원하지 않는 새로운 메소드를 사용하여 요청함 클라이언트 요청에 대해 서버가 수행할 수 있는 기능이 없음
    - 502(Bad Gateway): 서버 위의 서버에서 오류가 발생 proxy나 gateway 등에서 응답함
    - 503(Service Unavailable): 현재 서버가 일시적으로 사용이 불가함 일반적으로 유지보수로 인해 중단되거나 과부하가 걸린 서버
    - 504(Gateway Timeout): 서버가 다른 서버로 요청을 보냈으나 delay가 발생하여 처리가 불가능함
    - 505(HTTP Version Not Supported): 서버가 지원하지 않거나 적절하지 않은 프로토콜로 요청을 함
    - 506(Variant Also Negotiates): 서버에 내부 구성 오류가 있음
    - 507(Insufficient Storage): 서버에 내부 구성 오류가 있음
    - 508(Loop Detected): 요청을 처리하는 동안 무한 루프를 감지함
    - 510(Not Extended): 서버가 처리하기 위해서는 요청을 더 확장해야 함
    - 511(Network Authentication Required): 클라이언트가 네트워크 액세스를 얻으려면 인증이 필요함

  <br/>
  <br/>
  
# HTTP 단점

- 암호화 되지 않은 통신이기 때문에 도청이 가능하다.(패킷 강탈)
- 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
- 변조가 가능하다.
