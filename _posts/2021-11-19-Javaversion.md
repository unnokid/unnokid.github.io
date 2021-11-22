---
layout: single
title: "Java 버젼별 정리(5~17)"
---


# JDK 5
JDK 설명 대충
<details>
<summary>Generics</summary>
<div markdown="1">
  JDK 1.4까지 Collection 객체는 모두 Collection에 담긴 객체를 얻을 때 Object 타입으로 리턴을 하기 때문에 반드시 캐스팅이 필요했다.
 
  따라서 ClassCast Exception을 회피해야만 했지만 JDK 5부터는 Collection<자료형> 의 형태로 명시할 수 있다.
  
  ```
  List<Integer> numbers = new ArrayList<Integer>();
  numbers.add(1);
  numbers.add(2);
  numbers.add(3);
  ```
  

</div>
</details>
