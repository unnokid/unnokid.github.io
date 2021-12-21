---
layout: single
title: "HTTP와 HTTPS 차이점 정리(작성중)"
---

HTTP와 HTTPS 차이를 정리하려고 한다

# HTTP 란

HTTP(Hyper Text Transfer Protocol)로 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜이다.

80번 포트를 사용하며 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며 클라이언트는 80번 포트로 요청을 보내게 된다.

Stateless와 Connectionless 의 특징을 가진다

### HTTP 구조

<img src= "https://user-images.githubusercontent.com/58356031/146863335-eae94fce-8a18-47c3-8906-f85b633c6476.png" width="500">

- Start line(시작라인)

- Header(헤더)

- Empty line(공백라인)

- Message body(메시지 본문)

