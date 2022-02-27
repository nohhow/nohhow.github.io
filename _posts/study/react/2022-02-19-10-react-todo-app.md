---
layout: post
title: (To-do-List) Start Dev To-do-List
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# [To-do-List] 앱 만들기 시작

App.js 기본 구조

```javascript
import React, {Component} from "react";

export default class App extends Component {
  render() {
    return(
      <div>
      </div>
    )
  }
}
```


## Styling 방법

1. App.css 파일에 style 작성 후 App.js 파일에서 엘리먼트에 className 부여하고 App.css 파일을 Import 하여 style 적용하기

2. App.js 파일 내부에서 class 내부에  style 작성하기

```javascript
export default class App extends Component {
  //style
  btnStyle = {
    color: "#fff",
    border: "none",
  }
  render() {
    return(
      //일부 생략
      <input type="checkbox" defaultChecked={false} />
      폼롤러 스트레칭
      <button style={this.btnStyle}>x</button>
    );
  }
}
```


### JSX Key 속성

리액트에서 요소의 리스트를 나열할 때는 Key를 넣어줘야한다.
키는 React가 변경, 추가 또는 제거된 항목을 식별하는 데 도움이 된다.

#### 즉, key를 통해서 가상 돔의 어떤 부분이 바뀌었는지 인식할 수 있다.
예를 들어 다음과 같이 before 에서 after로 변화되면 React에서 `<li>3</li>`이 새롭게 추가되었음을 인식하는데 문제가 없고 이 부분만 추가하게 되지만
```html
<!-- before -->
<li>1</li>
<li>2</li>

<!-- after -->
<li>1</li>
<li>2</li>
<li>3</li>
```

아래와 같이 `<li>3</li>`이 위로 올라오게 된다면, React가 모든 요소가 새롭게 된거라고 인식하고 모든 요소들을 지우고 새롭게 그리게 된다.
```html
<!-- before -->
<li>1</li>
<li>2</li>

<!-- after -->
<li>3</li>
<li>1</li>
<li>2</li>
```

그렇기 때문에 key라는 유니크 값을 넣어주는 것이 필요하다고 이해할 수 있겠다.

## React State

리액트에서는 데이터가 변하더라도 렌더링을 새롭게 해주지 않는다면 화면에 변화가 생기지 않는다.
화면을 다시 렌더링 하기 위해서는 React State를 사용해야 한다.

### React State란?
컴포넌트 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체이다.
State가 변경되면 컴포넌트는 리렌더링 된다. 또한 State는 컴포넌트 안에서 관리된다.

state를 컴포넌트 내에서 객체로 생성하여 관리하고
setState메서드를 통해서 갱신해준다.

---

## 전개 연산자 (Spread Operator)

전개 연산자는 ECMAScript6(2015)에서 새롭게 추가되었으며, 특정 객체 또는 배열의 갑을 다른 객체, 배열로 복제하거나 옮길 때 사용한다. 연산자 모양은 ... 이렇게 생겼다.

### 배열 조합

다음 두 코드는 동일하게 동작한다는 것을 알 수 있다.

```javascript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arr3 = [7,8,9];
const arrWrap = arr1.concat(arr2, arr3);

console.log(arrWrap); // [1,2,3,4,5,6,7,8,9]
```
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arr3 = [7,8,9];
const arrWrap = [...arr1, ...arr2, ...arr3];

console.log(arrWrap); // [1,2,3,4,5,6,7,8,9]
```

### 객체 조합

객체 조합의 경우, ... 연산자를 사용하는 경우와 그렇지 않은 경우의 결과가 다르다.
... 연산자를 사용하지 않고 객체를 조합하는 경우에는 대상 객체들이 하나의 객체에 **객체 자체로 들어가게되는** 반면 ... 연산자를 사용하여 조합하는 경우 객체 자체가 아닌 **각각의 값이 할당**되어 조합된다.

```javascript
const obj1 = {
    a: 'A',
    b: 'B'
};
const obj2 = {
  c: 'C',
  d: 'D'
};
const objWrap = {obj1, obj2};
console.log(objWrap);

//log결과
{
  obj1: {
    a: 'A',
    b: 'B'
  },
  obj2: {
    c: 'C',
    d: 'D'
  }
}
```
```javascript
const obj1 = {
    a: 'A',
    b: 'B'
};
const obj2 = {
  c: 'C',
  d: 'D'
};
const objWrap = {...obj1, ...obj2};
console.log(objWrap);

//log결과
{
  a: 'A',
  b: 'B',
  c: 'C',
  d: 'D'
}
```

### 기존 배열 보존
다음과 같이 배열에 메서드를 동작하여 값을 할당하는 경우에 ... 연산자를 사용하지 않은 경우 원본 배열이 함께 메서드의 동작에 영향을 받는 반면 ... 연산자를 사용하여 할당한 경우 원본 배열이 유지됨을 확인할 수 있다.

```javascript
const arr1 = [1,2,3];
const arr2 = arr1.reverse();

console.log(arr1); //[3,2,1]
console.log(arr2); //[3,2,1]
```
```javascript
const arr1 = [1,2,3];
const arr2 = [...arr1].reverse();

console.log(arr1); //[1,2,3]
console.log(arr2); //[3,2,1]
```
