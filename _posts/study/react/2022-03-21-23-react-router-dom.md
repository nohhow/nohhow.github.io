---
layout: post
title: React Router Dom
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# React Router Dom

* toc
{:toc .large-only}

## React Router Dom이란?

React Router DOM을 사용하면 웹 앱에서 동적 라우팅을 구현할 수 있다.
라우팅이 실행 중인 앱 외부의 구성에서 처리되는 기존 라우팅 아키텍처와 다르게 React Router DOM은 앱 및 플랫폼의 요구 사항에 따라 컴포넌트 기반 라우팅을 용이하게 한다.

* url과 UI와 동기화 된 상태를 유지시켜준다.
`localhost:3000/home => <Home/>`

### 리액트는 SPA(Single Page Application)다.
리액트는 단일 페이지 어플리케이션이기 때문에 하나의 index.html 템플릿 파일을 가지고 있다.
이 템플릿에 자바스크립트를 이용해서 다른 컴포넌트를 넣어주는 것으로 페이지를 변경한다.

이 때, React Router Dom 라이브러리가 새로운 컴포넌트로의 라우팅/탐색을 하고 렌더링하는 데 도움을 준다.

## 설치
```
npm install react-router-dom --save

yarn add react-router-dom
```

## 설정
모든 리액트 컴포넌트에서 활용할 수 있도록 setting : index.js 에서 루트 구성요소 래핑하기

```javascript
import { render } from "react-dom";
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";
// import your route components too

render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />}>
        <Route index element={<Home />} />
        <Route path="teams" element={<Teams />}>
          <Route path=":teamId" element={<Team />} />
          <Route path="new" element={<NewTeamForm />} />
          <Route index element={<LeagueStandings />} />
        </Route>
      </Route>
    </Routes>
  </BrowserRouter>,
  document.getElementById("root")
);
```

* BrowserRouter = 래핑한 부분을 라우팅하겠다.
* Routes = 앱에서 생성된 모든 개별 경로에 대한 컨테이너/상위 역할, Route로 생성된 자식 컴포넌트 중에서 매칭되는 첫번째 Route를 기본으로 렌더링 해줌
* Route = 단일 경로를 만드는 데 사용. path와 element 속성을 가짐
  * path = 컴포넌트의 URL 경로를 지정한다. 첫 번째 경로 이름은 `/`이다.
  * element = 경로에 맞게 렌더링 되어야 할 컴포넌트를 지정한다.


## React Router Dom APIs

1. **중첩 라우팅 (Nested Routes)**
레이아웃을 복잡하게 구현할 필요없이 중첩 라우팅을 통해서 라우팅해줄 수 있다.

```javascript
function App() {
  return (
    <Routes>
      <Route path="invoices" element={<Invoices />}> // localhost:3000/invoices
        <Route path=":invoiceId" element={<Invoice />} /> // localhost:3000/invoices/12
        <Route path="sent" element={<SentInvoices />} /> // localhost:3000/invoices/sent
      </Route>
    </Routes>
  );
}
```

2. **인덱스 라우팅 (Index Routes)**
인덱스 속성을 부여한 Route를 default child routes 로 한다.
다음 코드를 살펴보면 localhost:3000 환경에서 동작할 때, `localhost:3000/`으로 경로를 설정하면 index 속성이 부여된 Route, 즉 `Activity` 컴포넌트를 element로 갖고 있는 Route로 경로가 설정된다.

```javascript
function App() {
  return (
    <Routes>
      <Route path="/" element={<Layout />}>
        <Route index element={<Activity />} />
        <Route path="invoices" element={<Invoices />} />
        <Route path="activity" element={<Activity />} />
      </Route>
    </Routes>
  );
}
```

3. **Outlet**
자식 경로 요소에서 렌더링하기 위해서는 부모 경로 요소에서 `<Outlet/>` 을 사용해야 한다.
이렇게 하면 하위 경로가 렌더링 될 때 중첩된 UI가 표시될 수 있다. 부모 라우트가 정확히 일치하면 자식 인덱스 라우트를 렌더링하거나 인덱스 라우트가 없을 시에는 아무것도 렌더링 하지 않는다.

4. **useNavigate**
경로를 바꿔준다. `navigate('/home')` => localhostL3000/home 으로 이동

5. **useParams**
:style 문법을 path 경로에 사용했다면 UseParams()로 읽을 수 있다.

```javascript
import { Routes, Route, useParams } from "react-router-dom";

function App() {
  return (
    <Routes>
      <Route
        path="invoices/:invoiceId"
        element={<Invoice />}
      />
    </Routes>
  );
}

function Invoice() {
  let params = useParams();
  return <h1>Invoice {params.invoiceId}</h1>;
}
```

6. **useLocation**

이 Hooks는 현재 위치 객체를 반환한다. 현재 위치가 변경될 때마다 일부 side effect를 수행하려는 경우에 유용하게 사용할 수 있다.
