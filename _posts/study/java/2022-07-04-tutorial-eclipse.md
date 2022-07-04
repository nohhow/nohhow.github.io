---
layout: post
title: Eclipse 살펴보기
image:
  path: /assets/img/thumbnail/javascript.png
description: >
  자바
sitemap: false
categories:
  - study
  - javascript

---
# Eclipse 살펴보기

* toc
{:toc .large-only}

~~~
이 포스트는 2013년에 업로드된 생활코딩의 Java 강의를 기반으로 생각을 정리하는 글입니다.
~~~


Eclipse IDE에서의 각 View 들은 가변적이기에 원하는 곳에 위치하게 할 수 있다.
- Package Explorer : 프로젝트 관리 도구
- Outline : 소스코드가 있으면 해당 소스코드의 문법적 요소들을 시각적으로 표시해서 어떤 명령어, 요소들로 구성되어있는지 확인할 수 있다.
- Problems : 소스코드에 문제가 있다면 표
- Console : 결과가 출력되는 곳
- Editor : 코드를 작성하는 공간


## 새로운 프로젝트 생성

Create a Java Project를 통해서 새롭게 프로젝트 생성
그럼 다음과 같은 폴더 구조를 가진다.

~~~
java-tutorial
 +- bin (실행파일 .class)
 +- src (소스코드 .java)
~~~

.java 확장자로 작성한 파일은 저장할 때 자동으로 컴파일러에 의해서 .class 확장자의 파일로 컴파일 된다.

> **소스코드 > 프로그램**
.java 파일 > Save > .class 파일 > Run

### Package 생성
하나의 디렉토리 내부에 같은 이름을 가진 파일이 둘 이상 존재할 수 없다. 같은 이름의 파일을 공존할 수 있도록 하기 위해서 Package도 이와 같은 맥락에서 사용된다.
더 깊은 이야기가 있지만 나중에 배우기로.

> **Package Name**은 통상 **도메인 주소**를 사용한다.
ex) org.opentutorials.javatutorials.eclipse
각 .은 구분자 역할을 하며 디렉토리로 생성된다.

### 새로운 자바 클래스 생성
`New > class`

클래스 생성 창은 별 다른 기능을 가진 것이 아니라, .java 파일을 생성할 때 기본이 되는 부분들을 쉽게 작성할 수 있도록 도와주는 역할을 한다고 이해하면 된다.

<img width="578" alt="스크린샷 2022-07-04 오후 1 43 20" src="https://user-images.githubusercontent.com/61059893/177082938-a45d52dd-9d67-439c-8548-5c3152d658de.png">

* 파일명을 helloWorld라고 짓고
* public static void main(String[] args)를 체크해준다. (기본 뼈대를 만들어주는 역할) ~~사진 상에서 체크가 안 되어있는데 해준다.~~ 다음 소스코드에 주석 부분이 자동 생성 된다.


```java
package org.ssafy.javatutorial.eclipse;

public class Helloworld {

  // 해당 부분 체크하면 여기 부분이 자동생성 되는 것이다.
	public static void main(String[] args) {
		// TODO Auto-generated method stub
    // 실행하고자 하는 코드 작성
	}

}
```

### MacOS에서 Content Assist 단축키 설정하기
Window에서 Eclipse로 Java 코딩을 할 때, `sysout`을 작성하고 ctrl + space를 누르면 `	System.out.println();`를 자동완성 해주던 기억이 나는데, Mac에서는 반응이 없었다.

그래서 `Preference > keys > content assist > binding : option + space`로 변경해주었더니 잘 된다.
