---
layout: post
title: Javascript Basic
image:
  path: /assets/img/thumbnail/javascript.png
description: >
  자바스크립트 기초 다지기
sitemap: false
categories:
  - study
  - javascript

---
# 자바스크립트 기초

* toc
{:toc .large-only}

> 자바스크립트를 내 main 언어로 말하지만 면접에서 어떠한 질문을 맞이하였을 때, 막힘없이 이야기 하고 싶어서 기초부터 다시 살펴보기로 했다.

[코딩앙마 - 자바스크립트 기초 강좌](https://www.youtube.com/watch?v=KF6t61yuPCY)

위 강의를 살펴보며 기초를 다듬어본다.
새롭게 느끼는 바가 없는 내용은 제외했다.

---

## 변수
* 상황에 따라서 let, const를 구분하여 사용할 줄 알아야함.
* var를 왜 사용하지 않게 되었는지 알아야함.

### var
es6 이전에 변수 선언을 위해서 사용했고, 다음과 같은 이유로 더 이상 사용하지 않는다.
1. **중복 선언 가능** : 코드의 양이 많아지거나 유지보수 시에 변수가 어디서 어떻게 사용됐는지 모른 체 중복 선언하여 사용하게 될 수 있다.

2. **호이스팅 (Hoisting)** : 변수 선언시 선언과 초기화(undefined로)가 동시에 발생하기 때문에 별도의 초기화를 하지 않아도 ERROR없이 참조를 할 수 있다. 이는 함수 표현식 사용에서도 문제가 된다. 자세한 내용은 다음 링크를 참고하자.

> **호이스팅이란 ?**
[자바스크립트 호이스팅 알아보기](https://nohhow.github.io/study/javascript/2022-03-12-02-hoisting)


3. **함수 스코프를 가짐** : 함수 내에서 var로 선언된 변수는 `{}`블록 스코프와 관계없이 유효하다. 이는 함수 내에서 이 값을 다룰 때, 실수이 여지가 생길 수 있다.

4. **반복문에서 정의된 변수가 계속 유효함** : 흔히 반복문을 사용할 때, `for(var i = 0; i < 5; i++){<실행문>}` 구조로 많이 작성하는데, 여기서 선언한 i가 반복문 밖에서도 유효하다. 유효한 이 값은 다른 실행에 영향을 미칠 수도 있기에 유의하게 된다.


### let 과 const

#### let
**변할 수 있는 값**으로, `let`은 선언한 값에 새로운 값을 할당할 수 있으나 동일한 변수명으로 재선언 하는 것은 불가능하다.

```javascript
let name = "Jinhyun";
let name = "Noh" //Uncaught SyntaxError: Identifier 'name' has already been declared" : 이중 선언 불가
```
```javascript
let name = "Jinhyun";
console.log(name); // Jinhyun
name = "Noh"
console.log(name); // Noh
```

#### const
**절대로 바뀌지 않는 상수**로, var이나 let과 다르게 수정이 불가능하다.
e.g. Pi, Birthday, Max-value 등을 설정할 때 사용한다.

* 대문자로 선언하는 것이 좋음. (=나 상수다 티내기)
* 여러 단어 조합시 `_`사용 (e.g. `MAX_SPEED`)

### 변수 명명 규칙
1. 문자와 숫자, `&`, `_` 만 들어갈 수 있음
2. 첫 글자는 숫자가 될 수 없음
3. 여러 단어 조합 시 카멜 표기법(camelCase)으로 작성
4. 대소문자는 구분됨 (`myName`과 `MyName`은 다른 변수다.)
5. 모든 언어를 변수명에 사용할 수는 있으나 영어 사용이 국제적 관습
6. 예약어는 피해서 명명해야 함.
7. 읽기 쉽고 이해할 수 있도록 명명

---

## 자료형
* 각 자료형의 특징들, 최신 문법을 인지해야함.


### 문자형 String

> 문자열 작성 방법 3가지

1. 큰따옴표
2. 작은따옴표
3. **백틱 (es5)** - template literal 템플릿 문자열

```javascript
const name1 = "Mike";
const name2 = 'Mike';
const name3 = `Mike`;
```

#### 템플릿 문자열
> **특징**

1. Multi-line strings
기존 문자열에서 줄바꿈을 하기 위해서는 newline characters(`\n`)을 삽입해야 한다. 그러나 template literal에서는 그냥 enter를 입력하여 줄바꿈하면 동일한 효과를 얻을 수 있다.

2. Expression interpolation(표현식 삽입법)
`${}` 표현을 사용해서 표현식을 보다 간편하게 삽입할 수 있다.

```javascript
var a = 5;
var b = 3;

//기존 문자열
console.log("eight is " + (a + b) + "and\n not " + (2 * a + b) + ".");

//template literal
console.log(`eight is ${a + b} and
not ${2 * a + b}.`)
```

### 숫자형 Number
* \+
* \-
* \*
* /
* %

#### NaN
* NaN : Not a Number
* 숫자 관련 작업을 할 때 NaN이 아닌지 항상 염두하며 작업해야함.

### 불리언 Boolean
* true
* false

### null, undefined
* 변수를 선언만 하고 아무 것도 할당하지 않으면 undefined를 출력한다. (호이스팅)
* null : 존재하지 않는다.

>`typeof null`을 실행해보면 `object`라고 출력되지만, 이는 객체가 아니다. 명백한 오류이나 하위호환성을 위해 수정하지 않는다.

---

## 대화상자

### Alert
알려주는 역할
`alert()`
* 취소버튼만 있음

### Prompt
입력 받는 역할
`prompt()`

* prompt 창에서 취소 클릭 시 `null`값 들어감
* default값도 입력 가능, 2번째 인자에 기입하는 값이 default 값이 됨.
`prompt("휴대폰 번호를 입력해주세요.", "010-");`

### Confirm
확인 받는 역할
`confirm()`

```javascript
const isAdult = confirm("당신은 성인입니까?");
console.log(isAdult);
```
* Alert와 비슷하나, 확인과 취소 버튼이 있어 선택할 수 있음.
* 확인 -> `true` 반환
* 취소 -> `false` 반환

### 대화상자 단점

1. 대화상자가 떠 있는 동안 스크립트가 일시 정지 됨.
2. 스타일링 X

---

## 형변환

* `String()` 문자형으로 변환
* `Number()` 숫자형으로 변환
  * `Number("문자") // NaN`
  * `Number(null) // 0`
  * `Number(undefined) // NaN`
* `Boolean()` 불린형으로 변환
  다음은 false에 대응되는 것들
  * 숫자 0
  * 빈 문자열
  * null
  * undefined
  * NaN

### 자동 형변환

```javascript
console.log(("50" + "70") / 2); // 2535
```
> 문자열끼리 더해주고, 나눗셈 단계에서 이를 **자동형변환**하여 계산했다.

자동 형변환은 편리할 수 있으나, 헷갈릴 수 있기 때문에 **명시적 형변환**이 필수적이다.

---

## 함수
* 한 번에 한 작업에 집중
* 읽기 쉽고 어떤 동작인지 알 수 있도록 네이밍 할 것

### 지역변수, 전역변수
* var와 let, const를 구분하여 이해할 것

```javascript
let msg = "hi";
console.log(msg); // hi

funtion showAlert(name){
  let msg = "hello";
  console.log(msg + ", "+ name);
}

showAlert("Brian"); // hello, Brian
console.log(msg); // hi
```

### return
* `return`문이 없는 함수의 반환값은 `undefined`이다.
* `return`만 있어도 `undefined`이다.
* 함수 내부 실행문에서 `return`을 만나면 그 즉시 우측 값을 반환하고 함ㅎ수를 종료한다. 그래서 **함수 종료를 목적**으로 사용하기도 한다.

```javascript
function showError(){
  alert('에러발생');
}
const result = showError();
console.log(result);
```

### 함수 선언문 vs 함수 표현식

* 함수 선언문 : `function showError(){}`와 같은 구조
* 함수 표현식 : 이름 없는 함수 `function(){}`을 만들고 이를 변수에 할당해주는 형태

#### 차이점

> **호출 위치**
* 함수 선언문은 호이스팅 대상이 되어 어디서든 호출이 가능하다.
* 함수 표현식은 호이스팅 규칙에서 제외되어 표현식 이후에만 호출이 가능하다.

### 화살표 함수
함수의 간결한 표현 방식

```javascript
// 화살표 함수
let add = (num1, num2) => {
  return num1 + num2
}
```

* `return` 문은 중괄호`{}`가 아닌 괄호`()`로 대체할 수 있다. but, `return` 이전에 **다른 코드가 있다면 일반 괄호 사용 불가**
* `return` 문이 한 줄이라면 괄호도 생략 가능
* 인수가 딱 하나라면 인수의 괄호도 생략 가능

---

## 객체

### 접근, 추가, 삭제

```javascript
const superman = {
  name : 'clark',
  age : 33,
}
```

> **접근**

```javascript
superman.name
superman['age']
```

> **추가**

```javascript
superman.gender = 'male';
superman['hairColor'] = 'black';
```

> **삭제**

```javascript
delete superman.hairColor;
```


### 단축 프로퍼티

다음과 같은 변수가 있다고 하자.

```javascript
const name = 'clark';
const age = 33;
```

그리고 이 변수의 값을 객체에 담는다고 할 때 다음과 같이 단축하여 작성할 수 있다.

```javascript
const superman ={
  name, //name : name,
  age,  //age : age,
  gender : 'male',
}
```

### 프로퍼티 존재 여부 확인

* 만약 존재하지 않는 프로퍼티에 접근한다면, Error가 발생하는 것이 아니라 undefined가 출력된다.
`superman.birthDay; //undefined`

* in을 사용하자.
`'birthDay' in superman; // false`
`'age' in superman; // true`

in을 사용하게 되는 경우는 어떤 값이 넘어올지 확신할 수 없을 때 사용, 통신할 때나 API 받아올 때.

### for ... in : 객체 탐색
for ... in 문은 객체를 순회하며 값을 얻을 수 있다.

```javascript

const Mike = {
  name : 'Mike',
  age : 30,
};

for (x in Mike){
  console.log(x) // name age
}

for (x in Mike){
  console.log(Mike[x]) // Mike 30
}
```
여기서 x는 key 값을 뜻한다.

---

## 배열

* `push()`
배열 맨 뒤에 값 추가

* `pop()`
배열 맨 뒤에 값 제거

* `unshift()`
배열 맨 앞에 값 추가

* `shift()`
배열 맨 앞에 값 제거

`push()`와 `unshift()`는 여러 값을 추가할 수 있음

### for ... of : 배열 탐색

```javascript
let days = ['월', '화', '수'];

for (let day of days){
  console.log(day); // 월, 화, 수
}
```
만약 배열에서 `for ... of`가 아닌 `for ... in` 문을 사용하는 경우에는 키 값에 해당하는 index가 출력된다.

```javascript
let days = ['월', '화', '수'];

for (let day in days){
  console.log(day); // 0, 1, 2
}
```
