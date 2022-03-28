---
layout: post
title: Javascript Intermediate
image:
  path: /assets/img/thumbnail/javascript.png
description: >
  자바스크립트 중급
sitemap: false
categories:
  - study
  - javascript

---
# 자바스크립트 중급

* toc
{:toc .large-only}

## 생성자 함수

객체를 다음과 같이 생성할 수 있다.
### 객체 리터럴
```javascript
let user = {
  name : 'Ryan',
  age : 30,
}
```
그런데, 이러한 객체를 여러 개 만들어야 하는 상황이 온다면 어떨까?
=> <mark>생성자 함수를 쓰자</mark>

### 생성자 함수 구조
* 함수 **첫 글자**는 **대문자**
* `new`연산자를 사용해서 호출

```javascript
function User(name, age){
  this.name = name;
  this.age = age;
}

let user1 = new User('Mike', 30);
let user2 = new User('Ryan', 26);
let user3 = new User('Tom', 20);
```

### 생성자 함수 동작
1. 빈 객체를 만들고 this에 할당 `this = {}`
2. Properties를 추가
3. this를 반환 `return this`

* 1,3은 실제 코드에는 없지만 new를 붙여 실행하면 위와 같은 알고리즘으로 동작한다.
* new를 붙이지 않고 그냥 함수로서 실행한다면 return값이 없어서 `undefined`가 출력될 것이다.

---

## 객체 메소드

#### 1. Object.assign() : 객체 복제

객체는 다음과 같이 복제되지 않는다. 새로운 변수를 선언하고 객체명을 할당해주면 객체 자체가 복제되는 것이 아니라 객체가 저장되어있는 메모리 주소인 참조값이 저장된다.
```javascript
const user = {
  name : 'Ryan',
  age : 30,
}

const cloneUser = user;
```

즉 `user`와 `cloneUser` 둘 다 같은 메모리주소를 참조하고 있기 때문에 cloneUser에서 name 프로퍼티의 값을 변경한다면 user에서 name 프로퍼티를 출력했을 때 값이 변경되어있겠다.
객체 자체를 복제하기 위해서는 `Ojbect.assign()`메소드를 사용해야한다.

```javascript
const newUser = Object.assign({}, user); // {} 빈 객체는 초기값, user가 빈 객체에 병합됨.
```
첫 매개 변수에는 초기값을 할당할 수 있고, 다음 매개 변수에 들어오는 인자들은 초기값에 병합된다.


#### 2. Object.keys() : 키 배열 반환
```javascript
const user = {
  name : 'Ryan',
  age : 30,
}
Object.keys(user); // ["name", "age"]
```

#### 3. Object.values() : 값 배열 반환
```javascript
const user = {
  name : 'Ryan',
  age : 30,
}
Object.keys(user); // ["Ryan", 30]
```

#### 4. Object.entries() : 키,값 배열 반환
```javascript
const user = {
  name : 'Ryan',
  age : 30,
}
Object.entries(user); // [ ["name", "Ryan"], ["age", 30] ]
```

#### 5. Object.fromEntries() : 키,값 배열을 객체로
```javascript
const arr = [ ["name", "Ryan"], ["age", 30] ];

Object.fromEntries(arr); // { name : 'Ryan', age : 30}
```
---

## 계산된 프로퍼티 (computed property name)
computed property name은 표현식(변수, 함수 등)을 이용해 객체의 `key` 값을 정의하는 문법이다.
[여기](https://velog.io/@yujuck/object-key%EC%97%90-%EB%B3%80%EC%88%98%EB%A5%BC-%EB%84%A3%EC%9C%BC%EB%A0%A4%EB%A9%B4-Computed-Property-Name) 이 글에서 객체에 템플릿 리터럴이 동작하지 않는 것으로부터 의문을 품어 computed property name을 학습하게 된 내용을 살펴볼 수 있었다. 그리고 제시해주신 예제를 보면서 활용성에 대해서 이해할 수 있었다.

```javascript
const studentId = 20160733;
function func1(a, b) {
  return a + b;
}
function func2() {
  return 'hello';
}

let obj = {
  [`${studentId}name`] : "Ryan",
  [`key${func1(5,8)}`] : 'result is 13',
  [func2()] : 'hi'
}

// obj = {
//   20160733name : 'Ryan',
//   key13 : 'value is 13',
//   hello: 'hi'
// }
```
또한 어떤 것이 `key`가 될 지 모르는 객체를 생성할 때 유용하게 쓰일 수 있다고 한다.
```javascript
function makeObj(key, val) {
  return {
    [key] : value,
  };
}

const obj = makeObj("성별", "male"); // {성별 : "male"}
```
---

## 심볼 (Symbol)

객체의 프로퍼티 키는 문자형이 될 수 있고, Symbol형이 될 수 있다.
Symbol은 유일한 식별자를 만들 때, 사용할 수 있는데 이것이 심볼 데이터 형식의 유일한 목적이다.

```javascript
const a = Symbol();
const b = Symbol();

console.log(a===b); // false
console.log(a==b);  // false
```
위의 예시처럼 Symbol()은 고유의 심볼값을 반환하기에 a와 b가 같지 않다는 결과를 표시한다.

Symbol은 선택적으로 문자열을 매개 변수를 받는데, 이는 디버깅할 때에 도움을 받을 수 있는 설명을 기입할 수 있는 것으로 이해할 수 있다. 동일한 description으로 작성했다고 하더라도 Symbol값은 유일하다. (**유일성 보장**)

> 객체의 Key가 Symbol형 인 경우에는 Object.values, Object.keys 등으로 조회되지 않는다.

### Symbol.for() : 전역 심볼
* 하나의 심볼만 보장받을 수 있음
* 없으면 만들고, 있으면 가져옴
* Symbol 함수는 매번 다른 Symbol 값을 생성하지만, Symbol.for 메소드는 하나를 생성한 뒤 키를 통해서 같은 Symbol을 공유

```javascript
const id1 = Symbol.for('id');
const id2 = Symbol.for('id');

console.log(id1 === id2); //true
```
id1을 생성할 때 매겨변수로 전달했던 description을 확인하고 싶으면
`Symbol.keyFor(id1)`으로 확인 가능하다.
전역 심볼이 아닌 경우에는
`변수명.Symbol.description`으로 확인할 수 있다.

---

## 숫자, 수학 관련 메소드

### toString()

toString은 문자열로 변환해주는 메소드라고 알고 있었는데,
**10진수 -> 2진수/16진수** 변환도 가능하다.

```javascript
let num = 10;

// 2진수
num.toString(); //"10"
num.toString(2); //"1010"

// 16진수
let num = 255;
num.toString(16); //"ff"
```

### Math.ceil() : 올림
### Math.floor() : 내림
### Math.round() : 반올림
```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.round(num1) // 5
Math.round(num2) // 6
```
> **내가 원하는 소수점 자리에서 반올림하려면 어떻게 해야할까?**
만약 소수점 둘째자리까지 표현(셋째 자리에서 반올림)해달라고 한다면 다음과 깉이 할 수 있다.

```javascript
Math.round(value * 100) / 100
```
### Math.random()
0에서 1 사이의 무작위 숫자 생성
> **만약 특정 범위 내 값을 뽑고 싶다면?**
식을 작성해서 추출해야한다.
0~100 사이 임의값 = `Math.floor(Math.random()*100)+1`

### Math.max(), Math.min() : 최대값, 최소값
Math.max()와 Math.min()은 각각 괄호 안의 숫자 나열에서 가장 큰 값과 작은 값을 반환한다.
괄호 안에 배열을 넣으면 `NaN`을 반환하는데, `...`스프레드 연산자를 사용해서 배열을 넣어주면 출력할 수 있다.
```javascript
const array = [1,2,3,4,5,-1];

console.log(Math.max(array)) // NaN
console.log(Math.max(...array)) // 5
```

### toFixed() : 소수점 자리수
3에서 살펴본 것처럼 소수점 자리에 대한 명확한 요구사항이 있다면 toFixed를 사용하는 것이 더 좋다. 인자로 원하는 자리수를 넘겨주면 해당 자리수가 되도록 반올림한다. 만약 해당 자리수에 값이 없다면 0으로 채운다.
> **주의** : `toFixed`는 **문자열을 반환**한다.

### isNaN() (Math 아님)
NaN은 `==` 나 `===`로 판별할 수 없다. `isNaN`만이 NaN을 판별할 수 있다.

### parseInt()
문자를 만날 때까지 숫자를 parsing하여 반환함.
```javascript
let margin = '10px';
parseInt(margin); // 10
Number(margin) //NaN
```
문자열에 포함된 모든 숫자를 parsing하는 것이 아니라 처음부터 읽어오기 때문에 처음이 문자면 `NaN`을 반환한다.

그러나 parseInt는 다른 진수 (2진수 16진수)로 변환할 수도 있다.
```javascript
let redColor = 'f3';
parseInt(redColor); //NaN

parseInt(redColor, 16); //243
```
---

## 문자열 메소드

### toUpperCase()
모든 문자를 대문자로 변환

### toLowerCase()
모든 문자를 소문자로 변환

### str.indexOf(text)
- `str.indexOf(text)`는 str에서 text가 위치하고 있는 index 번호를 반환한다.
- 만약 str에 text가 여러 개 존재한다면 가장 앞에 위치한 text의 index 번호를 반환한다
```javascript
a = "aaabbb";
console.log(a.indexOf('a')); // 0
```
- 만약 포함되어있지 않다면 `-1`을 반환하기 때문에 만약 문자열에 글자 포함여부를 확인하려거든 indexOf의 반환값이 `-1`보다 큰 지 확인해보면 된다.

### str.includes(text)
문자열의 포함여부를 판단해주는 메소드로 포함되어있으면 true, 포함되어있지 않으면 false를 반환한다.

### str.slice(n, m)
- 문자열의 특정 부분만 잘라서 반환해주는 메소드이다.
- n은 시작점, m은 종료지점인데, m이 없으면 문자열의 끝을 종료지점으로 보고 m이 양수이면 해당 숫자까지(해당 숫자는 포함X), m이 음수면 끝에서부터 센 수까지(해당 숫자는 포함X)이다.

### str.substring(n, m)
- 음수는 허용하지 않으며, 문장열의 인덱스 n과 m 사이의 값을 반환한다.
- n과 m을 바꿔서 작성해도 동작한다.

### str.substr(n, m)
- n부터 시작해서 m개의 값을 반환함

### str.trim()
- 맨 앞과 맨 뒤의 공백 제거

### str.repeat(n)
- 문자열을 n번 반복

---

## 배열 메소드

### arr.splice(n, m) : 특정 요소 삭제
- index n으로부터 m개 제거
- 반환값은 arr에서 제거한 요소들이다.

> **arr.splice(n, m, x) : 특정 요소 지우고 요소 추가**
세 번째 인자부터 추가하는 요소들은 특정 요소를 지우고 추가될 요소들이다.

만약에 삭제하는 요소가 0개이고 추가하는 요소들이 있다면 n이 가리키고 있는 Index 앞에 값이 추가된다.
```javascript
let arr = ["나는", "Ryan", "입니다"];
arr.splice(1, 0, "개발자");

console.log(arr) // ["나는", "개발자", "Ryan", "입니다"]
```

### arr.concat(arr2, arr3 ...) : 합쳐서 새 배열 반환
```javascript
let arr = [1];
arr.concat([2]); // [1,2]
arr.concat([3]); // [1,2,3]
```

### arr.forEach(fn) : 배열 반복
forEach에는 인자로 함수를 작성하게 되는데,
함수의 첫 번째 인자는 item, 두 번째는 index, 세 번째는 배열 자체를 의미한다.
다음과 같이 작성할 수 있다.
```javascript
let arr = ["Mike", "Tom", "Jerry"];

arr.forEach((name, index) => {
  console.log(`${index+1}. ${name}`); // 1. Mike 2. Tom 3. Jerry
})
```

### arr.indexOf / arr.lastIndexOf
- 문자열에서의 indexOf와 동일하게 인자로 넘겨준 값의 index를 반환한다.
- 인자를 두 개 넘겨주는 경우, 두 번째 인자는 탐색 위치를 지정해준다. 즉, `arr.indexOf(3,3)`은 3 이라는 수가 arr의 index 3 부터 탐색했을 때 어디에 위치하고 있는지 알고 싶은 것이다.
- `lastIndexOf`는 뒤에서부터 탐색한다.

### arr.find(fn) / arr.findIndex(fn)
indexOf와 비슷한 역할을 하지만 함수를 작성해서 조건을 작성하여 찾고자 하는 요소를 찾아낼 수 있다. 다음과 같이 배열이 객체를 가지고 있는 경우에 활용하기 좋다. **단, 처음 찾는 값만 반환한다.**

```javascript
let userList = [
  { name : "Mike", age: 30},
  { name : "Tom", age: 27},
  { name : "Jerry", age: 10},
];

const result = userList.find((user) => {
  if (user.age < 19){
    return true; // 결과적으로 true가 리턴된 값을 result에 반환하게 된다.
  }
  return false;
})
```
만족하는 모든 요소를 반환하기 위해서는 filter를 사용할 수 있다.

### arr.filter(fn)
find와 동일하게 사용할 수 있으나 함수에서 작성한 조건에 만족하는 모든 값이 배열로 반환된다.
```javascript
let userList = [
  { name : "Mike", age: 30},
  { name : "Tom", age: 27},
  { name : "Jerry", age: 10},
];

const result = userList.filter((user) => {
  if (user.age > 19){
    return true; // 결과적으로 true가 리턴된 값을 result에 반환하게 된다.
  }
  return false;
});

console.log(result)
```
**결과**
```javascript
[
  {
    "name" : "Mike",
    "age", 30
  },
  {
    "name" : "Tom",
    "age" : 27
  },
]
```

### arr.reverse() : 역순으로 정렬

### arr.map(fn)
함수를 받아서 특정 기능을 시행하고 새로운 배열을 반환한다.
userList를 가지고 있는데, 이를 토대로 새로운 userList를 만들고 싶을 때 map을 활용해서 다음과 같이 작성해 줄 수 있다.

```javascript
let userList = [
  { name : "Mike", age: 30},
  { name : "Tom", age: 27},
  { name : "Jerry", age: 10},
];

let newUserList = userList.map((user, index) => {
  return Object.assign({}, user, {
    id: index + 1,
    isAdult: user.age > 19,
  });
});

console.log(newUserList);
```

**결과**
```javascript
[
  {
    "name" : "Mike",
    "age", 30
  },
  {
    "name" : "Tom",
    "age" : 27
  },
  {
    "name" : "Jerry",
    "age" : 10
  }
]
```

### arr.join()
인자로 전달한 값으로 배열의 값들을 구분하여 문자열 하나로 병합하여 반환한다.
인자를 전달하지 않으면 기본적으로 쉼표로 구분하여 값을 병합한다.

### arr.split()
join과 반대로 문자열을 인자로 전달한 값을 기준으로 쪼개서 배열로 반환한다.
인자를 전달하지 않으면 기본적으로 문자 단위(공백 포함)로 쪼갠다.

### Array.isArray()
기본적으로 `typeof()` 메소드로 타입을 구분해줄 수 있지만 객체와 배열은 `typeof` 메소드 반환값이 object로 동일하기 때문에 구분할 수 없다.
그래서 `Array,isArray()`를 쓴다.

### arr.sort()
- 기본적으로 인자없이 사용 시 배열을 문자열 기준으로 재정렬해준다. 따라서 숫자가 담긴 배열을 오름차순으로 정렬하는 것을 보장하지 못한다.
- 숫자가 담긴 배열을 오름차순으로 정렬하기 위해서는 인수로 정렬 로직을 담은 함수를 받아야 한다.

```javascript
let arr = [27, 8, 5, 13];

arr.sort((a, b) => {
  return a - b;
});
```
a와 b를 비교하여 다음과 같이 정렬이 이뤄진다.
- 반환값이 0보다 작은 경우 a를 b앞에 정렬
- 반환값이 0보다 큰 경우 b를 a앞에 정렬
- 0일 경우, 그대로

arr.sort()는 직접 정렬 로직을 작성해야하기 때문에 어렵다.
그래서 `Lodash`라는 라이브러리를 많이 사용한다고 한다.
[Lodash](https://lodash.com) <- 공식사이트 참조


### arr.reduce()
reduce 메소드는 배열의 각 요소에 대해 주어진 `reducer` 함수를 실행하고, 결과값 하나를 반환한다.

reduce 메소드는 두 개의 인자를 가질 수 있다.
- callback (reducer 함수)
- initialValue - optional
  callback의 최초 호출에서 첫 번째 인수에 제공하는 값

reducer 함수는 네 개의 인자를 가진다.
- 누산기 (acc)
- 현재 값 (cur)
- 현재 인덱스 (idx) - optional
- 원본 배열 (src) - optional
리듀서 함수의 반환 값은 누산기에 할당되고, 누산기는 순회 중 유지되므로 결국 최종 결과는 하나의 값이 된다.

이러한 특성을 이용해서 배열의 모든 수를 합한 값을 출력할 수 있다.
```javascript
let arr = [1,2,3,4,5];

const result = arr.reduce((prev, cur) => {
  return prev + cur;
}, 0)
console.log(result); // 15
```
