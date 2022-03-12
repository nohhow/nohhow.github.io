---
layout: post
title: React Component
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---

# React Component, 리액트 컴포넌트

## React Component, 컴포넌트란?

**컴포넌트**는 리액트로 만들어진 앱을 이루는 최소한의 단위를 뜻한다.

만약 인스타 프로필 페이지를 만든다고 하면
* 검색 컴포넌트
* 프로필 컴포넌트
* 스토리 컴포넌트
* 포스트 컴포넌트
위와 같이 여러가지 컴포넌트가 모여서 하나의 페이지를 구성하게 된다.  
 > 실제로는 더 많이 쪼개져있을 수도 있다. E.g. 스토리 컴포넌트 > 아이템 컴포넌트

컴포넌트로 나눠서 페이지를 구성하게 되면 이 컴포넌트를 여러 곳에서 사용할 수 있다. (재사용성 높음)  
개발자가 동시에 한 페이지의 여러 부분을 개발/수정할 수 있다.

## 리액트 컴포넌트는 두 가지가 있다.

1. 클래스형 컴포넌트 (Class Component)
2. 함수형 컴포넌트 (Functional Component)

**'안녕하세요'**를 표현하기 위한 코드는 다음과 같이 차이를 보인다.
### 클래스형 컴포넌트
```js
class App extends Component {
  render() {
    return <h1>안녕하세요.</h1>;
  }
}
```

### 함수형 컴포넌트
```js
function App() {
  return <h1>안녕하세요.</h1>;
}
```

불과 몇 년 전까지는 리액트로 개발을 하면 대부분 클래스형 컴포넌트로 개발을 했었는데,  
지금은 함수형 컴포넌트로 개발하는 추세. 그래도 클래스형 컴포넌트를 학습해야하는 이유는 이전에 개발된 자료를 살필 때 이해하기 위함임 뿐만 아니라 클래스로 작성하는 것이 더 좋을 때도 있다.
