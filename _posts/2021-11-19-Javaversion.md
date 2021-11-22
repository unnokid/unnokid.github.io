---
layout: single
title: "Java 버젼별 정리(5~17)"
---


# JDK 5
2004년 9월 30일 발표, 일반 지원은 2009년 9월, 연장 지원은 2015년 5월에 종료되었다.

이 버젼부터 버젼이름의 앞부분인 1을 빼버리고 표기하기 시작했다. 
<details>
<summary>Generics</summary>
<div markdown="1">
  JDK 1.4까지 Collection 객체는 모두 Collection에 담긴 객체를 얻을 때 Object 타입으로 리턴을 하기 때문에 반드시 캐스팅이 필요했다.
 
  따라서 ClassCast Exception을 회피해야만 했지만 JDK 5부터는 Collection<자료형> 의 형태로 명시할 수 있다.
  
  >Collection 객체 종류 - List, Set, Map
  
  ```
  List<Integer> numbers = new ArrayList<Integer>();
  numbers.add(1);
  numbers.add(2);
  numbers.add(3);
  ```
</div>
</details>
  
<details>
<summary>Auto boxing / Unboxing</summary>
<div markdown="1">
  자바에서 기본형(short, int, long, float 등)과 래퍼 클래스(Short, Integer, Long) 가 있다.
  
  ```
  int i =1;
  Integer newI = new Ingeter(i);//boxing
  int j = newI.intValue();//unboxing
  ```
  위 예처럼 기본형과 래퍼 클래스를 변환할 때 매우 번거로움이 많았다.
  
  명시적으로 나타내거나 메서드를 호출하지 않고 바로 할당 할 수 있게 해주는것이 Auto boxing/Unboxing이다.
  
  ```
  int i = new integer(1);//Auto unboxing;
  Integer newI = 10;// Auto boxing;
  ```
</div>
</details>
  
<details>
<summary>향상된 루프</summary>
<div markdown="1">
  반복문의 기본문법은 for(초기식;조건식;증감식)으로 나타낸다.
  
  ```
  int[] arr = {1,2,3};
  for(int i=0; i<arr.length;i++){
    System.out.printf((i+1)+"번째"+arr[i]);                               
                                 
  }                    
  ```

   현재 인덱스가 중요하지 않고 그냥 값만 도출할 때 향상된 for(임시변수 : 반복할 대상)을 사용하면 좀 더 간결하게 표현이 가능하다.
        
  ```
  int[] arr = {1,2,3};
  for(int i : arr){
    System.out.printf(i);                               
                                 
  }                    
  ```                    
</div>
</details>
  
<details>
<summary>static import</summary>
<div markdown="1">
객체에 접근하려면 인스턴스가 필요하지만 static 으로 선언하면 클래스로 직접 접근할 수 있다.
  
  이때 import를 static으로 선언하면 클래스 명없이 해당 클래스에서 import한 클래스에 접근 할 수 있다.
  
  ```
  import static java.lang.Math.*
  
  public class Test{
    public static void main(String[] args){
        System.out.printf(PI);
        System.out.printf(cos(0,0));
    }
  }
  ```
</div>
</details>
  
<details>
<summary>Enums</summary>
<div markdown="1">
  열거형 타입을 제공하는 클래스로 상수방식의(final static) 열거보다 key와 value 형태로 효율적으로 관리 할 수 있다.

  ```
  enum Type{
      COMIC("코믹"),COOKING("요리"),FAIRYTALE("동화")
  
      final private String name;
  
      private Type(String name){
          this.name = name;
      }
      public String getName(){
          return name;
      }
  }
  
  public class Books{
      public static void main(String[] args){
          for(Type type : Type.values()){
              System.out.printf(type.getName());
          }
      }
  }
  ```
</div>
</details>
  
# JDK 6
