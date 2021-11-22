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
