---
layout: post
title: React Immutable
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# 리액트 불변성 지키기

### 리액트에서 불변성이란?
불변성이란 사전적 의미로는 값이나 상태를 변경할 수 없는 것을 의미한다.
자바스크립트 타입을 통해서 좀 더 자세히 알아볼 수 있다.

#### 자바스크립트 타입을 통한 불변성 의미 살펴보기
원시 타입은 불변성을 가지고 있고, 참조 타입은 그렇지 않기 때문에 둘을 비교하면서 불변성의 의미를 자세히 알아볼 수 있다.

* 원시 타입 : Boolean, String, Number, null, undefined, Symbol (불변성 지님)
* 참조 타입 : Object, Array

기본적으로 Javascript는 원시 타입에 대한 참조 및 값을 저장하기 위해 Call Stack 메모리 공간을 사용한다.
하지만 참조 타입의 경우 Heap이라는 별도의 메모리 공간을 사용한다. 이 경우 Call Stack은 개체 및 배열 값이 아닌 메모리에만 Heap 메모리 참조 ID값으로 저장한다.

<img width="807" alt="스크린샷 2022-03-01 오후 11 37 46" src="https://user-images.githubusercontent.com/61059893/156188913-1a5f32e0-8711-4e79-80e4-ac1bb4f2e602.png">


#### 정리
* 원시 타입 : 고정된 크기로 Call Stack 메모리에 저장, 실제 데이터가 변수에 할당된다.
* 참조 타입 : 데이터 크기가 저장되어 있지 않고 Call Stack 메모리에 저장, 데이터의 값이 heap에 저장되며 변수에 heap 메모리의 주소값이 할당된다.

**원시타입 데이터할당 예시)**
```javascript
let username = "walter"
    username = "john"
```
username walter 를 john으로 대체하는 것이 아닌 영역 a에 walter를 그대로 두고, 영역 b에 john을 새로 할당한다. (불변성 유지 중)

**참조 타입 데이터 할당 예시)**
```javascript
let array = ['1', '2', '3']
    array = ['4', 5, '6']
```
배열에 대한 요소를 추가하거나 객체 속성 값을 변경할 때, Call Stack의 참조 ID는 동일하게 유지되고 해당 주소(참조ID)가 실제 위치한 Heap 메모리에서만 변경이 이뤄진다. 그렇기 때문에 불변성이 유지되지 않는다. = 실제 값이 바뀌는 것


### 불변성이 지켜져야 하는 이유
1. 참조 타입에서 객체나 배열의 값이 변할 때 원본 데이터가 변경되기 때문에 원본 데이터를 참조하고 있는 다른 객체에서 예상치 못한 오류가 발생할 수 있어서 프로그래밍의 복잡도가 올란간다.

2. 리액트에서 화면을 업데이트 할 때 불변성을 지켜서 값을 이전 값과 비교해서 변경된 사항을 확인한 후 업데이트하기 때문에 불변성을 지켜야 한다.

### 불변성을 지키기 위해서는...!

참조 타입에서 값을 바꿨을 때, Call Stack 주소 값은 같은데 Heap 메모리 값만 바꿔주기 때문에 불변성을 유지할 수 없었다. 그렇다면 아예 <mark>새로운 배열을 반환하는 메소드를 사용하자!</mark>

`spread operator, map, filter, slice, reduce` => 불변성을 지킬 수 있어!

<주의 !!> 원본 데이터를 변경하는 메소드 =>`splice, push`
