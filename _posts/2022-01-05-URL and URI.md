---
layout: single
title: "URL 과 URI 차이점"
---

Spring 공부도중 URL과 URI는 무슨 차이인지 알지 못해서 정리하려고 한다.

<br/>


# URI와 URL

### URI(uniform resource identifier)
인터넷의 우편물 주소같은 의미로 정보 리소스를 고유하게 식별하고 위치를 지정할 수 있다.

### URL(uniform resource locator)

네트워크 상의 자원의 위치를 나타내는 주소이다.

### 예시로 비교

- `https://www.naver.com` 은 네이버 서버를 나타내기에 URL이면서 URI이다
- `https://www.naver.com/images` 는 네이버서버의 images라는 네트워크 상의 자원의 위치를 의미하기에 URL이면 URI이다
- `https://www.naver.com/images/dog.jpeg` 
  
    네이버서버의 images 디렉터리 아래의 dog.jpeg를 기리키므로 URL이면 URI이다
- `https://www.naver.com/user/123`
   
   URL 부분은 user 까지이고 원하는 정보에 도달하기 위한 식별자 123을 포함하면 URI이다.
- `https://www.naver.com/user?id=11` 
    

### 정리
URL은 URI에 포함되는 개념이며 URL은 자원의 위치를 의미한다.

