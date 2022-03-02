---
layout: post
title: Destructuring
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# 구조분해할당(Destructuring)

* toc
{:toc .large-only}

배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript표현식(ES6)

<mark>Clean Code를 위해서 사용</mark>

### 객체 구조 분해 할당
```javascript
function buildAnimal(animalData){...}
```
```javascript
let obj = {
  accessory : 'horn',
  animal: 'horse',
  color : 'purple',
  hairType : 'curly'
}
```
아래 두 코드는 동일하게 동작한다.
```javascript
function buildAnimal(animalData){
  let accessory = animalData.accessory,
      animal = animalData.animal,
      color = animalData.animal,
      hairType = animalData.hairType;
      ...
}
```
```javascript
function buildAnimal(animalData){
  let {accessory, animal, color, hairType} = animalData;
}
```


### 배열 구조 분해 할당
요일을 담은 배열을 할당할 때
```javascript
const week = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday'];
const day1 = week[0];
const day2 = week[1];
const day3 = week[2];
const day4 = week[3];
const day5 = week[4];
```
위 코드는 다음과 같이 구조 분해 할당을 통해서 더 깔끔하게 작성할 수 있다.
```javascript
const week = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday'];
const [day1, day2, day3, day4, day5] = week;
```

#### for ... of , for ... in 문 (반복문)
* for ... of 문은 열거형 속성을 가진 객체를 key와 value로 나눠 보았을 때 value에 접근이 가능하다.
* for ... in 문은 key에만 접근 가능하다.
