---
layout: single
title: "Redirect 와Forwarding 차이점"
---

Redirect와 Forwarding은 JSP 환경에서 다른 페이지로 이동하는 페이지 전환 기능이다.

하지만 둘이 차이점을 정확히 설명할 수 없기에 정리하려고 한다.

<br/>



# 포워딩(Forwarding)


<img src= "https://user-images.githubusercontent.com/58356031/156950954-957847a4-6b2a-4575-abd0-e19116f70ac7.png" width="400">



- 웹 컨테이너 차원에서 페이지 이동을 의미

- 클라이언트에게 알리지않고 서버의 다른 자원에게 요청이 전달 됨

- 따라서 Request와 Response 객체를 공유 함


<br/>
<br/>


# 리다이렉트(Redirect)


<img src= "https://user-images.githubusercontent.com/58356031/156951106-82277fcf-4929-456f-958d-c0b2fa6ecac8.png" width="400">



- 클라이언트 요청을 처리한 후 sendRedirect() 라는 메서드가 호출되면 웹 컨테이너가 웹 브라우저에게 새로운 URL을 주며 이동하라고 함  

- 클라이언트는 다시 새로운 URL로 요청을 만들어 보냄

- 따라서 첫 요청과 새로운 요청은 서로 다름(전 요청의 객체는 소멸하고 새로 만들어짐)


<br/>
<br/>

# 차이점 정리

- 리다이렉트는 URL가 바뀌고 포워딩은 바뀌지 않음

- 리다이렉트는 Request와 Response 객체가 서로 같고 포워딩은 서로 다름

- 리다이렉트는 클라이언트가 다른페이지로 이동했는지 알 수 있고 포워딩은 서버에서 넘기는 것으로 알 수 없음

- 성능은 포워딩이 리다이렉트 보다 좋음(리다이렉트 < 포워딩)
