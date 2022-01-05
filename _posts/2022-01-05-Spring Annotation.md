---
layout: single
title: "Spring Annotation 정리"
published : false
---

Spring에서 사용되는 에노테이션에 대해 간단하게 정리하려고 한다.

<br/>
<br/>

# Spring Annotation 정리

### @Requestmapping

  URL을 Controller의 메서드와 맵핑할때 사용하는 어노테이션이다.

- @RequestMapping(value="/test1",method ={RequestMethod.GET,RequestMethod.POST})
  
- @RequestMapping("/test1")


<br/>

- @RequestMapping(value="/test1",method ={RequestMethod.GET})

- @GetMapping("/test1")

<br/>

- @RequestMapping(value="/test1",method ={RequestMethod.POST})

- @PostMapping("/test1")


<br/>
<br/>

  하나의 URL로 두개이상의 맵핑을 처리가능하고 그 코드자체만으로 어떤 전송 방식을 처리하는지 확인할 수 있다.

- @GetMapping
  
  GET요청 URL을 처리하는 방식으로 주로 데이터를 조회할 때 사용한다.

<br/>

- @PostMapping

  POST요청 URL을 처리하는 방식으로 데이터의 값을 변경하거나 상태를 바꿀때 사용한다.

<br/>
  
>-----------------
- @Pathvariable

  URL 경로의 일부를 파라미터로 사용할 때 URL  

- @Requestparam

    메소드의 파라미터값으로 @RequestParam으로

- @RequestBody

  함께 받아야하는 데이터가 있다면 이 에노테이션을 활용한다.
  
  HTTP Body에 담긴 데이터를 맵핑해서 가지고온다.

<br/><br/>




- @Autowired

- @Controller

- @Service

- @Repository

- @NoArgsConstructor

- @Configuration

- @Bean

- @SpringBootApplication

@Configuration, @EnableAutoConfiguration, @ComponentScan 3가지를 합친 것이다.

- @Test

- @SpringBootTest

- @Transcational

- @BeforeEach

- @AfterEach

