---
layout: single
title: "Comparator 와 Comparable 정리"
---


# Comparable 과 Comparator

Steram 정리를 하다가 Comparator를 보게 됬는데 생각해보니 정렬에 할때 자주쓰지만 자세히는 잘 모르고 있다.

객체의 정렬 기준을 명시하는 두 가지 방법으로 Comparable 과 Comparator가 있다.

<br/>
<br/>

### Interface Comparable

정렬 수행 시 기본적으로 적용되는 정렬 기준이 되는 메서드를 정의하는 인터페이스이다.

Java에서 제공되는 정렬이 가능한 클래스(Interger, Double, String)들은 모두 Comparable 인터페이스를 구현하고 있으며 정렬을 할 때 이에 맞게 정렬이 수행된다.

