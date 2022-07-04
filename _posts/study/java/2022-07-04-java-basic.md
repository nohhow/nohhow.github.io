---
layout: post
title: Java 기초 문법
image:
  path: /assets/img/thumbnail/java.png
description: >
  자바
sitemap: false
categories:
  - study
  - java

---
# Java 기초 문법

* toc
{:toc .large-only}

~~~
이 포스트는 2013년에 업로드된 생활코딩의 Java 강의를 기반으로 생각을 정리하는 글입니다.
~~~
## 변수

변수(Variable)은 앞서 살펴본 (문자와 숫자 같은) 데이터를 담는 컨테이너 이다. 여기에 담겨진 데이터는 다른 데이터로 바꿀 수 있다.

### 변수 선언과 할당

```java
int age;
age = 26;
System.out.println("next year age : " + (age+1));
```

* 변수 선언
  * `int age;` 에서 int는 데이터타입을 명시하는 것이고, age는 변수명이다.
* 변수 할당
  * `age = 26;` age 변수에 26 값을 저장함

---

## 주석

주석은 로직에 대한 설명이나 코드를 비활성화 할 때 사용.
주석은 프로그래밍적으로 해석되지 않는다.

* 한 줄 주석 : `// 내용`
* 여러 줄 주석 : `/* 내용 */`
* JavaDoc 주석(자바의 문서 만들 때 사용) : `/** 내용 */`
~~~
/**
 *
 * 이 사이에 주석을 작성
 *
 */
~~~

---

## 데이터타입 (자료형)

### 숫자 Number
  * 정수

  | 데이터 타입 | 메모리의 크기 | 표현 가능 범위 |
  |--|--|--|
  |byte|1byte|-128 ~ 127|
  |short|2byte|-32,768 ~ 32,767|
  |int|4byte|-2,147,483,648~2,147,483,647|
  |long|8byte|-9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807|

  정수형 저장 시 int를 주로 사용하게 되는데, CPU 처리속도가 빠르고 충분히 큰 수를 표현할 수 있기에 자주 사용하게 된다.

  * 실수 (double)

  | 데이터 타입 | 메모리의 크기 | 표현 가능 범위 |
  |--|--|--|
  |float|4byte|	±(1.40129846432481707e-45 ~ 3.40282346638528860e+38)|
|double|8byte|±(4.94065645841246544e-324d ~ 1.79769313486231570e+308d)|

실수형 저장 시에는 주로 double을 사용한다.

### 상수와 데이터 타입
변수는 변하는 값, 상수는 변하지 않는 값이다.
`int a = 1;`에서 1이 상수이다.

변수를 만들 때 데이터타입을 지정하게 되는데, 상수에도 데이터타입이 있음을 이해해야한다.

#### 실수 표현

```java
float a = 2.2;
```
위 예제는 다음과 같은 에러가 발생한다.
"Type mismatch: cannot convert from double to float"
=> 2.2는 float형이 아니라는 뜻.

double형인 2.2를 float 변수에 저장하기 위해서는 다음과 같이 작성한다.

```java
float a = 2.2F;
```

#### 정수 표현

데이터 타입이 정수인 상수는 어떤 데이터 타입을 가지느냐?
int이다.

int가 담을 수 있는 값을 넘어서는 2147483648도 int 데이터 타입을 가지기 때문에 `long a = 2147483648;`은 에러가 발생한다. float과 마찬가지로 long 데이터 타입임을 명시하는 L을 붙여줘서 데이터 타입을 명시해준다.

```java
long a = 2147483648L;
```
> **byte와 short은 어떨까?**
byte와 short 데이터타입의 경우에는 int형을 허용하기 때문에 long과 다르게 에러가 발생하지 않는다.

### 형변환

컴퓨터는 데이터타입에 따라서 200이라는 숫자와 200.0이라는 숫자, 즉 정수형의 값과 실수형의 실제 값이 일치하더라도 값을 다르게 인식하고 표현한다.

> **int 타입 정수의 bit 표현**
00000000 00000000 00000000 11001000

> **float 타입 정수의 bit 표현**
01000011 01001000 00000000 00000000

이처럼 형식이 다른 값 끼리는 덧셈과 같은 연산도 불가능하다. 그래서 데이터 형을 변환하는 **'형변환'**을 해서 데이터타입을 일치시켜줄 필요가 있다.

자바는 이러한 형 변환을 자동으로 처리해주기도 하는데, 이를 자동(암시적) 형 변환이라고 한다.

#### 암시적 형변환
`double a = 3.0F;`는 float형의 수 3.0이 double로 형 변환된다. double이 float보다 더 많은 수를 표현할 수 있기 때문에 가능한 일이다.
> 자동 형 변환은 표현범위가 좁은 데이터 타입에서 넓은 데이터 타입으로의 변환만 허용된다.

다음과 같이 char => int로의 변환도 가능(유니코드 값)

```java
char a = 'A'; //유니코드 65
int b = 1;
System.out.println(a+b); // 66
```

#### 명시적 형변환

다음은 float형 변수에 double형 상수를, int형 변수에 float형 상수를 넣으려는 시도를 하고 있다.

```java
float a = 100.0;
int b = 100.0F;
```
당연히 에러가 발생하는데, 암시적 형 변환이 이뤄지지 않기 때문이다. 덧셈과 같은 연산을 할 떄에는 암시적 형 변환이 이뤄졌던 것과 달리 여기서는 명시적 형 변환을 해줘야한다.

```java
float a = (float)100.0;
int b = (int)100.0F;
```

### 문자와 문자열 Character & String
  * 문자 char
    * **한 글자**를 의미
    * 문자는 작은 따옴표로 감싸서 구분함.

    | 데이터 타입 | 메모리의 크기 | 표현 가능 범위 |
    |--|--|--|
    |char|2byte|모든 유니코드 문자|

  * 문자열 string
    * **문자와 문자가 결합된 형태**
    * 문자열은 큰 따옴표로 감싸서 구분함.
    * 문자열의 메모리 크기는 글자수에 따라서 결정(각 글자당 2byte) - 6글자면 12byte 공간 차지
  > 단, 한 글자도 문자열이 될 수 있기 때문에 한 글자에 큰 따옴표 가능.

  > **문자 하나가 1byte가 아니라 2byte인 이유?**

  ```java
  String str = "안녕하세요.";
  System.out.println(str.length());
  ```
  위 예시에서 문자열의 길이를 출력했을때 `6`이 출력되지만 실제로 메모리 크기는 12byte이다. 이는 각 글자(char) 하나가 인코딩 방식이 유니코드 이기 때문에 1byte가 아닌 2byte의 크기를 가지기 때문이다.

```java
public class CharString {

	public static void main(String[] args) {
		System.out.println('노');
		System.out.println('노진현'); // 에러발생
		System.out.println("노");
		System.out.println("노진현");
	}
}
```

* 문자 + 문자열 간에 덧셈 연산자로 연결 가능
`System.out.println('노' + "진현");`

* 이스케이프
약속되어있는 특수한 기호를 일반적인 문자로 사용하고 싶은 경우에는 이스케이프 기호를 사용해야한다. java에서는 이스케이프를 위해서 `\`를 사용한다. `\`다음에 오는 기호는 문법적인 역할에서 도망(이스케이프)쳐서 문자로 인식된다.

---

## 연산자

### 대입 연산자
* =, +=, -=, *=. /=, %=

### 산술 연산자
* \+ , -, *, /, %

#### 단항 연산자
* +(양수표현), -(음수표현), ++, --
++, -- 증감 연산자는 앞에 오냐 뒤에오냐에 따라서 연산 순서가 바뀜.


### 비교 연산자
* ==, !=, >, >=, <, <=
  * 결과는 true 또는 false 이다.
  * <mark>비교하고자 하는 대상의 주소값을 비교</mark>
* .equals (메서드)
  * <mark>비교하고자 하는 내용 자체를 비교</mark>
  * 문자와 문자를 비교할 때 사용.
  * 다음과 같은 상황을 극복하고자 사용.

  ```java
  public static void main(String[] args) {
    String a = "Hello world";
    String b = new String("Hello world");
    System.out.println(a == b); //false
    System.out.println(a.equals(b)); //true
  }
  ```
  a와 b에 저장된 문자열이 같은 주소값을 가지고 있는 것이 아니기 때문에 주소값을 통해서 값을 비교하는 `==` 연산자에서는 false가 출력되고 값 내용 자체를 비교하는 `.equals` 메서드에서는 true가 출력된다.

### 논리 연산자
* &&(and), ||(or), !(not)

---

## 반복문

### for문

~~~
for(초기화; 종료조건; 반복실행){
    반복적으로 실행될 구문
}
~~~

```java
for (int i = 1; i < 366; i++) {
    System.out.println("Coding Everyday " + i);
}
```

### while 문

~~~
while(조건){
    반복 실행 영역
}
~~~
조건이 `참(true)`인 동안에 실행

```java
int i = 1
while (i < 366) {
    System.out.println("Coding Everyday " + i);
    i++
}
```

---

## 배열

배열은 연관된 데이터를 모아서 관리하기 위해서 사용하는 데이터 타입이다.

### 배열의 생성

```java
public static void main(String[] args) {

    String[] classGroup = { "최진혁", "최유빈", "한이람", "이고잉" };
}
```

```java
public static void main(String[] args) {
    String[] classGroup = new String[4];
    classGroup[0] = "최진혁";
    System.out.println(classGroup.length); //4
    classGroup[1] = "최유빈";
    System.out.println(classGroup.length); //4
    classGroup[2] = "한이람";
    System.out.println(classGroup.length); //4
    classGroup[3] = "이고잉";
    System.out.println(classGroup.length); //4

}
```

`new String[4]`는 4개의 원소를 저장하는 배열을 선언한 것.
index 4까지를 저장하는게 아님.


### 배열 제어

* index를 통해서 각 데이터에 접근 가능.
* 배열의 길이는 .length 메서드 이용. = <mark>현재 값이 담겨있는 갯수가 아니라 값이 담길 수 있는 갯수를 반환</mark>

### for each : for문을 좀 더 간편하게

* for 문
```java
public static void main(String[] args) {
    String[] members = { "최진혁", "최유빈", "한이람" };
    for (int i = 0; i < member.length; i++) {
        String member = members[i]
        System.out.println(member + "이 상담을 받았습니다");
    }
}
```

for문에서 반복적으로 사용하는 부분을 간소화하여
for each문이 탄생했다.
멈춤 조건이나 증감을 따로 설정하지 않고 배열에 순차 접근하여 값을 꺼낼 수 있다.

* for each 문
```java
public static void main(String[] args) {
    String[] members = { "최진혁", "최유빈", "한이람" };
    for (String e : members) {
        System.out.println(e + "이 상담을 받았습니다");
    }
}
```

`String e : members` members 배열의 값을 변수 e에 담아서 중괄호 구간 안으로 전달한다. 종료 조건이나 증감연산에 대해서는 은닉되어 있다. => 실수를 줄일 수 있겠지.

### 배열의 한계

Javascript나 Python은 유연하게 배열에 값을 추가할 수 있는데, java 같은 경우는 배열을 초기화할 때 그 크기가 정해지며 정해진 크기 이상의 값을 넣을 수 없다.
단, 자바에는 컬렉션 Collection이라는 기능이 있고, Container라고 부르는 이 기능을 이용하면 Javascript의 배열과 같이 유연하게 사용할 수 있다. 이 부분은 추후에 배우게 될 것.

---
