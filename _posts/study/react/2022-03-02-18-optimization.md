---
layout: post
title: (To-do-List) Project Optimization with React.memo
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# [To-do-List] 프로젝트 최적화 (React.memo, useMemo, useCallback)

### React.memo를 이용한 컴포넌트 최적화

#### 현재 To-Do 앱 문제점
* App, Lists, List, Form 으로 컴포넌트가 나눠져 있음.
* 이렇게 나눠준 이유는 재사용성을 위해서이기도 하지만 각 컴포넌트의 렌더링의 최적화를 위해서 이기도 함.

여기서 **문제**가 있다.

Form 에서 text를 작성할 때, Form과 App 만 렌더일 되어야하지만, Log를 설정하고 확인해보면 Lists, List 컴포넌트도 함께 렌더링되고 있음을 알 수 있다.

#### 문제 해결 방법 : React.memo 적용
각 컴포넌트 함수에 React.memo()적용

```javascript
const List = React.memo(() => {})
```

---

### useCallback 을 이용한 함수 최적화

#### 현재 문제
* 원래 컴포넌트가 렌더링 될 때 그 안에 있는 함수도 다시 만들게 됨.
* 컴포넌트가 렌더링 될 때마다 **계속해서 함수를 다시 만드는** 현상은 좋은 현상이 아님.

#### 문제 해결 방법 : React.useCallback 적용
useCallback은 함수를 재사용할 수 있게 만들어 준다.
[velopart님 글 참고](https://react.vlpt.us/basic/18-useCallback.html)

>위에서 React.memo를 이용하여 List,Lists 가 재사용성을 갖도록 설정해 두었고, Form 컴포넌트에서 text 입력을 할 때, 불필요하게 List와 Lists를 리렌더링 하지 않는 것을 볼 수 있었다.

>하지만 만약 각각 자식/자손 컴포넌트에 해당하는 List와 Lists가 부모 컴포넌트에 해당하는 App이 특정 함수를 List와 Lists에 props로 전달하고 있다면, props가 변화함에 따라 함수가 변화하기 때문에 이는 또 다시 렌더링할 이유를 제공하게 된다.

이 때 렌더링을 방지하기 위해서 useCallback을 사용하겠다는 것.


##### useCallback 적용 방법
useCallback은 useCallback 안에 콜백함수와 의존성 배열을 순서대로 넣어주면 된다.
의존성 배열에는 함수 내에서 참조하는 state, props가 있는 경우에 추가해준다.

의존성 배열에 포함되어있는 참조값들이 변할 때에 다시 함수를 생성하게 된다.
```javascript
const handleClick = useCallback( () => {}, [참조값] )
```
---

### useMemo를 이용한 결과 값 최적화

> Memo = Memoization

#### Memoization 이란?
Memoization은 비용이 많이 드는 함수 호출의 결과를 저장하고 동일한 입력이 다시 발생할 때 캐시된 결과를 반환하여 컴퓨터 프로그램의 속도를 높이는데 주로 사용되는 최적화 기술이다.

**연산의 복잡도가 높으면 발생하는 문제**
1. 성능 문제
2. UI 지연 현상

#### 문제 해결 방법 : useMemo 적용
useMemo를 적용하면 함수의 인자값이 달라지지 않는다면 반환값을 이전에 계산했던 것의 값 그대로 반환시켜준다(재활용).

#### useMemo 적용 방법
useCallback과 마찬가지로 인자를 두 개 갖는데, 첫 번째 인자는 적용하고자 하는 부분, 그리고 다른 하나는 의존성 배열이 들어간다.
```javascript
function Component({ a, b}) {
  const result = useMemo( () => compute(a, b), [a, b])
  return <div>{result}</div>
}
```
