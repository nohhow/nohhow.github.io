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

## Q5
다음과 같은 문자열 `a:b:c:d`가 있다. 문자열의 replace 함수를 사용하여 `a#b#c#d`로 바꿔서 출력해 보자.


```java
public class Q5 {

	public static void main(String[] args) {

		String a = "a:b:c:d";		
		System.out.println(a.replace(":", "#"));
	}

}
```

## Q6
다음과 같은 [1, 3, 5, 4, 2] 리스트를 [5, 4, 3, 2, 1]로 만들어 보자.

```java
package jumpToJava;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;

public class Q6 {
    public static void main(String[] args) {
        ArrayList<Integer> myList = new ArrayList<>(Arrays.asList(1, 3, 5, 4, 2));

        Collections.sort(myList, Collections.reverseOrder());
        System.out.println(myList);
    }
}
```

## Q7
다음과 같은 ['Life', 'is', 'too', 'short'] 리스트를 "Life is too short" 문자열로 만들어 출력해 보자.

```java
package jumpToJava;

import java.util.ArrayList;
import java.util.Arrays;

public class Q7 {
    public static void main(String[] args) {
        ArrayList<String> myList = new ArrayList<>(Arrays.asList("Life", "is", "too", "short"));

		String str = String.join(" ", myList);
		System.out.println(str);
    }
}
```

## Q8
다음의 맵 grade에서 "B'에 해당되는 값을 추출해 보자. (추출하고 나면 grade에는 "B"에 해당하는 아이템이 사라져야 한다.)

```java
package jumpToJava;

import java.util.HashMap;

public class Q8 {
    public static void main(String[] args) {
        HashMap<String, Integer> grade = new HashMap<>();
        grade.put("A", 90);
        grade.put("B", 80);
        grade.put("C", 70);

        System.out.println(grade.remove("B"));  // "B"의 값 출력
        System.out.println(grade.toString()); // {A=90, C=70}
    }
}
```

## Q9
다음의 numbers 리스트에서 중복 숫자를 제거해 보자.

```java
package jumpToJava;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;

public class Q9 {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<>(Arrays.asList(1, 1, 1, 2, 2, 3, 3, 3, 4, 4, 5));
        HashSet<Integer> set = new HashSet<>(numbers);
        System.out.println(set);
    }
}
```

## Q10
다음은 커피의 종류(1: 아메리카노, 2:아이스 아메리카노, 3:카페라떼)를 입력하면 커피의 가격을 알려주는 프로그램이다.

> **개선 전**
```java
package jumpToJava;

import java.util.HashMap;

public class Q10 {
    static void printCoffeePrice(int type) {
        HashMap<Integer, Integer> priceMap = new HashMap<>();
        priceMap.put(1, 3000);  // 1: 아메리카노
        priceMap.put(2, 4000);  // 2: 아이스 아메리카노
        priceMap.put(3, 5000);  // 3: 카페라떼
        int price = priceMap.get(type);
        System.out.println(String.format("가격은 %d원 입니다.", price));
    }

    public static void main(String[] args) {
        printCoffeePrice(1);  // "가격은 3000원 입니다." 출력
        printCoffeePrice(99);  // NullPointerException 발생
    }
}
```

> **개선 후** (Enum)

```java
package jumpToJava;

import java.util.HashMap;

public class Q10 {
	enum CoffeeType {
		AMERICANO,
		ICE_AMERICANO,
		CAFE_LATTE
	};


    static void printCoffeePrice(CoffeeType type) {
        HashMap<CoffeeType, Integer> priceMap = new HashMap<>();
        priceMap.put(CoffeeType.AMERICANO, 3000);  
        priceMap.put(CoffeeType.ICE_AMERICANO, 4000);          
        priceMap.put(CoffeeType.CAFE_LATTE, 5000);          
        int price = priceMap.get(type);
        System.out.println(String.format("가격은 %d원 입니다.", price));
    }

    public static void main(String[] args) {
        printCoffeePrice(CoffeeType.CAFE_LATTE);  // "가격은 5000원 입니다." 출력
    }
}
```
-> 엉뚱한 숫자값에 의한 오류가 발생하지 않는다.
-> 매직넘버를 사용할 대보다 코드가 명확해 진다.
