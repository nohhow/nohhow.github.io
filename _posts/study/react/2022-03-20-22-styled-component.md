---
layout: post
title: Styled Components
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# Styled Components

* toc
{:toc .large-only}

## Styled Components란?

Styled Component는 Css-in-JS 라고 하는 Javascript 파일 안에서 CSS를 처리할 수 있도록 해주는 대표적 라이브러리이다.

[styled-components 공식 페이지](https://styled-components.com/)

아래부터는 공식 홈페이지 docs에 기반하여 간단한 설명을 덧붙인다.


## 소개
styled-components는 리액트 컴포넌트 시스템에서의 스타일링 경험을 향상시키기 위해서 고민한 결과물이다. 그리고 다음과 같은 특징을 갖는다.

1. **Automaticall critical CSS**
렌더링 되는 구성 요소를 추적해서 자동으로 해당 스타일만 삽입하여 준다. 이는 사용자에게 필요한 최소한의 코드만 로드 되는 것을 돕는다. = 리액트의 컨셉에 부합하다.

2. **No class name bug**
styled-components는 스타일을 위해 unique한 클래스명을 사용하기 때문에 절대 중복되거나 덮어쓰거나하는 경우가 없다.

3. **Easier deletion of CSS**
코드를 많이 작성하다보면 불필요한 CSS를 남겨두거나 어디서 사용되는지 모르게 된다. 하지만 styled-components는 모든 구성 요소와 연결되어 있기 때문에, 사용되지 않을 경우 감지되며 삭제될 때 구성 요소의 스타일은 모두 삭제된다.

4. **Simple dynamic styling**
클래스를 수동으로 관리할 필요없시 props 또는 전역 테마를 기반으로 구성 요소의 스타일을 적용하는 것이 간단하고 직관적이다.

5. **Painless maintenance**
구성 요소에 영향을 주는 다른 스타일을 찾기 위해 탐색할 필요가 없고, 조각화 되어 관리가 용이하다.

6. **Automatic vendor prefixing**
CSS를 표준에 따라 작성하면 나머지는 styled-components가 처리해준다.

## 설치
```
# with npm
npm install --save styled-components

# with yarn
yarn add styled-components
```

## 작성 예시

### BASIC

다음과 같이 리액트 컴포넌트를 생성하면 스타일이 적용된다.

```javascript
// Create a Title component that'll render an <h1> tag with some styles
// Title 변수에 다음과 같이 작성하고, 컴포넌트처럼 작성해주면 h1으로 render되며 다음 스타일이 적용된다.
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`

const App = () => {
  return(
      <div>
        <Title>
          안녕하세요!
        </Title>
      </div>
  );
};
```

### props 기반으로 스타일 적용

props의 값에 따라서 스타일에 변화를 줄 수도 있다.

```javascript
const Button = styled.button`
  /* Adapt the colors based on primary prop */
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    <Button primary>Primary</Button>
  </div>
);
```

### 스타일 상속받아 확장 적용

Java에서 클래스를 상속받아 Override 하는 것과 유사하다.
미리 작성된 Button style을 기반으로 하여 TomatoButton을 생성하는 것을 예시로 소개하고 있다.

```javascript
// The Button from the last section without the interpolations
const Button = styled.button`
  color: palevioletred;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

// A new component based on Button, but with some override styles
const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;
`;

render(
  <div>
    <Button>Normal Button</Button>
    <TomatoButton>Tomato Button</TomatoButton>
  </div>
);
```
