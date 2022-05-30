---
layout: post
title: Homebrew MySQL 명령어 정리
image:
  path: https://source.unsplash.com/random
description: >
  Homebrew MySQL 명령어 정리
sitemap: false
categories:
  - study
  - etc

---
# Homebrew MySQL 명령어 정리

* toc
{:toc .large-only}

### MySQL 일반 실행
1. **설치**

`brew install mysql`


2. **MySQL 서버 실행하기**

`mysql.server start`

3. **MySQL 서버 종료하기**

`mysql.server stop`


###MySQL을 데몬으로 실행하기

1. **실행**

`brew services start mysql`

2. **서비스 재시작하기**

`brew services restart mysql`

3. **데몬으로 실행되고 있는 프로그램 목록 확인하기**

`brew services list`

4. **데몬 형태로 실행되고 있는 MySQL 종료하기**

``brew services stop mysql``

[출처 : 치악산 복숭아](https://bsscl.tistory.com/5)
