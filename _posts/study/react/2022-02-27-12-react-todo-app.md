---
layout: post
title: (To-do-List) Refactoring with React Hooks
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# [To-do-List] 리액트 Hooks를 이용해서 함수형 컴포넌트로 바꾸기

## 클래스 컴포넌트에서 함수 컴포넌트로 바꾸는 순서
정해진 순서는 없지만 강의에서는 다음과 같은 순서로 진행한다.

1. 컴포넌트 자체를 바꾸기
2. `render(){return()}` -> `return()`
3. State -> useState Hook를 이용해서 표현
> `const [value, setValue] = useState("");`
첫 번째 인수는 변수 이름, 두 번째 인수는 State를 정하는 함수를 뜻한다.

4. `this.state.value -> value`
5. state를 새로운 값으로 update 해줄 때, `this.setState({value:""}) -> setValue("")`
> Setter에서 이전 State를 가지고 오기 위해서는 인수에 함수를 이용해서 사용할 수 있다.
`this.setState({todoData: [...todoData, newTodo]});` -> `setTodoData(prev => [...prev, newTodo])`

6. 함수 및 변수 정의 방법 변경
> `handleClick = (id) => {}` -> `const handleClick = (id) => {})`

7. 정의된 함수 및 메소드 사용 방법 변경
> this.함수명 -> 함수명
