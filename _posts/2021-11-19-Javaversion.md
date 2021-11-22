---
layout: single
title: "Java 버젼별 정리(5~17)"
---

Java 버전들의 추가된 기능과 변해 가는 과정을 정리하려고 한다.

# JDK 5
2004년 9월 30일 발표, 일반 지원은 2009년 9월, 연장 지원은 2015년 5월에 종료되었다.

이때부터 버전 앞부분 1을 빼버리고 표기하기 시작했다. 
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
  2006년 12월 11일 발표, 일반 지원은 2013년 2월에 종료되었으며, 연장 지원은 2018년 12월에 종료되었다. 
  
  이때부터 표기가 J2SE에서 Java SE로 바뀌었다.
  
  
  
  
  
# JDK 7
  2011년 7월 7일 발표, 일반 지원은 2015년 4월에 종료되었으며, 연장 지원은 2022년 7월에 종료될 예정이다. 
<details>
<summary>Diamond Operato</summary>
<div markdown="1">
  Jdk 5에서 추가된 Generics는 Collection의 자료형을 명시해 주는 기능이였다. 
  
  Jdk 7부터는 왼쪽에 선언한 것을 바탕으로 컴파일러가 타입을 추측할 수 있도록 지원했다.
  
  따라서 다음과 같이 작성이 가능해졌다.
  
  ```
  //Before Jdk 7
  ArrayList<Integer> arr = new ArrayList<Integer>();
  
  //In Jdk 7
  ArrayList<Integer> arr = new ArrayList<>();
  ```
</div>
</details>
  
<details>
<summary>Using strings in switch statements</summary>
<div markdown="1">
Switch 문은 Primitive 자료형이나 Enumerated 자료형을 사용할 수 있었지만 Jdk 7 부터는 Switch 문에 String 자료형을 사용할 수 있게 되었다.
  
  ```
  //Before Jdk 7
  private void processTrade(Trage t){
    String status = t.getStatus();
    if(status.equalsIgnoreCase(NEW)){
      newTrade(t);
    }
    else if(status.equalsIgnoreCase(EXECUTE)){
      executeTrade(t);
    }
    else if(status.equalsIgnoreCase(PENDING)){
       pendingTrade(t)' 
    }
  }
  
  //In Jdk 7
  public void processTrade(Trade t){
    String status = t.getStatus();
    switch(status){
      case NEW: newTrade(t);break;
      case EXECUTE: executeTrade(t);break;
      case PENDINg: pendingTrade(t);break;
      defalut: break;
    }
  }
  ```
</div>
</details>

  
<details>
<summary>Automatic resource management</summary>
<div markdown="1">
  개발자는 사용한 리소스를 .close()를 사용하여 수동으로 회수해야 했다.
  
  Jdk 7 부터는 Try 문 안에 리소스를 선언하면 자동으로 리소스를 관리한다. 리소스가 여러 개면 세미콜론(;)으로 구분하여 선언 할 수 있다.
  
  ```
  //Before Jdk 7
  static String readFirstLineFromFile(String path) throws IOException{
    BufferedReader br = new BufferedReader(new FileReader(path));
    try{
      return br.readLine();
    }finally{
      if(br != null) br.close();
    }
  }
  
  //In Jdk 7
  static String readFirstLineFromFile(String path) throws IOException{
    try(BufferReader br = new BufferedReader(new FileReader(path))){
      retrun br.readLine();
    }
  }
  ```
  finally 에서 close하는 부분을 쓰지 않아도 된다.
</div>
</details>
  
  
<details>
<summary>Improved exception handling</summary>
<div markdown="1">
 Multi-catch 기능은 예외처리를 하기 위해 과도한 블록 생성을 하지 않는 방법이다.

  ```
   // Before Jdk 7
  public void oldMultiCatch() {
    try {
      methodThatThrowsThreeExceptions();
    } 
    catch (ExceptionOne e) {
    } 
    catch (ExceptionTwo e) {
    } 
    catch (ExceptionThree e) {
    }
  }

  // In Jdk 7
  public void newMultiCatch() {
    try {
      methodThatThrowsThreeExceptions();
    } 
    catch (ExceptionOne | ExceptionTwo | ExceptionThree e) {
    }
  }
  ```
  
  만약 다른 타입에 속하는 여러가지 예외가 있다면 Multi Multi-catch 블록을 이용 할 수 있다.
  
  ```
  public void newMultiMultiCatch(){
    try{
      methodThatThrowsThreeExceptions();
    }
    catch (ExceptionOne e) {
    }
    catch (ExceptionTwo | ExceptionThree e) {
    }
  }
  ```
</div>
</details>
  
<details>
<summary>Underscore in Numeric literal</summary>
<div markdown="1">
  숫자형(정수,실수)에 _문자열을 사용 할 수 있다. 큰 숫자들을 다룰때 가독성이 향상될 수 있도록 도와준다.
  
  ```
  int money = 1_000_000_000;
  long cardnumber = 1234_5678_8901_1234L;
  double pi = 3.1415_9265;
  float pif = 3.14_15_92_65f;
  ```
  
  - 소숫점 뒤에 _ 를 붙인 경우
  - 숫자 끝에 _ 를 붙인 경우
  - 숫자 시작에 _ 를 붙인 경우
  
  위 3가지 경우에 컴파일 에러가 발생할 수 있다.
</div>
</details>
    
<details>
<summary>More Precise Rethrowing of Exception</summary>
<div markdown="1">
  try 내부에 다양한 Exception이 발생 할 수 있지만 catch 구문내에서 선언한 예외 유형만 던질 수 있었다.(throws)
  
  하지만 Jdk 7 부터는 조금 더 정확한 Exception을 전달 할 수 있다.

  ```
  // Before Jdk 7
public void obscure() throws Exception {
    try {
        new FileInputStream("abc.txt").read();
        new SimpleDateFormat("ddMMyyyy").parse("12-03-2014");
    } catch (Exception ex) {
        System.out.println("Caught exception: " + ex.getMessage());
        throw ex;
    }
}

// In Jdk 7
public void precise() throws ParseException, IOException {
    try {
        new FileInputStream("abc.txt").read();
        new SimpleDateFormat("ddMMyyyy").parse("12-03-2014");
    } catch (Exception ex) {
        System.out.println("Caught exception: " + ex.getMessage());
        throw ex;
    }
}
  ```
</div>
</details>

<details>
<summary>Java NIO 2.0</summary>
<div markdown="1">
java.nio.file 패키지가 추가되었다.
  
  전에는 꽤나 길고 복잡한 파일 코드를 사용했어야 했지만 간단하게 기본 시스템 파일에 접근이 가능하고 다양한 파일I/O기능을 제공하는 등 외부라이브러리로 해결했던 많은 일들이 JDK API로 추가되었다.
  
  
</div>
</details>

  
# JDK 8
  
  2014년 3월 18일 발표, 일반 지원은 2019년 1월에 종료되었고, 연장 지원은 2023년 9월에 종료될 예정이다.
  
<details>
<summary>Lambde 표현식</summary>
<div markdown="1">

  ```
  ```
</div>
</details>
  
  
<details>
<summary>Default Method</summary>
<div markdown="1">
intefrace 안에 구현된 메소드를 추가해야 할 때 default 키워드를 붙여준다.
  
  하위 호환성을 위해서 이미 많은 사람이 사용하고 있는 인터페이스에 새로운 메소드를 추가해야 할 때 기존 방식대로 추가하면 이미 사용하고 있는 사람들은 전부 오류가 발생하고 수정해야하는 일이 발생한다. 이럴 때 사용 할 수 있다.
  ```
  ```
</div>
</details>

  
<details>
<summary>함수형 인터페이스</summary>
<div markdown="1">

  ```
  ```
</div>
</details>


<details>
<summary>Stream</summary>
<div markdown="1">

  ```
  ```
</div>
</details>


<details>
<summary>Optional</summary>
<div markdown="1">

  ```
  ```
</div>
</details>
  
<details>
<summary>날짜 관련 클래스 추가</summary>
<div markdown="1">

  ```
  ```
</div>
</details>

  
<details>
<summary>병렬 배열 정렬</summary>
<div markdown="1">

  ```
  ```
</div>
</details>
  
<details>
<summary>String Joiner</summary>
<div markdown="1">

  ```
  ```
</div>
</details>
