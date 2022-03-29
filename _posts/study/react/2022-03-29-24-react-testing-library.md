---
layout: post
title: React Testing Library
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# React Testing Library

* toc
{:toc .large-only}

## React Testing Library란?
React Testing Library(이하 RTL)는 React 구성 요소 작업을 위한 API를 추가하여 DOM Testing Library 위에 구축된다.

기본적으로 `create-react-app`으로 프로젝트를 생성했다면 자동으로 설치되어있다.


> **DOM Testing Library**는 DOM 노드를 테스트하기 위한 매우 가벼운 솔루션  


RTL은 구현 세부 정보를 테스트하는 Enzyme의 대안으로 각광받고 있는 테스트 도구라고 한다.

RTL은 Enzyme와 달리 구현보다 **기능**과 **동작**에 초점을 맞춘 테스트 도구이다. 즉 '어떻게 구현되었는가?' 보다 '사용자에게 어떻게 보이는가?' 가 더 중요하다고 보는 '사용자 관점'에서 수행되는 테스트가 되겠다.

또한 Enzyme는 state와 props를 사용하여 컴포넌트를 테스트하는데, 누군가 변수 이름이나 props를 변경하면 기능적 요소가 변경되지 않았더라도 테스트가 실패할 수도 있다.
반면 RTL에서는 state와 props에 따른 테스트가 아닌, 사용자가 상호작용하는지 테스트하기 위해 DOM요소를 사용한다. Enzyme는 어떤 경우에 DOM도 테스트할 수 있지만 RTL은 DOM에 따라서 구성 요소를 테스트하도록 강제하며 구성 요소 내부에는 액세스할 수 있는 방법이 없다.

> Enzyme과 RTL을 자체적으로 비교하여 무엇이 더 나은지를 판단하기보다, 상황에 맞게 사용할 것을 권한다.

요약 출처 : https://medium.com/wesionary-team/react-testing-library-vs-enzyme-afd29db380ac

### CRA에 기본으로 작성되어있는 App.test.js 살펴보기

```javascript
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

테스트 케이스 내부를 살펴보면
`render()`를 통해서 DOM에 컴포넌트를 렌더링하고 있다. 이를 통해서 App 컴포넌트를 렌더링하고 그 결과 스크린에 learn react라는 문구가 포함되어있는가를 테스트하고 있다.
expect와 matcher를 이용하여 테스트를 진행하고 있다.

실제로 CRA로 프로젝트를 생성하면 App.js는 다음과 깉이 작성되어있기 때문에 테스트 결과는 PASS이다.
```javascript
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React // 여기에 Learn React가 위치하고 있는 것을 알 수 있다.
        </a>
      </header>
    </div>
  );
}

export default App;
```

### 쿼리 함수
위애서 살펴본 테스트 케이스에서 learn react라는 요소를 찾기 위해서 `  const linkElement = screen.getByText(/learn react/i);` 이런 코드가 작성되어 있는 것을 볼 수 있다.

여기서 `getByText`는 쿼리 함수에 해당하는데, 페이지의 특정 요소를 찾기 위해서 사용하는 함수이다. `getByText` 외에도 페이지의 특정요소를 찾기 위한 다양한 쿼리함수를 React Testing Library에서 제공하고 있다.

#### 1. getBy
쿼리에 대해서 일치하는 노드를 반환하고 일치하는 요소가 없거나 둘 이상의 일치가 발견되면 설명 오류를 발생시킴(둘 이상의 요소가 예상되는 경우에는 getAllBy를 사용해야함)

#### 2. queryBy
쿼리에 대해서 일치하는 노드를 반환하고 일치하는 **요소가 없으면 null을 반환**한다. 둘 이상의 일치가 발견되면 오류 발생(queryAllBy 사용)

#### 3. findBy
주어진 쿼리와 일치하는 요소가 발견되면 Promise를 반환. 요소가 발견되지 않거나 기본 제한 시간인 1000ms 후에 둘 이상의 요소가 발견되면 Promise가 거부됨.(둘 이상의 요소는 findAllBy 이용)
