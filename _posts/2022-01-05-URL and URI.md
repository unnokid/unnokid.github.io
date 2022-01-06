---
layout: single
title: "URL 과 URI 차이점"
---

Spring 공부도중 URL과 URI 용어를 헷갈리는 일이 발생했다.

따라서 간단하게 정리하려고 한다.

<br/>


# URI와 URL

### URI(uniform resource identifier)

자원의 위치뿐만이 아니라 정보 리소스를 고유하게 식별하는 통합 자원 식별자이다.

<br/>

### URL(uniform resource locator)

네트워크 상의 자원의 위치를 나타내는 주소이다.

<br/>
<br/>

### 예시로 비교

- `https://www.naver.com`
  
  네이버 자체 주소를 나타내고 있으므로 URL이자 URI이다.


  
- `https://www.naver.com/images`
  
  마찬가지로 네이버에서 이미지라는 주소경로를 나타내므로 URL이면 URI이다.


- `https://www.naver.com/images/dog.jpeg`

    네이버 images 디렉터리 아래의 dog.jpeg를 주소를 나타내므로 URL이면 URI이다.

  
- `https://www.naver.com/user/123`
   
   URL 부분은 `https://www.naver.com/user` 까지이고 원하는 정보에 도달하기 위한 식별자 `123`을 포함한 전체부분은 URI이다.

  
- `https://www.naver.com/user?id=11` 

  URL 부분은 `https://www.naver.com/user` 까지이고 원하는 정보에 도달하기 위한 식별자 `?id=11`을 포함한 전체부분은 URI이다.
    

### 정리
- URL은 URI에 포함되는 개념이다.(URL⊂URI)
- URL은 자원의 위치를 의미한다.
- URI은 자원의 위치뿐만이 아니라 고유하게 식별하는 통합 자원 식별자이다.

