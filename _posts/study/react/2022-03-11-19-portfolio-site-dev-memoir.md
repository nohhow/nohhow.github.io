---
layout: post
title: Portfolio site development memoir, with React
image:
  path: https://user-images.githubusercontent.com/61059893/157826432-582d4822-626a-4812-996b-93539f92c845.png
description: >
  포트폴리오 사이트 개발 회고
sitemap: false
categories:
  - study
  - react

---
# 포트폴리오 사이트 개발 회고 (with React) - 설계

* toc
{:toc .large-only}

## 포트폴리오 사이트 개발 개요
졸업장을 받은 지난 달까지 대외 활동, 개발 파트 타임 등 바쁜 시간을 보내느라고 3월 중반이 다가오는 지금까지도 포트폴리오와 이력서가 준비되어있지 않았다.

가고 싶던 회사들에의 취업 공고가 계속해서 올라오고, 더 이상 미룰 수 없게 되어 예전 기록들을 뒤적이며 이력서를 작성하고, 그 동안 진행했던 프로젝트들을 좀 더 잘 보여주기 위해서 포트폴리오를 작성하기 시작했다.

포트폴리오를 pdf나 ppt로 만들지 아니하고 웹 페이지로 개발한 이유는 아무래도 프론트엔드 개발 직무에 지원하는데, 웹에서 나의 표현 방식을 보여주는 것이 중요하다고 생각이 들었기 때문이다.
내가 어떤 활동을 했고, 어떤 이력을 갖고 있는지 <mark>브라우저에서 보여준다는 점</mark>이 가장 중요한 포인트라고 생각한다.

p.s. 물론 포트폴리오를 URL로 받아보지 않는 회사도 존재하기 때문에 pdf 파일도 준비해야했다.


## 결과물 소개
1. INTRO
<img width="1792" alt="pf-thumbnail" src="https://user-images.githubusercontent.com/61059893/157826432-582d4822-626a-4812-996b-93539f92c845.png">

2. ABOUT ME
<img width="1790" alt="pf-1" src="https://user-images.githubusercontent.com/61059893/157826382-41f157ec-d40b-44f9-b6b4-18480c6f90e4.png">
<img width="1792" alt="pf-2" src="https://user-images.githubusercontent.com/61059893/157826409-d231ec06-a1cb-4f84-9d4e-2397559f82d3.png">

3. SKILLS
<img width="1792" alt="pf-4" src="https://user-images.githubusercontent.com/61059893/157826429-036383e5-365a-4a5b-be22-ac385d9368b7.png">

4. PROJECTS
<img width="1792" alt="pf-3" src="https://user-images.githubusercontent.com/61059893/157826422-9a029d7a-7f44-40ab-b74c-917df61602dc.png">

---

## 개발 과정

* 기술 선정
* 화면 설계
* 기능 정의
* 개발
* 미디어별 대응 - 반응형

### 기술 선정
먼저 어떤 기술 스택으로 포트폴리오를 작성할지 생각해봤다.

> **언어**

* HTML, CSS
* Javascript

> **라이브러리**

* React.js
* Bootstrap - react-bootstrap `UI 디자인`

> **호스팅**

* GitHub Pages - gh-pages

> **개발 도구**

* Visual Code

HTML과 CSS, Javascript는 선택의 여지가 없고
동적인 요소가 많이 있는 것은 아니지만 React를 사용한 이유는 다음과 같다.
~~~
1. React 생태계를 경험해보고 싶어서 (다양한 라이브러리)
2. JSX에 익숙해지고 싶어서
3. 컴포넌트 단위로 작성하면 추후에 재사용할 수 있을 것이라고 생각해서  
~~~
또한 반응형 웹으로 만들고 싶었고, Bootstrap을 활용하면 잘 할 수 있다고 생각했다.

### 화면 설계
와이어프레임에 그려가면서 상세하게 디자인하면 좋겠지만 제출 날짜에 쫓겨 대략적으로 작성했다.

1. 고려사항

* 거슬리지 않는 단순한 디자인과 색상 선정 `블랙, 화이트, 블루`
* 네비게이션바를 최상위에 두고 고정
* 하단 스크롤만으로 모든 내용을 훑어볼 수 있도록 항목들을 배치

2. 기본 골격

```html
 <nav>
 <section id="intro">
 <section id="about-me">
 <section id="skills">
 <section id="projects">
 <footer>
```

3. 구성 요소

~~~
✔️ Nav : 브랜드명 = '노진현 포트폴리오', 메뉴는 Section 항목들로 구성
✔️ Intro : 시선을 사로잡는 이미지나 문구로 '나'를 표현하기
✔️ About Me : 이름, 연락처, 이메일, 주소, 생년월일, 학력 (기본 인적사항)
✔️ Skills : 기술 스택들
✔️ Projects : 프로젝트 이미지, 프로젝트명, 프로젝트 세부내용, 기술스택, 성과
✔️ Footer : 블로그 바로가기, github 바로가기
~~~

### 기능 정의
어떤 것을 보여주고 어떻게 구현할 것인가에 대한 정리  

> **네비게이션 바**

* 네비게이션 바는 상단 고정
* 네비게이션바에서 각 항목 클릭시 각 Section으로 Scroll 이동 `href=#`

> **인트로**

* 스크롤 유도 애니메이션 첨부 `방문자의 다음 행동에 대한 가이드`

> **자기소개**

* 이름, 연락처, 이메일, 주소 등 기본 인적사항 Bootstrap의 Grid System 이용해서 표현 (Container > Row> Col)

> **기술 스택**

* Certificate와 Main 기술, Sub 기술을 구분하여 Bootstrap의 Grid System 이용해서 표현 (Container > Row> Col)
* Main 기술에 대해서는 각 항목에 MouseOver 이벤트를 추가하고, MouseOver시 기술에 대한 숙련도를 ProgressBar로 표현
* 이벤트로부터 상태 변화에 대응하기 위해서 State로 관리
* 유지 보수를 위해서 객체로 관리

> **프로젝트**

* 각 프로젝트는 Bootstrap의 Card로 나열 `img`, `title`, `tech-stack` 표시
* 각 항목에 Click 이벤트를 추가하고, Click 시 프로젝트 상세내용 표시 `img`, `title`, `subtitle`, `tect-stack`, `description`, `result` 등
* 프로젝트 상세내용에서 보여질 이미지가 많아, Slick 슬라이드로 표시
* 상세 내용 조회 후 목록 화면으로 돌아갈 수 있도록 버튼 배치
* 이벤트로부터 상태 변화에 대응하기 위해서 State로 관리
* 유지 보수를 위해서 객체로 관리

---

### 개발부터 반응형 대응까지는 다음 게시물에서
[여기](https://nohhow.github.io/study/react/2022-03-11-26-portfolio-site-dev-memoir-tech/)서 다음 내용(개발, 미디어 대응)이 이어집니다.
