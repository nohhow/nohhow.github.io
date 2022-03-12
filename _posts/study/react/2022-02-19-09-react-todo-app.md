---
layout: post
title: (To-do-List) Intro & JSX
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# [To-do-List] 앱 소개 및 JSX 알아보기

### To-do-List 앱 소개

처음 언어를 배우거나 프레임워크를 익힐 때 가장 많이 만들어보는 To-do List 앱.
기본적인 CRUD 구현을 해보는 것을 목표로 한다.

### JSX 알아보기 (JSX : Javascript syntax extension)

JSX는 자바스크립트의 확장 문법이다. 리액트에서는 이 JSX를 이용해서 화면에서 UI가 보이는 모습을 나타내준다.

다음 예시 코드를 살펴보자.
```jsx
const simple = <h1>Hello World!</h1>;
```
`const simple = `은 javascript
`<h1>Hello World</h1>`은 HTML 의 모습을 보인다.

이처럼 JSX를 이용하면 UI를 나타낼 때 자바스크립트(logic)와 HTML구조(markup)를 같이 사용할 수 있기 때문에 기본 UI에 데이터가 변하는 것들이나 이벤트들이 처리되는 부분을 더욱 쉽게 구현 가능하다.

#### 리액트에서 JSX 사용은 의무인가?
의무는 아니지만 자바스크립트 안에서 UI 작업을 하는데 너무 편리하기 때문에 React를 사용하는 거의 모든 사람이 JSX를 사용한다.

##### JSX 없이 리액트에서 화면을 그리는 방식

React.createElement API를 사용해서 엘리먼트를 생성한 후 이 엘리먼트를 In-Memory에 저장한다. 그리고 ReactDOM.render 함수를 사용해서 실제 웹 브라우저에 그려준다.

> 화면 그리는 순서
[React.createElement] -> [ReactDOM.render]

```javascript
const myelement = React.createElement('h1', {}, 'I do not use JSX!!!');
```
```javascript
ReactDom.render(myelement, document.getElementById('root'));
```
JSX로 작성된 코드는 Babel 모듈을 통해서 위에서 작성한 코드로 변환된다.
<br>

##### 결국 JSX는 createElement를 쉽게 사용하기 위해서 사용하는 것
모든 UI를 만들 때마다 createElement를 사용해서 컴포넌트를 만들기 어렵다. 그러기에 JSX를 사용한 후 그걸 바벨이 다시 createElement로 바꿔서 사용한다.

##### JSX를 사용하면서 주의해야하는 문법들(규칙)

1. JSX 컴포넌트에 여러 엘리먼트 요소가 있다면 반드시 부모 요소 하나로 감싸줘야 한다.

```javascript
// 잘못된 코드
function hello() {
  return(
    <div>Hello World!</div>
    <div>What are you doing?</div>
  )
}
// 올바른 코드
function hello() {
  return(
    <div>
      <div>Hello World!</div>
      <div>What are you doing?</div>
    </div>
  )
}
```

나머지 규칙들은 추후 추가!
