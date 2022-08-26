---
layout: single
title: "Spring MVC, Security 동작원리와 처리 흐름 정리(작성중)"
published: false
---

추천받은 사이트에 대해 정리가 잘 되어있고 필요한 지식이라고 생각해서 간단히 정리하려고 한다.

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

Java Servlet을 활용한 웹 어플리케이션 개발이 활성화되면서 여러 디자인 패턴들을 적용하여 Java 웹 개발을 더 쉽게 도와주는 Spring Framework가 등장하게 되었다. 초기에는 페이지를 동적으로 렌더링하기 위해 각 요청마다 Servlet을 할당하여 요청을 처리했다면 Spring은 각 요청마다 Servlet보다 작은 단위인 Bean을 할당하여 요청을 처리한다.

- 요청을 처리하는 단위가 Servlet이라면 Servlet 관리를 위한 Servlet Container
- 요청을 처리하는 단위가 Bean이라면 Bean 관리를 위한 Bean Container가 필요합니다.(Bean Container = Spring Container)

<br/>
<br/>

Spring은 기본적으로 MVC 모델로 Model, View, Controller 세 그룹의 역할로 분리 개발을 돕는 프레임워크이기에 아무리 디자인 패턴에 지식이 부족하더라도 유지보수성, 재사용성이 뛰어난 웹 어플리케이션을 만들 수 있다.

또한 데이터베이스 접근을 위한 JPA, 트랜잭션, 보안 등 웹 어플리케이션에서 필요로하는 모든것을 Bean 설정으로 제공하기 때문에 어떤 초보자여도 탄탄한 이해만 바탕이 된다면 손쉽게 만들 수 있다.

<br/>
<br/>

# Spring + Web Application

Spring MVC 동작 과정을 쉽게 이해하기 위해서는 MVC 와 Front Controller 패턴을 알면 됩니다.


<br/>
<br/>

### MVC

Model, View, Controller로써 유저의 요청을 효율적으로 처리하기 위한 모델입니다. 

유저가 어떤 페이지를 요청하면

1. 요청에 적합한 Controller 가 요청을 받아서
2. 요청 페이지에 필요로 하는 정보인 Model을 조회/생성하고
3. 조회/생성한 Model을 통해 최종 페이지인 View를 생성하여 유저에게 반환하는 모델

<br/>
<br/>

### Front Controller 패턴

요청을 받는 부분이 Controller라고 했는데 tomcat은 요청을 Servlet 이라는 Controller에서 처리하고, Spring은 요청을 Bean 이라는 Controller에서 처리한다.

2-레벨 Controller의 의미는 (1) 맨 앞의 tomcat이 모든 요청을 단일 Servlet으로 먼저 받아서 요청 URL이 무엇인지에 따라
(2)Spring의 Controller Bean에 재할당해주게 됩니다.

가장 앞의 (1)tomcat 단일 Servlet을 `요청을 가장 앞에서 먼저 받는다`는 의미로 Front Controller라고 부르고, 그뒤(2) Spring Controller Bean을 실제 페이지 생성에 사용된다는 의미에서 Page Controller라고 부른다.

<br/>
<br/>

# Spring MVC의 요청/처리 흐름

<!-- 그림에 대한 공간이 필요함 -->

tomcat 에 Spring을 연결하여 사용하려면 tomcat 설정파일인 web.xml 에 2가지 설정이 필요하다.

web.xml(Deployment Description)
- ServletContextListener 인터페이스 구현체 - Root WebApplicationContext -> Spring 공용 Bean(@Service,@Repository,@Component...)객체들을 미리 생성해 놓기 위함

-모든 요청은 Front Controller 에 해당하는 단일 Servlet 객체(DispatcherServlet)가 처리한다.

<br/>
<br/>

최초 구동시

- tomcat 웹 어플리케이션이 최초 구동시 가장 먼저 웹 컨테이너(ServletContext)를 구동한다.
- ServletContext 구동시 web.xml에 설정한 Spring Root WebApplicationContext가 동시에 구동된다.

<br/>
<br/>

요청 처리시

위 최초 구동 후 tomcat은 모든 요청을 단일 Servlet(DispatcherServlet)으로 받을 준비가 완료되었고 Spring 도 Controller Bean이 결과를 반환하기 위해 필요로하는 모든 Bean들이 Root WebApplicationContext로 준비가 완료된다. 


Spring의 키워드는 Ioc, DI라고 할 수 있는데 간단하게 설명하면 기존에는 개발자가 new를 통해서 객체를 직접 생성하고 주입했다면
Spring에서는 어떤 인터페이스, 클래스를 사용할것인지만 표기해놓으면 ApplicationContext(BeanFactory 상속)라고 불리는 Spinrg Container가 객체를 Bean이라는 단위로 알아서 생성하고 알아서 주입해주는 개념이다. 이렇게 Spring에서는 Java의 모든 객체를 Bean이라고 부르며 사용한다.

> Spring Container = ApplicationContext

Spring에서 Bean은 웹 어플리케이션 관점에서 크게 2개의 타입으로 구분 될 수 있다.

그에 따라 Bean의 생명주기를 관리하는 Spring Container도 2개의 타입으로 나뉘어진다.

- 요청이 들어왔을 때 적합한 처리를 위해 요청과 상관없이 모든 Servlet들이 공유하는 공용 Bean
  - 예: @ComponentScan으로 등록된 @Service, @Repository, @Component 등
  - 생명주기 관리: Spring Container 1(Root WebApplicationContext)
- 요청이 들어왔을 때 할당되는 Servlet처럼 요청이 들어왔을 때만 생성하면 되는 Bean
  - 예: @ComponentScan으로 등록된 @Controller, @Interceptor 등
  - 생명주기 관리: Spring Container 2(Servlet WebApplicationContext)


최초 구동시에 생성된 Spring Container 1 아래에 또 하나의 Spring Container 2가 생긴걸 볼 수 있다.

Parent와 Child라고 써있는 두 컨테이너 간에 계층이 있다는 의미이며 단순히 child인 Servlet WebApplicationContext 의 Bean들은 부모인 Root WebApplicationContext의 Bean들을 참조할 수 있지만 그 반대로는 참조할 수 없음을 의미한다.

Root WebApplicationContext이 모든 Servlet들이 공유하는 Bean 생명주기를 관리하는 것이라고 생각하면 된다.


























