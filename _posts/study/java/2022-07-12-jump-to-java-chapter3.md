---
layout: post
title: 점프 투 자바 3장 연습문제 풀이
image:
  path: /assets/img/thumbnail/java.png
description: >
  자바
sitemap: false
categories:
  - study
  - java

---
# [점프 투 자바] 3장 연습문제 풀이

* toc
{:toc .large-only}

~~~
점프 투 자바 03장 연습문제 개인적 풀이
~~~

## Q1
홍길동 씨의 과목별 점수는 다음과 같다. 홍길동 씨의 평균 점수를 구해 보자.

|과목|점수|
|--|--|
|국어|80|
|영어|75|
|수학|55|

> 풀이

```java
public static void main(String[] args) {
  int[] scores = {80, 75, 55};
  int total = 0;
  for (int value : scores) {
    total += value;
  }
  System.out.println(total/scores.length);
}
```

## Q2
자연수 13이 홀수인지 짝수인지 판별할 수 있는 방법에 대해 말해 보자.

> 풀이

```java
boolean isOdd(int num) {
  if (num % 2 == 1) {
    return true;
  }else {
    return false;
  }
}

public static void main(String[] args) {
  int myNum = 13;

  Sample sample = new Sample();
  boolean verify = sample.isOdd(myNum);

  System.out.println(verify);
}
```

## Q3
홍길동 씨의 주민등록번호는 881120-1068234이다. 홍길동 씨의 주민등록번호를 연월일(YYYYMMDD) 부분과 그 뒤의 숫자 부분으로 나누어 출력해 보자.

>풀이

```java
package org.ssafy.test;

public class Sample {


	public static void main(String[] args) {
		String gildongNum = "881120-1068234";
		String front = gildongNum.substring(0,6);
		String back = gildongNum.substring(7);
		System.out.printf("앞자리 : %s, 뒷자리 : %s", front,back);
	}

}
```

## Q4
주민등록번호 뒷자리의 맨 첫 번째 숫자는 성별을 나타낸다. 주민등록번호에서 성별을 나타내는 숫자를 출력해 보자.

`pin = "881120-1068234"`

>풀이

```java
public static void main(String[] args) {
  String pin = "881120-1068234";
  System.out.println(getSex(pin.substring(7,8)));
}

public static String getSex(String num) {
  if (num.equals("1")) {
    return "male";
  }
  else {
    return "female";
  }
}
```
