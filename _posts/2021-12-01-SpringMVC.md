---
layout: single
title: "Spring MVC, Security 동작원리와 처리 흐름 정리(작성중)"
---

나사장이 추천한 사이트에 대해 필요한 지식이라고 생각해서 나름대로 간단히 정리하려고 한다.

참고) https://aaronryu.github.io/2021/02/14/a-tutorial-for-spring-mvc-and-security/

<br/>
<br/>


# Web Server 와 Web Application

### Web Server(static 페이지)

Web Server는 정적인 문서를 서버에서 저장하고 유저가 요청하면 해당 파일을 유저의 브라우저에 다운받아 보여주는 형식

예) Apache, Nginx

요청처리
- 유저는 웹 서버에게 특정 페이지(index.html)을 요청함
- 웹 서버는 index.html을 검색 후, 있다면 유저에게 반환함

<br/>
<br/>

### Web Application(dynamic 페이지)

Javascript의 등장으로 유저와의 인터렉션을 통해 양방향의 서비스에 대한 요구사항이 생겨났다.

일반적인 어플리케이션처럼 데이터베이스와의 연결도 필요하고, 동적 페이지 렌더링이 필요해졌고
서버에 있는 자원만 반환하는게 아닌 요청받은 시점에 알맞은 자원(페이지)를 만들어서 반환해야 된다.

따라서 웹 서버와 프로그램 사이를 연결해주는 방식(CGI: Common Gateway Interface)가 여러 언어로 개발되어 있다.

그중 Java에서는 Web Server 요청/반환과 Java Application 사이를 연결해 주는 Servelet 객체가 등장한다.

Servlet은 유저의 요청 하나마다 하나씩 생성되기 때문에 여러 요청에 따른 Servlet 자원 관리가 필요해졌고 이 역할을 하는것이 바로 **Web Container**이며 
Servlet Container라고 부르기도 한다.

유저의 요청/반환을 관할하는 **Web Server** + 요청에 따른 적합한 Java Application 구동을 위한 Servlet 관리자 **Web Container** 둘을 합쳐서
**Web Application** 이라고 부른다.

예) tomcat

<br/>
<br/>


용어에 대해 몇가지 정리를 해야한다.

### ServletContext(Web Container)

Servlet 객체 주기 관리를 위한 웹 컨테이너 에 해당되고 관리라는 의미로 Context를 사용한다.

모든 요청에 대한 Servlet 생명주기는 이 ServletContext가 모두 관리한다.
<br/>
<br/>


### ServletContextListener

Servlet 객체 주기 관리를 위한 웹 컨테이너 `ServletContext` 최초 구동시(Listener) 수행할 작업을 정의한다.

<br/>
<br/>

### web.xml(Deployment Description)

웹 컨테이너 구동시, Servlet을 위한 2가지 설정을 한다.
- ServletContextListener 인터페이스 구현체(어떤 것을 실행할지)
- 어떤 요청에 어떤 타입의 Servlet객체를 생성할지


<br/>
<br/>


최초 구동시
- tomcat 웹 어플리케이션이 최초 구동시 가장 먼저 웹 컨테이너(ServletContext)를 구동합니다.
- ServletContext 구동 시 web.xml 에 설정한 ServletContextListener 를 같이 수행합니다.

요청처리
- 유저는 웹 서버에게 특정 페이지(index.html)을 요청함
- 웹 서버는 index.html을 검색 후, 존재하지 않기 때문에 웹 컨테이너(ServletContext)에게 요청을 이관한다.
- ServletContext는 web.xml에서 index.html 요청에 맞는 타입의 Servlet을 생성한다.
- 생성된 Servlet은 유저가 요청한 페이지를 동적으로 생성하여 유저에게 반환 후 파기된다.

<br/>
<br/>


# Spring MVC Framework



