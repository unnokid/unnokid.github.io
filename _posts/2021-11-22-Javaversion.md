---
layout: single
title: "Java 버전별 정리(5~10)"
---

Java 버전들의 추가된 기능과 변해 가는 과정을 정리하려고 한다.

# JDK 5
2004년 9월 30일 발표, 일반 지원은 2009년 9월, 연장 지원은 2015년 5월에 종료되었다.

이때부터 버전 앞부분 1을 빼버리고 표기하기 시작했다. 
<details>
<summary>Generics</summary>
<div markdown="1">
  재네릭은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미한다.
  
  ### 제네릭의 장점
  - 형변환이 필요없고, 타입안정성이 보장된다.
  - 코드의 재사용성이 높아진다.
  
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
<summary>Annotation</summary>
<div markdown="1">
  데이터 유효성 검사등을 쉽게 알 수 있고 관련 코드를 깔끔하게 나타낼 수 있다.
  
  
  ### 주요 Annotation 종류
  
  - @Override
  
  선언한 메서드가 오버라이드 되었다는 것을 나타낸다.
  
  만약 상위(부모) 클래스(또는 인터페이스)에서 해당 메서드를 찾을 수 없다면 컴파일 에러를 발생시킨다.
  
  - @Deprecated
  
  해당 메서드가 더 이상 사용되지 않음을 표시한다.
  
  만약 사용할 경우 컴파일 경고를 발생 시킨다.
  
  - @SuppressWarnings
  
  선언한 곳의 컴파일 경고를 무시하도록 한다.
  
  - @SafeVarargs
  
  Java 7 부터 지원하며 제네릭 같은 가변인자의 매개변수를 사용할 때의 경고를 무시한다.
  
  - @FunctionalInterface
  
  Java 8 부터 지원하며 함수형 인터페이스를 지정하는 Annotation이다.
  
  만약 메서드가 존재하지 않거나 1개 이상의 메서드(default 메서드 제외)가 존재할 경우 컴파일 오류를 발생시킨다. 

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
    System.out.println((i+1)+"번째"+arr[i]);                               
                                 
  }                    
  ```

   현재 인덱스가 중요하지 않고 그냥 값만 도출할 때 향상된 for(임시변수 : 반복할 대상)을 사용하면 좀 더 간결하게 표현이 가능하다.
        
  ```
  int[] arr = {1,2,3};
  for(int i : arr){
    System.out.println(i);                               
                                 
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
        System.out.println(PI);
        System.out.println(cos(0,0));
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
              System.out.println(type.getName());
          }
      }
  }
  ```
</div>
</details>
  
# JDK 6
  2006년 12월 11일 발표, 일반 지원은 2013년 2월에 종료되었으며, 연장 지원은 2018년 12월에 종료되었다. 
  
  이때부터 표기가 J2SE에서 Java SE로 바뀌었다.

<details>
<summary>JDBC 4.0</summary>
<div markdown="1">
  자바에서 데이터베이스 JDBC 4.0이 업데이트 되었다.
</div>
</details>
  
<details>
<summary>Scripting Language Support</summary>
<div markdown="1">
  자바에서 다른 스크립트 엔진을 가져와서 실행 가능하게 만들어준다.
</div>
</details>
  
<details>
<summary>pluggable annotation</summary>
<div markdown="1">
  annotation을 이용해서 클래스 수준 주석, 메서드 수준 주석을 나타낼 수 있다.
</div>
</details>
  
  
  
  
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
  
  32비트를 지원하는 마지막 공식 Java 버전으로, 이후 버전의 32비트 지원은 오직 서드파티를 통해서만 지원된다.
  > 서드파티란? 하드웨어나 소프트웨어 등의 제품을 제조하고 있는 주요 기업이나 그 계열회사 또는 기술 제휴를 하고 있는 기업이 아닌 제 3자 기업
  
<details>
<summary>Lambde 표현식</summary>
<div markdown="1">
  
  모든걸 컴파일러의 추론에 의지하고 코드로 표현하는건 다 줄여서 코드를 간결하게 만드는 것이다.
  
  람다 표현식으로 구현이 가능한 인터페이스는 오직 추상 메서드가 1개뿐인 인터페이스만 가능하며 그렇기 때문에 추상 메서드가 1개인 인터페이스를 부르는 명칭이 추가됬다.

  ```
  //예시
  interface Movable{
      void move(String str);
  }
  
  class Car implements Movable{
      @Override
      public void move(String str){
          System.out.println("gogo car move" + str);
      }
  }
  ```
  
  ```
  Movable movable = new Movable(){
      @Override
      public void move(String str){
          System.out.println("gogo move move" + str);
      }
  }
  
  ```
  Movable 인터페이스를 구현하고있다. 따로 클래스를 만들어 객체화하거나 재사용성이 없다면 그자리에서 바로 익명클래스 객체를 구현하는게 기존방식이다.
  
  여기서 재사용을 위해서 클래스를 남겨두고 익명 클래스부분을 람다표현식으로 수정하고싶다면
 
  - 대상타입을 앞에서 명시에 했기에 new 부분은 없어도 컴파일러가 추론가능하다.
  - 구현할 메서드가 move() 1개만 있기에 메서드명칭을 명시하지않아도 무엇을 구현했는지 알 수 있다.
  - 컴파일러가 인터페이스와 메서드를 추론했다면 인자도 추론할 수 있다. 구현할때 인자는 사용하니 타입까지는 명시하지않는다.
  
  ```
  Movable movable1 = (str) -> {
      System.out.println("gogo move move" + str);
  };
  
  //인자가 하나이고 실행구문이 1줄이라면 중괄호와 괄호도 생략할 수 있다.
  Movable movable2 = str -> System.out.println("gogo move move" + str);
  ```
  
 
</div>
</details>
  
  
<details>
<summary>Default Method</summary>
<div markdown="1">
  인터페이스는 메소드 정의만 할 수 있었고 구현을 할 수 없었지만 Jdk 8부터 Defalut method라는 개념이 생겨서 구현 내용도 인터페이스에 포함 시킬 수 있다.
  
  
  ```
  public interface Vehicle{
      public void doSomething(int n);
  }
  ```
 
  Default Method를 사용하면 구현내용도 인터페이스에 포함시킬 수 있다. 아래 예시처럼 메소드앞에 `default` 키워드를 입력하고 구현내용을 추가하면 된다.
  
  ```
  public interface Vehicle{
      public default void doSomething(int n){
          System.out.println("doSomething(Vehicle)");
      }
  }
  ```
  
  디폴트 메소드가 구현된 인터페이스도 상속받을 수 있다. 클래스가 디폴트 메소드가 정의된 인터페이스를 implements 하면 자동으로 구현이 된다.
  
  >추상 클래스 vs 인터페이스
  - 추상클래스, 인터페이스 둘다 객체로 만들 수 없다. extends하거나 implements 해야한다.
  - 추상클래스는 public, protected, private 메소드를 가질 수 있지만 인터페이스는 public만 허용된다.
  - 추상클래스에는 멤버변수 선언이 가능하지만 인터페이스는 public static 변수만 선언이 가능하다.
  - 인터페이스는 implements 키워드로 여러 인터페이스를 구현할 수 있지만 추상클래스는 extends 키워드로 1개의 클래스만 상속받을 수 있다.
  
</div>
</details>

  
<details>
<summary>함수형 인터페이스</summary>
<div markdown="1">
  함수형 인터페이스(Functional interface)는 1개의 추상 메소드를 갖고 있는 인터페이스를 말한다.
  
  Single Abstract Method(SAM)라고 불린다.
  
  추상메서드가 하나이면 조건을 만족한다. 다른 static 메서드나 default메서드가 추가적으로 있어도 추상 메서드가 하나라면, 함수형 인터페이스라고 할 수 있다.
  ```
  //추상메서드가 하나인 인터페이스 형태이다
  public interface FunctionalInterface{
      void doSomething();
  }
  
  //추상 메서드가 2개 이상인 인터페이스는 함수형 인터페이스가 아니다.
  public interface FunctionalInterface{
      void doSomething();
  
      void doSomething2();
  }
  
  ```
  
  자바의 람다식은 함수형 인터페이스로만 접근이 됩니다.
  
  @FunctionalInterface 어노테이션의 활용이 가능하다. 함수형 인터페이스가 아닌경우, 컴파일 에러를 발생 시켜준다고 한다.

  추상메서드가 1개인 인터페이스가 인스턴스 필드가 존재하는 클래스가 있을 수있다.
  
  ```
  Movable movable = new Movable(){
      private int speed;
  
      @Override
      public void move(){
          System.out.println("gogo move move current speed : "+ speed);
      }
  }
  ```
  메서드와 함수의 가장 큰차이는 함수는 인풋에 의해서만 아웃풋이 달라야 하지만 메서드는 객체에 종속되어있어 인풋이 달라지지않아도 객체의 상태에 따라 결과값이 다를 수 있다.
  
  따라서 람다 표현식으로 구현할때 객체는 상태를 가질 수 없다.
  
  
  ### 함수형 인터페이스 종류
  
  - Runnable
    기존부터 존재하던 인터페이스로 스레드를 생성할 때 주로 사용하였으며 가장 기본적인 함수형 인터페이스다. void 타입의 인자없는 메서드를 갖고있다.
  
  ```
  Runnable r = () -> System.out.println("짬뽕");
  r.run();
  ```
  
  - Supplier<T>
    인자는 받지않으며 리턴타입만 존재하는 메서드를 갖고있다. 순수함수에서 결과를 바꾸는건 오직 인풋뿐이다. 그런데 인풋이 없다는건 내부에서 랜덤함수같은것을     쓰는게 아닌 항상 같은 것을 리턴하는 메서드라는 것을 알 수 있다.
  
  ```
  Supplier<String> s = () -> "hello 짬뽕";
  String result = s. get();
  
  ```
  
  - Consumer<T>
    리턴을 하지않고(void), 인자를 받는 메서드를 갖고있다. 인자를 받아서 소모한다는 뜻으로 인터페이스 명칭으로 이해하면 된다.
  
  ```
  Consumer<String> c = str -> System.out.println(str);
  c.accept("hello 짬뽕");
  ```
  
  - Function<T , R>
    인터페이스 명칭에서부터 알 수 있는 것처럼 전형적인 함수를 지원한다고 보면 된다. 하나의 인자와 리턴타입을 가지며 그걸 제네릭으로 지정해 줄 수 있다.
  
    그래서 타입 파라미터(Type Parameter)가 2개이다.
  
  ```
  Function<String, Integer> f = str -> Integer.parseInt(str);
  Integer result = f.apply("1");
  ```
  
  - Predicate<T>
    하나의 인자와 리턴타입을 가진다. Function과 비슷해 보이지만 리턴타입을 지정하는 타입 파라미터가 안보인다. 반환타입은 boolean으로 고정되어있다.
  
  Function<T,Boolean> 형태라고 생각하면 된다.
  
  ```
  Predicate<String> p = str -> str.isEmpty();
  boolean result = p.test("hello");
  ```
 - UnaryOperator<T>
   하나의 인자와 리턴타입을 가진다. 그런데 제네릭의 타입파라미터가 1개인것은 인자와 리턴타입의 타입이 같다는 것이다.
  
  ```
  UnaryOperator<String> u = str -> str +"operator";
  String result = u.aplly("hello unary");
  ```
  
  - BinaryOperator<T>
    동일한 타입의 인자 2개와 인자와 같은 타입의 리턴타입을 가진다.
  
  ```
  BinaryOperator<String> b = (str1, str2) -> str1 +" " +"str2";
  String result = b.apply("hello", "짬뽕");
  ```
  
  - BiPreficate<T, U>
    서로 다른 타입의 2개의 인자를 받아 boolean 타입으로 반환한다.
  
  ```
  BiPreicate<String, Integer> bp = (str,num) -> str.equals(Integer,toString(num));
  boolean result = bp.test("1",1);
  ```
  
  - BiConsumer<T,U>
    서로 다른 타입의 2개의 인자를 받아 소모한다.(리턴없음)
  
  ```
  BiConsumer<String, Integer> bc = (str, num) -> System.out.println(str+ "::" + num);
  bc.accept("숫자", 5);
  ```
  
  - BiFunction<T,U,R>
    서로다른 타입의 2개의 인자를 받아 또 다른 타입으로 반환한다.
  
  ```
  BiFunction<Integer,String,String> bf = (num,str) -> String.ValueOf(num) + str;
  String result = bf.apply(5,"678");
  ```
  
  -Comparator<T>
    자바의 전통적인 인터페이스 중 하나이다. 객체간 우선순위를 비교할 때 사용하는 인터페이스인데 전통적으로 1회성 구현을 많이하는 인터페이스이다.
    람다의 등장으로 Comparator의 구현이 매우 간결해져 Comparable 인터페이스의 실효성이 많이 떨어진듯 하다.
  
  ```
  Comparator<String> c = (str1,str2) -> str1.compareTo(str2);
  int result = c.compare("aaa","bbb");
  ```
  
</div>
</details>


<details>
<summary>Stream</summary>
<div markdown="1">
  자바의 자료구조들을 선언적으로 다루는 역할을 한다. 컬렉션, 배열등에 대해 저장되어있는 요소들을 하나씩 참조하며 반복적인 처리를 가능하게 해주는 기능이다.
  
  불필요한 for문과 그안에서 이루어지는 if문등 분기처리를 쓰지않고 깔끔하고 직관적인 코드로 변형 할 수 있다.
  
  ```
  int[] numberArr = {1,2,3,4,5,6};
  List<Integer> numberList = Arrays.asList(1,2,3,4,5,6);
  Set<Integer> numberSet = new HashSet<>(numberList);
  
  Arrays.stream(numberArr);
  Stream.of(1,2,3,4,5,6);
  numberList.stream();
  numberSet.stream();
  ```
  컬렉션은 자료구조들의 구현체고 스트림은 자료구조들을 다루는 역할이라고 생각하면 된다.
  
  ```
  //Collection
  List<Integer> numbers = Arrays.asList(1,2,3,4,5,6);
  List<Integer> evenList = new ArrayList<>();
  
  for(int number: numbers){
    if(number %2==0){
      evenList.add(number);
    }
  }
  ```
  
  ```
  //Stream
  List<Integer> evenList = Stream.iterate(1,n -> n+1)
      .limit(6)
      .filter(number -> number % 2==0)
      .collect(toList());
  ```
  Stream을 사용한 코드는 계속해서 도트 연산자로 메서드 체이닝을 일으킨다. 메서드가 반환하는 어떤 객체가 도트 뒤에 나오는 메서드를 갖고있다고 생각해야 한다.
  
  스트림은 중간 연산과 최종연산으로 만들어져있으며 최종연산이 수행되어야 중간 연산들도 모두 수행되어진다.
  
  ### 중간연산 종류
  -Stream<R> map(Function<A, R>)
  -Stream<T> filter(Predicate<T>)
  -Stream<T> peek(Consumer<T>)

  ### 최종연산 종류
  -R collect(Collector)
  -void forEach(Consumer<T>)
  -Optional<T> reduce(BinaryOperator<T>)
  -boolean allMatch(Predicate<T>)
  -boolean anyMath(Predicate<T>)  
  
</div>
</details>


<details>
<summary>Optional</summary>
<div markdown="1">
  반복적인 null 체크를 없애기 위해서 Optional<T> 라는 클래스가 추가되었다.
  
  실제 레퍼런스를 한번 감싸는 래퍼 객체를 만들어 null 체크를 내부로 숨겼기에 외부코드에선 null체크가 보이지않게 감춘 것이다.
  
  ```
  public static void main(String args[]){
      String str ="hello";
      Optional <String> o1 = Optional.of(str); // str이 null이면 NPE발생
      Optional <String> o2 = Optional.ofNullable(str); // str이 null이면 빈 Optional 객체반환
      Optional <String> o3 = Optional.empty(); // 빈 Optional 객체 반환
  {
  
  ### Optional API
  
  - boolean isPresent()
    내부객체가 null이 아닌지 확인한다. null이면 false반환한다.
  
  - void ifPresent(Consumer<T>)
    Consumer<T>는 함수형 인터페이스에서 나온 것처럼 void 추상메서드를 갖고 있다. null이 아닐때만 실행된다.
  
  - Optional<T> filter(Preficate<T>)
    스트림은 여러 데이터를 들고 있는 객체이다보니 filter로 걸러지는 데이터들이 반환되었지만 Optional은 내부객체가 단일객체인만큼 해당 조건을 만족하는지만 확인하는 정도로 사용할 수 있다.
  
  - Optional<U> map(Function<T,U>)
    스트림과 같다. 내부 객체를 변환하는 용도로 사용한다.
  
  - T get()
    내부 객체를 반환한다. 다만 내부 객체가 null이면 NPE가 발생한다. null이 아니라는 확실한 경우에만 사용을 해야한다.
  
  - T orElse(T)
    내부 객체를 반환한다. 내부 객체가 null이면 인자로 들어간 기본값을 반환한다.
  
  -T orElseGet(Supplier<T>)
    orElse()와 동일한데 orElse()가 기본값 레퍼런스를 인자로 받는다면 orElseGet()은 내부 객체가 null일때 기본값을 반환할 객체를 인자로 받는다.
  
  -T orElseThrow(Supplier<U>)
    내부 객체가 null이면 인자로 전달받은 예외를 발생시킨다.
  ```
</div>
</details>
  
<details>
<summary>날짜 관련 클래스 추가</summary>
<div markdown="1">
  전 버전에는 Date 와 Calender 클래스가 제공되었고 불편하다는 의견이 많았다. jdk 8부터 LocalDateTime 과 ZonedDateTime을 제공해준다.
  
  - 불편 객체가 아님
  - int 상수 필드의 남용
  - 헷갈리는 월 지정
  - 일관성 없는 요일 상수
  - 오류에 둔감한 timezone id 지정
  - java.util.Date 의 하위 클래스 문제
  
  ```
  //우리가 사용하는 달력 그대로 나타낼 수 있음
  LocalDate curDate = LocalDate.now(); // 2021-11-22
  LocalDate TargetDate = LocalDate.of(2021,11,22);//2021-11-22
  ```
  
  ```
  //시간 클래스이고 매우 직관적임
  LocalTime curTime = LocalTime.now();//23:58분
  LocalTime targetTime = LocalTime.of(23,57,30);//23:57:30 nano시간까지 적용가능
  ```
  
  ```
  LocalDateTime curDateTime = LocalDateTime.now();
  LocalDate curDate = LocalDate.now();
  LocalTime curTime = LocalTime.now();
  LocalDateTime targetDateTime = LocalDateTime.of(curDate,curTime);
  
  //서로 동일함
  System.out.println(curDateTime);
  System.out.println(targetDateTime);
  ```
  
  ```
  //LocalDateTime -> String 변환
  System.out.println(curDateTime.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")));
  ```
</div>
</details>

  
<details>
<summary>병렬 배열 정렬</summary>
<div markdown="1">
  Arrays.parallelSort()는 MultiThread로 동작하기 때문에 일반적인 Arrays.sort()보다 빠르다.
  
  배열을 둘로 계속 쪼개며 합치면서 정렬하는 알고리즘을 가진다.
  
</div>
</details>
  
<details>
<summary>String Joiner</summary>
<div markdown="1">
StringJoiner는 여러 문자들을 연결할 때 붙일 구분자를 지정해줄 수 있는게 특징이다.
  
  
  ```
  String first = "짬뽕";
  String second = "짜장면";
  String third = "탕수육";
  String fourth = "깐풍기";
  
  //1-2-3-4를 나타내고싶다면
  //String, Operator 사용
  String menu = first + "-" + second + "-" + third + "-" + fourth;
  
  
  //Stringbuffer 사용
  StringBuffer sb = new StringBuffer();
  sb.append(first);
  sb.append("-");
  sb.append(second);
  sb.append("-");
  sb.append(third);
  sb.append("-");
  sb.append(fourth);
  String menu = sb.toString();
  //StringJoiner
  StringJoiner sj = new StringJoiner("-");
  sj.add(first);
  sj.add(second);
  sj.add(third);
  sj.add(fourth);
  String menu = sj.toString();
  ```
  
  StringJoiner는 prefix와 suffix도 붙여줄 수있습니다 
  ```
  //[짬뽕-짜장면-탕수육-깐풍기]
  StringJoiner sj = new StringJoiner("-","[","]");
  sj.add(first);
  sj.add(second);
  sj.add(third);
  sj.add(fourth);
  String menu = sj.toString();
  ```
  
  Stream을 이용해서 쉽게 사용도 가능하다.
  
  ```
  List<String> food = Arrays.asList(first,second,third,fourth);
  String menu = food.stream().collect(Collectors.joining("-","[","]"));
  ```
</div>
</details>
  
  
# JdK 9
  2017년 9월 21일 발표. 일반 지원은 2018년 3월에 종료되었다.
  
  Project jigsaw 기반으로 런타임을 모듈화된 것이 가장 큰특징이다. 이에 대부분의 콘솔 프로그램 개발에는 더 이상 AWT나 Swing같은 불필요한 라이브러리를 끌어쓸 필요도 없이 최상위 모듈인 Base만 사용해도 된다. 특정 프로그램에 최적화된 최소 런타임을 제작할 수도 있게 되어 패키징 역시 간편해졌다.
  
  기본 Garbage Collector로 G1(Garbage First)을 사용한다.
  
<details>
<summary>Java Platform Module System(jigsaw) 추가</summary>
<div markdown="1">
유연한 런타임 이미지를 만들기위해 Java 플랫폼을 모듈화 하여 필요한 모듈만으로 경량화된 이미지를 만들 수 있게 되었다.
  
  기존에는 JRE 일부분만 배포가 불가능했지만 Jigsaw를 통하여 원하는 모듈만 모아 런타임 환경 이미지를 만들 수 있게 되었다.
</div>
</details>
  
<details>
<summary>JShell 추가</summary>
<div markdown="1">
javascript(node),파이썬 같은 인터프리터 언어의 shell 환경처럼 바로 코드를 작성하고 결과를 확인 할 수 있는 REPL(Read-Eval-Print-Loop) 도구를 제공한다. 번거롭게 java 파일을 만들고 컴파일해서 결과를 볼 필요 없이 코드를 작성하고 바로 실행하여 결과를 확인할 수 있다.
</div>
</details>
  
  
  
<details>
<summary>Convenience Factory Methods for Collections</summary>
<div markdown="1">
  List, Set, Map 인터페이스에 불변 Collection을 만들 수 있는 편리한 매서드가 생겼다.
  
  ```
  // Before Jdk 9
  List<String> menu = new ArrayList<>();
  menu.add("짬뽕");
  menu.add("짜장면");
  menu.add("탕수육");
  menu = Collections.unmodifiableList(menu);
  
  // In Jdk 9
  List<String> menu = List.of("짬뽕","짜장면","탕수육");// [짬뽕,짜장면,탕수육]
  
  List<String> menu = List.of(); // [] //비어있는 불변 리스트 만들기
  Set<String> fruits = Set.of("Apple","Banana","Cherry");//중복인자를 넘기면 예외가 발생함
  Map<Integer,String> menu = Map.of(1,"짜장면",5,"짬뽕",3,"탕수육");
  Map<Integer,String> menu = Map.ofEntries(Map.entry(1,"짜장면"),Map.entry(5,"짬뽕"),Map.entry(3,"탕수육"));
  ```

</div>
</details>

<details>
<summary>private 구현체 추가</summary>
<div markdown="1">
  java 8에서 defualt method, static method를 제공했지만 
  
  - 특정기능을 처리하는 내부 method인데도 외부에 공개되는 public method로 만들어야 했다.
  - interface를 구현하는 다른 interface 또는 calss가 해당 method에 액세스하거나 상속 할 수 있는 것을 원하지 않는다.
  
  이때 private를 사용한다.

</div>
</details>
  
# JdK 10
  2018년 3월 20일 발표. 일반 지원은 2018년 9월에 종료되었다.
  
<details>
<summary>Local-variable type inference</summary>
<div markdown="1">
  로컬변수를 선언할때 타입추론을 이용하여 명시적으로 타입선언 없이도 변수를 선언할 수 있게 되었다.
  
  컴파일 할때 컴파일러가 value type을 가지고 변수 타입을 추론한다.
  
  다이아몬드 연산자에 아무 타입도 선언해주지 않거나 반복문 안에서 사용되는 var변수의 초깃값을 주지 않으면 Object로 인식한다.
  
  ```
  var list = new ArrayList<Strsing>(); //ArrayList<String>
  var stream = list.stream(); //Stream<String>
  ```
  
  ```
  //주의할 점은 리터럴로 선언할때와 for문 for each구문에서만 사용이 가능하다. 
  for(var value : list){
    System.out.prntln(value);
  }
  
  for(var i=0;i<list.size();i++){
      System.out.prntln(i);
  }

  ```
  
  ```
  //또한 변수에 함수를 담을 수 있다.
  public static void main(String[] args){
    var val = countingStar();
  }
  
  public static List countNumbers(){
    var numbers = List.of(1,2,3,4,5);
    
    for(var number : numbers){
      System.out.printf(number);
    }
    return numbers;
  }
  ```
  
  
</div>
</details>
  
<details>
<summary>Parallel Full GC for G1</summary>
<div markdown="1">
이전 JDK의 G1 GC는 Full GC를 피할 수 있게 설계 되긴했지만 병행 컬렉터 작업에서 충분할 만큼 빠르게 메모리 반환을 하지 못하면 Full GC가 발생한다. 
  
  G1는Mark-Sweep-Compact 알고리즘을 사용했는데 이전까지는 단일 쓰레드로 GC를 수행했다면 이번 버전부터는 병렬로 Mark-Sweep-Compact를 수행한다.
  > [GC 기본 정리](https://unnokid.github.io/GC/)
  
   >Mark-Sweep-Compact 알고리즘 - 살아있는 객체를 식별하고 살아있는것만을 남기고 삭제하며 살아있는 객체를 모아준다.
  
  쓰레드 수는 기본적으로 Young and Mixed Collection의 쓰레드와 동일하고 필요한 경우 옵션으로도 조절이 가능하다.
 
</div>
</details>
  
<details>
<summary>Application Class-Data Sharing</summary>
<div markdown="1">
  기존의 Class-Data Sharing(CDS)기능을 확장해 애플리케이션 크래스를 공유 아카이브에 배치하고 서로 다른 자바 프로세스들이 공유를 할수 있도록 개선함으로 startup 시간을 단축시키고 메모리 사용량을 최적화 시켰다.
  
  여러 대의 JVM이 하나의 물리 장비 또는 가상 장비에서 돌아가는 경우, 자원에 미치는 영향을 줄이기 위해 개발된 기능이다.
</div>
</details>


