---
layout: post
title: Structure of create-react-app
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# Create React App으로 설치된 리액트 기본 구조

`npx create-react-app` 명령어로 리액트 설치 시 다음과 같이 폴더와 파일이 생성된다.

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

이 중에서 이름이 수정되지 말아야하는 파일들이 있다.

```plain text
1. public/index.html -> 페이지 템플릿
2. src/index.js      -> 자바스크립트 시작점
```

* public 폴더 내부에서는 public/index.html에서 쓰이는 파일만 위치한다.
* src 하위에는 JS 파일과 CSS 파일들을 위치 시키면 된다. 그리고 Webpack은 이 경로에 있는 파일들만 본다. 그래서 이 폴더 밖에 파일이 위치하면 Webpack에 의해서 처리도지 않는다.

### src 폴더
대부분의 리액트 소스 코드들은 src 폴더 내부에서 작업하면 된다.

### Package.json 파일
해당 프로젝트에 대한 정보들이 들어있다. 프로젝트 이름, 버전, 필요한 라이브러리와 라이브러리의 버전들이 시되어있다. 앱을 시작할 때 사용 할 스크립트, 앱을 빌드할 때, 테스트할 때 사용할 스크립트 등이 명시되어있다.

package.json
```
{
  "name": "react-basic-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.2",
    "@testing-library/react": "^12.1.3",
    "@testing-library/user-event": "^13.5.0",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-scripts": "5.0.0",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}

```

여기서 좀 더 살펴봐야할 곳은 scripts 부분이다.
```
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject"
},
```
여기서 명시한 대로 다음 명령어가 동작한다.
* `npm run start`를 했을 때 아래 보이는 코드 부분, json 파일의 script의 start라고 명시된 부분의 스크립트가 실행된다.
* `npm run build` 명령어는 build 폴더가 생성되며, 폴더 하위에 개발한 것들이 webpack을 통해서 압축이 되어 실제 운영을 위한 파일을 build 해준다.
* `npm run test` 명령어는 App.test.js에 작성해 둔 테스트 케이스를 리액트에서 실행하며 테스트 통과 여부를 알려준다.
