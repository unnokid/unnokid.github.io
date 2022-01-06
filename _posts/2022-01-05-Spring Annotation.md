---
layout: single
title: "Spring Annotation 정리(작성중)"
published : false
---

Spring에서 사용되는 에노테이션에 대해 간단하게 정리하려고 한다.

<br/>
<br/>

# Spring Annotation 정리

### @Requestmapping @GetMapping @PostMapping

  URL을 Controller의 메서드와 맵핑할때 사용하는 어노테이션이다.

  아래예시는 서로 같은 의미를 가진 Annotation을 예시로 나열했다.

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

### 왜 둘다 처리할 수 있는 RequestMapping을 안쓰고 Get과 Post로 나누는가?

  하나의 URL로 두개이상의 맵핑을 처리가 가능하고 그 코드자체만으로 어떤 전송 방식을 처리하는지 확인할 수 있다.

- @GetMapping
  
  GET요청 URL을 처리하는 방식으로 주로 데이터를 조회할 때 사용한다.

<br/>

- @PostMapping

  POST요청 URL을 처리하는 방식으로 데이터의 값을 변경하거나 상태를 바꿀때 사용한다.

<br/>
<br/>
  
### @requestparam @requestbody @pathvariable

  Controller에서 파라미터를 받을때 사용하는 어노테이션이다.  


<br/>

- @Pathvariable

  URL 경로의 일부를 파라미터로 사용할 때 쓴다.

```java
@Controller
public class TestController{
  @RequestMapping(values = "users/{id}",method= RequestMethod.GET)
  public String getUser(@PathVariable String userId){
      // Using userId
  }
}
```

<br/>
<br/>

- @RequestParam

    GET방식으로 넘어온 URI의 queryString을 받기위해서 사용한다.

    `http://localhost:8080/api/foos?id=abc`

```java
@Controller
public class TestController{
    @GetMapping("/api/foos")
    public String getFoos(@RequestParam String id){
        // Using Id
    }
}
```

<br/>
<br/>

- @RequestBody

  HTTP 요청 본문에 담긴 body부분을 java 객체로 받을 수 있게 해줘서 사용한다. 주로 json을 받을 때 사용한다.

  받아올 json에 맞는 클래스(UserVO)를 미리 만들어서 자바 객체로 변환한다. 
```java
@Controller
public class TestController{
    @PostMapping("/api/test")
    public String Test(@RequestBody UserVO getUserVO){
        // Using getUserVO
    }
}
```

<br/>
<br/>


### 다음

- @Autowired
  
  필요한 의존 객체의 타입에 해당하는 빈을 찾아 주입한다.
  
  주입방법은 생성자 주입, setter 주입, 필드 주입이 있다.


- @Controller

- @Service

- @Repository

- @NoArgsConstructor

- @Configuration

- @Bean

- @SpringBootApplication

  @Configuration, @EnableAutoConfiguration, @ComponentScan 3가지를 합친 것이다.

<br/>

- @Test

  Test 메서드임을 인식하고 테스트한다.

<br/>

- @SpringBootTest

  스프링부트 어플리케이션 테스트에서 필요한 모든 의존성을 제공한다.

<br/>

- @Transcational

  테스트 부분에서 테스트 완료 후 자동으로 rollback 처리 한다.

<br/>

- @BeforeEach

```java
@BeforeEach
public void beforeEach(){
    System.out.println("@BeforeEach");    
}
```

  이 에노테이션을 붙이면 테스트 메서드 실행 이전에 실행된다.

<br/>

- @AfterEach

```java
@AfterEach
public void AfterEach(){
    System.out.println("@AfterEach");    
}
```

  이 에노테이션을 붙이면 테스트 메서드 실행 이후에 실행된다.