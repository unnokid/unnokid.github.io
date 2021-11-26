---
layout: single
title: "Comparator 와 Comparable 정리"
---


# Comparable 과 Comparator

Steram 정리를 하다가 Comparator를 보게 됐는데 생각해 보니 정렬을 할 때 자주 사용되지만 자세히는 잘 모르고 있다.

사용자가 정의한 정렬 기준에 맞춰 정렬해야 하는 경우가 있다.
- ex) 좌표를 x좌표가 증가하는 순, x좌표가 같다면 y좌표가 감소하는 순으로 정렬
- ex) 국어 점수는 증가하는 순, 수학 점수는 감소하는 순으로 정렬


객체의 정렬 기준을 명시하는 두 가지 방법으로 Comparable 과 Comparator가 있다.

<br/>
<br/>

### Interface Comparable

정렬 수행 시 기본적으로 적용되는 정렬 기준이 되는 메소드를 정의하는 인터페이스이다.

Java에서 제공되는 정렬이 가능한 클래스(Interger, Double, String)들은 모두 Comparable 인터페이스를 구현하고 있으며 정렬을 할 때 이에 맞게 정렬이 수행된다.

```java
//package: java.lang.Comparable
//Integer, Double 클래스는 오름차순 정렬
//String 클래스는 사전 순으로 정렬
public final class Integer extends Number implements Comparable<Integer>{...}
public final class String implements java.io.Serializable, Comparable<String>,CharSequence{...}
```

정렬할 객체에 Comparable interface를 implemets 후, compareTo() 메소드를 오버라이드하여 구현한다.

<br/>
<br/>

compareTo() 메소드는 
 - 현재 객체 < 파라미터로 넘어온 객체 : 음수 리턴
 - 현재 객체 == 파라미터로 넘어온 객체 : 0 리턴
 - 현재 객체 > 파라미터로 넘어온 객체 : 양수 리턴
 - 음수 or 0 이면 객체의 자리가 그대로 유지되며 양수인 경우에는 두 객체의 자리가 바뀐다.

```java
//x좌표가 증가하는 순, x좌표가 같으면 y좌표가 감소하는 순으로 정렬
class Point implements Comparable<Point>{
    int x, y;
    
    @Override
    public int compareTo(Point p){
        if(this.x > p.x){
          return 1; //x에는 오름차순
        }
        else if(this.x == p.x){
            if(this.y < p.y){
                return 1;
            }
        }
        return -1;
    }
}

List<Point> pointList = new ArrayList<>();
pointList.add(new Point(x,y));
Collection.sort(pointList);
```


사용 예시
- Arrays.sort(array)
- Collections.sort(list)

<br/>
<br/>

#### Arrays.sort() 와 Collections.sort() 차이가 헷갈려서 정리해야 한다.
    
#### 1. Arrays.sort()
      
 - Object[], T[]등 Object Array에서는 TimSort(Merge sort + Insertion Sort)를 사용한다.

```java
//Object[] 예시
public static void sort(Object[] a){
  if(LegacyMergeSort.userRequested){
    lagacyMergeSort(a)
  }
  else{
    ComparableTimeSort.sort(a, 0, a.length,null,0,0 );
  }
}
```
TimSort는 부분적으로 정렬되어 있을 때 더욱 효과적이다.

<br/>
<br/>

 - byte[], char[], double[], int[] 등에 대한 배열 Primitive Array에서는 Dual Pivot QuickSort(Quick Sort + Insertion Sort)를 사용 한다.
> Primitive Array : 기본 자료형에 대한 배열

```java
//int[] 예시
public static void sort(int[] a){
  DualPivotQuicksort.sort(a,0,a.length-1,null,0 ,0);
}
``` 

<br/>
<br/>

#### 2. Collections.sort()

List Collection 정렬의 경우 사용되고 ArrayList, LinkedList, Vector 등 내부적으로 Arrays.sort()를 사용한다.

Collections.sort에 들어가보면 list.sort를 사용하고 list.sort에서는 Arrays.sort를 호출한다.

<br/>
<br/>
<br/>


### Interface Comparator

정렬 가능한 클래스(Comparable 인터페이스를 구현한 클래스)들의 기본 정렬 기준과 다르게 정렬하고 싶을 때 사용하는 인터페이스이다.

주로 **익명 클래스**로 사용되고 기본적인 정렬 방법인 오름차순 정렬을 내림차순으로 정렬할 때 많이 사용한다.

Comparator interface를 implements 후 compare() 메소드를 오버라이드한 myComparator class를 작성한다.

<br/>
<br/>


compare()메소드는 
 - 첫 번째 파라미터로 넘어온 객체 < 두 번째 파라미터로 넘어온 객체 : 음수 리턴
 - 첫 번째 파라미터로 넘어온 객체 == 두 번째 파라미터로 넘어온 객체 : 0 리턴
 - 첫 번째 파라미터로 넘어온 객체 > 두 번째 파라미터로 넘어온 객체 : 양수 리턴
 - 음수 or 0 이면 객체의 자리가 그대로 유지되며 양수인 경우에는 두 객체의 자리가 바뀐다.

오름차순 일 때는 Integer.compare(x, y) 내림차순 일때는 Integer.compare(y,x); 

```java
//x좌표가 증가하는 순, x좌표가 같은면 y좌표가 감소하는 순으로 정렬
Comparator<Point> myComparator = new Comparator<Point>(){
    @Override
    public int compare(Point p1, Point p2){
        if(p1.x > p2.x){
            return 1;
        }
        else if(p1.x == p2.x){
            if(p1.y <p2.y){
                return 1;
            }
        }
        return -1;
    }
};

List<Point> pointList = new ArrayList<>();
pointList.add(new Point(x,y));
Collections.sort(pointList, myComparator);
```
<br/>
<br/>

사용 예시
- Arrays.sort(array,myComparator)
- Collections.sort(list,myComparator)
