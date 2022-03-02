---
layout: post
title: TailWindCSS
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# TailWindCSS

* toc
{:toc .large-only}

### TailWindCSS 란?
HTML 안에서 CSS 스타일을 만들 수 있게 해주는 **CSS 프레임워크**

#### CSS 프레임워크란?
CSS 프레임워크는 레이아웃 및 여러 컴포넌트 구성, 브라우저 호환성을 보장하는데 소요되는 시간을 최소화하기 위해서 여러 웹 개발/디자인 프로젝트에 적용할 수 있는 CSS 파일 모듈이다.
> 더 빠르게 애플리케이션을 스타일링 하는데 도움을 준다.

#### CSS 프레임워크 종류 for React JS
```
1. Material UI
2. React bootstrap
3. Semantic UI
4. Art Design
5. Materialize
```

### TailWindCSS의 장점
Bootstrap과 비슷하게 m01, flex와 같이 미리 세팅된 Utility Class를 활용하는 방식으로 HTML 에서 스타일링을 할 수 있다.

1. 빠른 스타일링 작업 가능
2. class 혹은 id명을 작성하기 위한 고생을 하지 않아도 됨
3. 유틸리티 클래스에 익숙해지는 시간이 필요하나 intelliSense 플러그인이 제공돼서 금방 익숙해질 수 있음

#### TailWindCSS intelliSense (VSCode)
<img width="863" alt="스크린샷 2022-03-01 오후 12 53 35" src="https://user-images.githubusercontent.com/61059893/156101720-c87c0654-aa23-473b-901c-d53669db83e5.png">

> intelliSense는 처음에 class utility를 사용할 때 익숙해질 수 있도록 도움을 줄 수 있다.

#### TailWindCSS 공식 홈페이지
[TailWindCSS](https://tailwindcss.com/)

### TailWindCSS React에 적용하기

1. `npm install`
```
npm install -D tailwindcss postcss autoprefixer
```

npm install -D 로 설치하면 package.json 파일에서 보면 dependencies에 들어가는 것이 아니라 개발환경에서만 적용되어
```
"devDependencies": {
  "autoprefixer": "^10.4.2",
  "postcss": "^8.4.7",
  "tailwindcss": "^3.0.23"
}
```
devDependencies에 삽입되어있는 것을 볼 수 있다.

2. `npx tailwindcss init`
해당 명령 실행시, tailwind.config.js 파일이 생성됨

3. CSS 파일에 해당 코드 붙여 넣기
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

### 자주쓰는 Class Utility

1. 마진(Margin)
```
m-1 // margin, 숫자 1 = 0,25rem
ml-1 // margin-left
mr-1 // margin-right
mt-1 // margin-top
mb-1 // margin-bottom

mx-1 // margin-left, margin-right
my-1 // margin-top, margin-bottom
```

2. 패딩(Padding)
```
p-1 // padding
.
.
.

마진과 동일한 패턴
```

3. display = flex
`flex`

4. justify-content : ''
`justify-between // justify-content = 'space-between'`

5. align-items : center
`items-center`

6. width
```
w-full // width:100%
w-4/5 // width:80%
```

7. border-width
`border`

8. border-radius
`rounded`
