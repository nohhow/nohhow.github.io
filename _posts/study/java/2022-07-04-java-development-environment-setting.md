---
layout: post
title: Java 개발 환경 설정
image:
  path: /assets/img/thumbnail/java.png
description: >
  자바
sitemap: false
categories:
  - study
  - java

---
# Java 개발 환경 설정

* toc
{:toc .large-only}

~~~
교육, 테스트 환경에 맞게 다음 버전으로 환경 설정
- jdk 8
- eclipse 2018-09
~~~

## 개요

JDK (Java Development Kit)만 설치하면 java 코드 파일을 컴파일하고 실행할 수 있다. 하지만 개발 편의와 협업 등의 이유로 IDE를 사용하게 되는데 여기서는 Eclipse를 설치한다.

본인의 경우 교육 기관에서 Java 학습 및 프로젝트를 하게 된 상황이고, 이에 따라 jdk 8, eclipse 2018-09 버전 설치가 권장되었다.

## JDK 설치

기존에 설치된 JDK가 있는지, 버전이 맞는지 확인하고
없거나, 버전이 다르면 설치 진행

`javac -version`
`java -version`

* 기대하는 버전 : java version "1.8.0_333"
* 현재 버전 : java version "14.0.1" 2020-04-14

본인은 Window PC 같은 경우 초기화를 진행해서 JDK가 설치되어 있지 않았고, 맥북은 JDK 14가 설치되어 있는 상태였다.
이 상황에서 어떻게 설치를 진행했는지 작성해본다.

### Window

* 설치 링크 : https://cdn.azul.com/zulu/bin/zulu8.33.0.1-jdk8.0.192-win_x64.msi

* 환경 변수 설정
  * 제어판 > 시스템 환경변수 편집 > 고급 > 환경 변수
  * 변수추가
    * 변수 이름 : JAVA_HOME
    * 변수값 : C:\Program Files\Zulu\zulu-8
  * path(변수) 경로 추가
    * %JAVA_HOME%\bin
  * classpath 추가
    * 변수 이름 : classpath
    * 변수 값 : .
* 설정 확인
`javac -version`
`java -version`


```
javac 1.8.0_192
openjdk version "1.8.0_192"
```
이렇게 나오면 OK

### macOS

mac에서는 우선 기존에 설치된 JDK를 삭제해줬다.

일반적으로 jdk 경로는 다음과 같다.
`/Library/Java/JavaVirtualMachines/`

```
$ cd /Library/Java/JavaVirtualMachines/
$ ls
```
이 때 설치하고자 하는 버전과 다른 버전을 삭제 해준다.
본인의 경우 jdk14.0.1 파일을 삭제했다.

삭제 명령은
```
$ sudo rm -rf jdk14.0.1.jdk
```

설치는 Window에 설치한 것과 같은 버전의 zulu-8를 설치했다.
* 설치 링크 : https://cdn.azul.com/zulu/bin/zulu8.33.0.1-jdk8.0.192-macosx_x64.dmg

그리고 환경변수 PATH 설정을 해줘야하는데
macOS에서는 주로 bash 쉘을 사용하는데 본인의 경우 zsh를 사용하고 있기 때문에 zshrc에 환경 변수 설정을 해줬다.

```
$ vi ~/.zshrc
```
```
// .zshrc
export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contetens/Home
export PATH=${PATH}:$JAVA_HOME/bin
```

## Eclipse 설치

Window와 macOS 상관없이 Eclipse 설치 링크를 통해서 각 OS에 맞는 파일 설치 진행

### eclipse 설치 후 환경설정

* Eclipse encoding 설정 : xml, html, css, json, workspace (utf-8로 설정)
* Open perspective : default JAVA EE에서 JAVA로 변경

### eclipse 단축키

> 글자크기 조절 : ctrl + shift + '+','-'
> 제안 : ctrl + 1
> 자동완성 : ctrl + space
> 줄 단위 복사 : ctrl + alt + 위, 아래 방향키
> 줄 단위 이동 : alt + 위, 아래 방향키
> 블록단위 영역 선택 : shift + alt + 위, 아래 방향키
> 자동 import : ctrl+shift+o
> run : ctrl+f11
