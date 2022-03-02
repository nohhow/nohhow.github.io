---
layout: post
title: Drag and Drop
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# HTML 드래그 앤 드롭

* toc
{:toc .large-only}

>* HTML 드래그 앤 드롭 API를 사용해서 원하는 항목을 드래그 할 수 있도록 할 수 있다.
 [Mozilla 문서 바로가기](https://developer.mozilla.org/ko/docs/Web/API/HTML_Drag_and_Drop_API)
> * 사용자가 드래그를 할 때 적절한 애니메이션을 부여한다.
> * 사용자가 드래그를 멈췄는지 확인한다. 그리고 여기에도 애니메이션을 부여한다.
> * 클라이언트가 목록을 재정렬한 경우 항목의 위치를 새 항목으로 업데이트 한다.

리액트에서 이것을 쉽게 구현할 수 있도록 도와주는 모듈 : react-beautiful-dnd

### react-beautiful-dnd 설치
`npm install react-beautiful-dnd --save`

### react-beautiful-dnd 모듈 설명

#### import 하기
```javascript
import { DragDropContext, Droppable, Draggable } from "react-beautiful-dnd"
```

#### 각 요소 설명
* DragDropContext : 드래그 앤 드롭이 가능한 영역
* Droppable : 드래그 한 항목을 드랍할 수 있는 영역
* Draggable : 드래그 할 수 있는 영역

#### Provided Object

provided object에는 스타일 지정 및 조회를 위한 속성이 포함되어 있다.

사용자가 요소를 드래그할 때 className 속성을 selected로 변경하고 나중에 스타일을 적용하는 데 사용한다.

placeholder 속성은 목록에 빈 공간을 생성하고 이렇게 하면 드래그 작업이 자연스럽게 보인다.

#### 추후 추가예정 (2022.03.01 기준 미작성)
