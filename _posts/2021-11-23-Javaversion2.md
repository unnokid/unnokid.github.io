---
layout: single
title: "Java 버전별 정리(11~15)()"
---
이어서 Java 버전별 정리(11~15)를 하려고 한다.

# JDK 11
2018년 9월 25일 발표. 일반 지원은 2023년 9월, 연장 지원은 2026년 9월에 종료될 예정이다.

이클립스 재단으로 넘어간 Java EE가 Jdk에서 삭제되고 JavaFx도 Jdk에서 분리되어 별도의 모듈로 제공된다.

이번 버전부터 Oracle Jdk의 독점 기능이 오픈 소스 버전인 OpenJDK에 이식되었다. 즉 Oracle JDK와 OpenJDK가 완전히 동일해진다는 뜻이다.
 <details>
<summary>Epsilon과 Z Garbage Collector 추가</summary>
<div markdown="1">

 ### Epsilon
 Epsilon은 메모리 할당은 처리하지만 사용되지 않은 영역에 대해 재활용하지 않는다. 그리고 기존에 다른 알고리즘의 GC들은 Java Heap 영역이 가득찼을경우 OS에 요청하여 추가적으로 Heap 영역을 할당받았는데 Epsilon의 경우 Java Heap 영역을 모두 소진하면 JVM이 down됩니다.
 
 Epsilon의 목적은 제한된 영역의 메모리 할당을 허용함으로써 최대한 lathency overhead를 줄이는 것이다.
 
 어플리케이션이 외부환경으로부터 고립된 채로 실행되기 때문에 실제 내 어플리케이션이 얼마나 메모리를 사용하는지에 대한 임계치나 어플리케이션 퍼포먼스 등을 봐 정확하게 측정할 수 있다.
 
 ### ZGC
 대량 메모리를 적은 대기시간(low-latency)으로 잘 처리하기 위해 디자인 된 GC이다.
 
 Heap Reference를 위해서 Load barrier를 사용한다. Load barrier는 이전 버전에서 사용하던 G1GC보다 딜레이가 낮다.
</div>
</details>

# JDk 12
2019년 3월 19일 공개. 
 <details>
<summary>Switch문 확장</summary>
<div markdown="1">

  ```
  //Before Jdk 12
  switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
  }
 
  //In Jdk12
  switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
    case TUESDAY                -> System.out.println(7);
    case THURSDAY, SATURDAY     -> System.out.println(8);
    case WEDNESDAY              -> System.out.println(9);
  }  
  ```
</div>
</details>

<details>
<summary>Garbage Collector 개선</summary>
<div markdown="1">
  Shenandoah GC가 도입되었다. Jdk 11에서 추가된 ZGC(Z Garbage Collector)와 비슷하게 대량의 메모리 처리에 우수한 퍼포먼스를 내지만 좀더 많은 옵션을 제공한다
  ```
  ```
</div>
</details>

<details>
<summary></summary>
<div markdown="1">

  ```
  ```
</div>
</details>
# JDk 13
2019년 9월 17일 공개. 
<details>
<summary>yield 예약어 추가</summary>
<div markdown="1">
 
  ```
 var a = switch (day) {
    case MONDAY, FRIDAY, SUNDAY:
        yield 6;
    case TUESDAY:
        yield 7;
    case THURSDAY, SATURDAY:
        yield 8;
    case WEDNESDAY:
        yield 9;
};
  ```
</div>
</details>


# JDk 14
2020년 3월 18일 공개.
 <details>
<summary>Instanceof 패턴 매칭</summary>
<div markdown="1">


</div>
</details>



# JDk 15
 <details>
<summary></summary>
<div markdown="1">

  ```
  ```
</div>
</details>




