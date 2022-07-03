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
---

## 구조 분해 할당 Destructuring assignment

구조 분해 할당 구문은 배열이나 객체의 속성을 분해해서 그 값을 변수에 담을 수 있게 하는 표현식이다.

### 배열 구조 분해

**기본 구조**
```javascript
let users = ["Mike", "Den", "Ryan"];
let [user1, user2, user3] = users;

console.log(user1, user2, user3); // Mike Den Ryan
```

**기본값 부여**
할당될 값이 없을 때 undefined가 할당되는데, 이를 방지하기 위해서 기본값을 부여해줄 수 있다.
할당되는 값이 기본값보다 우선임.
```javascript
let [a=3, b=3, c=3] = [1, 2]; // c=3을 기본값으로 부여하지 않았다면 undefined가 할당될 것임

console.log(a, b, c); // 1 2 3
```
**반환값 무시**
반환값을 건너뛰고자한다면 `공백 + ,`로 해당 위치의 값을 무시할 수 있다.
```javascript
let [user1, ,user2] = ["Mike", "Den", "Ryan"];
console.log(user1, user2); //Mike Ryan
```

**바꿔치기**
```javascript
let a = 1;
let b = 2;

[a, b] = [b, a];
console.log(a,b); //2 1
```

### 객체 구조 분해
**기본 구조**
```javascript
let user = {name : "Mike", age: 30};
let {age, name} = user;

console.log(name, age); // Mike 30
```

**새로운 변수 이름으로 할당**
```javascript
let user = {name : "Mike", age: 30};
let {age:userAge, name:userName} = user;

console.log(userName, userAge); // Mike 30
```
**기본값 부여**
배열에서와 마찬가지로 할당되는 값이 없을 때 기본값으로 할당될 값을 지정해줄 수 있다. 기본값이 있다고 하더라도 할당되는 값이 우선임.
```javascript
let user = {
  name : 'Mike',
  age: 18
};

let {name, age, gender ='male'} = user;
console.log(gender); // 'male'
```
---

## 나머지 매개변수, 전개 구문

함수에 값을 전달하는 방법으로 전통적인 방식으로 arguments를 사용하였으나 최근(es6)에는 나머지 매개 변수를 많이 사용하는 추세이다.

> **arguments**
- 함수로 넘어 온 모든 인수에 접근
- 함수내에서 이용 가능한 지역 변수
- length / index
- Array 형태의 객체
- 배열의 내장 메서드 없음

```javascript
function showName(name){
  console.log(arguments.length);
  console.log(arguments[0]);
  console.log(arguments[1]);
}

showName('Mike', 'Tom');
//2
//'Mike'
//'Tom'
```

### 나머지 매개변수
정해지지 않은 갯수의 인수를 배열로 나타낼 수 있게 한다.
나머지 매개 변수는 매개 변수들 중 가장 마지막에 위치해야한다.
```javascript
function showName(...names){
  console.log(names);
}

showName(); // []
showName('Mike'); // ['Mike']
showName('Mike', 'Tom'); // ['Mike', 'Tom']
```

### 전개 구문 Spread Syntax

#### 배열에서
```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];

let result = [...arr1, ...arr2];
console.log(result); // [1,2,3,4,5,6]
```

#### 객체에서
```javascript
let user = {name:'Mike'};
let mike = {...user, age:30};

console.lgo(mike); // {name: "Mike", age : 30}
```
`Object.assign`을 사용하지 않아도 객체를 복제할 수도 있다.
```javascript
let user1 = {name : 'Mike', age: 30};
let user2 = {...user1}

user2.name = 'Den';
// 원본 값은 그대로 두고 복제된 것을 확인할 수 있다.
console.log(user1); // {"name" : "Mike", "age" : 30}
console.log(user2); // {"name" : "Den", "age" : 30}
```

---

## 클로저 Closure

> **함수와 렉시컬 환경의 조합**

클로저는 함수와 함수가 선언된 어휘적 환경의 조합이다.
함수가 처리되기 위해서 함수 안의 지역 변수들은 처리되는 동안 존재하는데, 클로저가 형성되면 이 때 생성된 지역 변수들을 참조하며 값을 저장하고 있게 된다.

그래서 다음과 같이 서로 다른 맥락(어휘)적 환경을 저장한 `add5`, `add10`는 같은 함수를 통해서 생성되었지만 저장된 값이 다르기 때문에 다른 값을 출력하는 것을 볼 수 있다.
```javascript
function makeAdder(x) {
  var y = 1;
  return function(z) {
    y = 100;
    return x + y + z;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);
//클로저에 x와 y의 환경이 저장됨

console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
console.log(add10(2)); // 112 (x:10 + y:100 + z:2)
//함수 실행 시 클로저에 저장된 x, y값에 접근하여 값을 계산
```


이런 예시도 있다.

```javascript
function makeCounter() {
  let num = 0;

  return function () {
    return num++;
  };
}

let counter = makeCounter();

console.log(counter()); //0
console.log(counter()); //1
console.log(counter()); //2

```

위와 같은 경우에는 `num`을 **은닉화**한 것으로, `counter()`를 호출할 때마다 `num`의 값이 참조되기 때문에 값이 증가하는 것을 알 수 있는데, 이 값은 외부에서 수정할 수 없다. 이를보고 은닉했다고 이야기하는 것 같다.

함수 렉시컬 환경에서 `num`이 `++` 되는 것이기 때문에 다음과 같이 변경하더라도 참조되는 num값이 증가하기 때문에 동일한 현상(?)을 파악할 수 있었다.

```javascript
function makeCounter(){
  let num = 0

  return function(k){
    return num++ + k
  }
}

let counter = makeCounter()
console.log(counter(1)) //1
console.log(counter(1)) //2
console.log(counter(1)) //3
```

개념 자체가 어려운 것은 아니지만 실제로 어떻게 사용할지 알아봐야겠다.

---

## setTimeout / setInterval : 스케줄링

### setTimeout
setTimeout은 일정 시간 뒤에 동작을 실행시켜주는 함수이다.
기본적으로 매개 변수를 2개 받는데, 첫 번째는 함수, 두 번째는 지연시킬 시간을 ms단위로 입력 받는다.
추가로 함수가 매개변수를 취하는 경우, 3번째 매개 변수로 인수를 둘 수 있다.

```javascript
funciton fn(){
  console.log(3)
}

setTimeout(fn, 3000);
```
setTimeout이 반환하는 id를 입력받아 `clearTimeout()`를 실행하면 setTimeout에 의해 예정된 동작을 없앨 수 있다.

### setInterval
`setTimeout`은 한 번만 수행하는 것과 다르게 `setInterval`은 시간마다 반복적으로 수행한다.
마찬가지로 중단하기 위해서는 `clearInterval()`을 실행하면 된다.

---

## call, apply, bind

함수 호출 방식과 관계없이 this를 지정할 수 있다.

### call

모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있다.
해당 함수가 주어진 객체의 메서드인 것처럼 사용할 수 있다.

```javascript
const ryan = {
  name : "Ryan",
  age : 26
}

function showName() {
  console.log(this.name);
}

showName(); // ""
showName.call(ryan); // Ryan
```

### apply

apply는 call과 사용하는 방식이 거의 동일하나, 사용하는 함수에 추가적으로 매개변수를 전달해야하는 경우, call은 직접 입력받지만, apply는 매개변수를 배열로 받는다.

```javascript
const ryan ={
  name : "Ryan"
}

function update(number, age) {
  this.phoneNumber = number;
  this.age = age;
}

//update.call(ryan, "01011112222", 26) //아래와 동일한 동작
update.apply(ryan, ["01011112222", 26])
```

### bind

함수의 this 값을 영구히 변경할 수 있다.

```javascript
const user ={
  name : "Ryan",
  showName : function() {
    console.log(`hello ${this.name}`);
  }
}

user.showName(); // hello Ryan

let fn = user.showName;

fn(); // hello

// bind 사용해서 함수 생성
let boundFn = fn.bind(user);

boundFn(); // hello Ryan
```

---

## 상속, Prototype

### prototype
객체에서 프로퍼티를 읽으려고 할 때, 없으면 `__proto__`에서 찾게 된다.
즉 다음과 같이 hasOwnProperty 라는 프로퍼티를 임의로 생성해주면 __proto__의 hasOwnProperty를 읽어오는 것이 아니라 임의로 생성해준 hasOwnProperty를 읽는다.

```javascript
const user = {
  name : 'Ryan',
  hasOwnProperty : function(){
    console.log('hi');
  }
}
user.hasOwnProperty() // hi
```

이러한 특성을 이용해서 객체가 동일 속성을 갖는 상황에서 동일 속성에 대해서 한 번만 작성하고 상속해줄 수 있다.

가장 흔한 예제 자동차 3사

```javascript
// 상속할 특성 car
const car = {
  wheels: 4,
  drive() {
    console.log("drive..");
  }
};

const bmw = {
  color: "red",
  navigation: 1,
};

const benz = {
  color : "black",
};

const audi = {
  color : "blue",
};

bmw.__proto__ = car;
benz.__proto__ = car;
audi.__proto__ = car;

console.log(audi.wheels) // 4
// 그렇다고 기존에 가지고 있던 __proto__가 사라지는 것은 아니었습니다..!
console.log(audi.hasOwnProperty('color')) // true
```

`__proto__`를 이용해서 상속해버리면 기존에 `hasOwnProperty`와 같은 메서드는 사라지는게 아닐까? 걱정했는데 다음과 같이 중첩되는 방식으로 `prototype`이 쌓이는 듯 하다.

<img width="382" alt="스크린샷 2022-06-28 오후 9 21 51" src="https://user-images.githubusercontent.com/61059893/176177277-b3c25ded-ea7c-4870-b517-e417c683ec0a.png">

객체 자신에게서 property가 있는지 확인하고 있으면 해당 값을 우선 참조하고 없으면 prototype에서 찾아서 참조한다는 것을 이해하면 상속으로 인해서 property가 겹칠 때 어떤 값을 참조하게 될지는 충분히 생각할 수 있다. (=prototype chain

### for in 문 과 prototype
for in 문을 사용하면 상속받은 property 항목을 모두 출력할 수 있다.

```javascript
const user = {
  name : "Ryan"
}

const person = {
  leg : 2
}

user.__proto__ = person
for (p in user){
  console.log(p); // name leg
}
```

위 상황에서 Object.keys(user) 나 Object.values(user)의 경우는 어떤 결과를 나타낼까?

```javascript
Object.keys(user); // ['name']
Object.values(user); // ['Ryan']
```

=> 상속받은 property는 제외하고 본인의 property만을 출력한다.


### 생성자와 prototype

생성자를 사용해서 객체를 생성하는 경우에는 다음과 같이 prototype을 상속시킬 수 있다. (중복 코드 줄일 수 있다.)

```javascript
const Bmw = function (color){
  this.color = color;
}

Bmw.prototype.wheels = 4;
Bmw.prototype.drive = function(){
  console.log("drive.");
}

const x5 = new Bmw("red");
const z4 = new Bmw("blue");

// x5.__proto__ = car
// z4.__proto__ = car
```

### constructor를 보장하지 않는 javascript

위에서 작성한 코드를 다음과 같이 작성할 수도 있는데 이는 생성자로 생성된 인스턴스의 constructor가 맞는가? 라는 조건문에서 false를 반환하게 된다.

```javascript
const Bmw = function(color){
  this.color = color;
}

Bmw.prototype = {
  wheels: 4,
  drive() {
    console.log("drive.");
  }
}

const x5 = new Bmw("red");

console.log(z4.constructor === Bmw); // false
```
Bmw.prototype의 property로 constructor를 Bmw라고 명시해주는 방식으로 해결할 수 있다. 또는 위에서 사용한 방법을 사용하지 않고 일일히 명시해주면 된다.

---

## 클래스 class

원래 객체를 생성하는 방법

```javascript
const User = function (name, age){
  this.name = name;
  this.age = age;
  this.showName = function(){
    console.log(this.name);
  }
}

const mike = new User("Mike", 30);
```

es6에 추가된 class를 통해서 생성하는 방법

```javascript
class User2 {
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
  showName() {
    console.log(this.name);
  }
}

const tom = new User2("Tom", 19);
```

### 기존 객체 생성 방식과 class 객체 생성 방식의 차이

> **첫 번째**
* 기존 방식으로 객체를 생성한 `mike`는 `showName` 메서드가 객체 내부에 있는 반면에
* class로 생성한 객체인 `tom`은 `showName`이 prototype 내부에 있다.


> **두 번째**
* 기존 방식으로 객체를 생성했을 때, new 키워드를 뺴먹었을 때 에러가 발생하지 않고 undefined가 반환된다.
* class를 사용했을 때는 new 키워드를 빼놓고 작성하면 에러가 난다. (디버깅에서 유리)
-> constructor에 class라고 명시되어있기 때문에 이를 검사하게 된다.

> **세 번째**
* 기존 방식에서는 for in 문을 활용해서 상속받은 property를 확인할 수 있다.
* class 방식에서는 for in 문에서 상속받은 property가 표시되지 않는다.

> **네 번째**
상속 방식에서 차이가 있다.

class에서는 extends라는 키워드를 사용한다.

```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log("drive.");
  }
  stop() {
    console.log("stop!");
  }
}

class Bmw extends Car {
  park(){
    console.log("park!");
  }
}

const z4 = new Bmw("blue");
```

### class 메소드 오버라이딩(method overriding)

상속받는 객체에서 동일한 프로퍼티 키워드로 값을 저장하면 이를 우선 참조하기 때문에 overriding된다.
그런데 부모의 값을 확장하여 사고 싶을 때는 `super` 키워드를 사용하면 된다.

```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log("drive.");
  }
  stop() {
    console.log("stop!");
  }
}

class Bmw extends Car {
  park(){
    console.log("park!");
  }
  // overriding
  stop(){
    super.stop();
    console.log("OFF");
  }
}

const z4 = new Bmw("blue");

console.log(z4.stop()); // STOP! OFF -> 부모의 stop과 overriding한 stop 모두 표시되는 것을 볼 수 있다.
```

### class 오버라이딩 (constructor overriding)

잘못된 오버라이딩 예시부터 살펴보면서 이해해본다.

> **잘못된 오버라이딩 예시 1**

```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log("drive.");
  }
  stop() {
    console.log("stop!");
  }
}

class Bmw extends Car {
  // overriding
  constructor(){
    this.navigation = 1;
  }
  park(){
    console.log("park!");
  }
}

const z4 = new Bmw("blue");
```
-> construtor를 오버라이딩 하기 위해서는 반드시 상속받는 객체의 construtor를 참조해야하기 때문에 `super()` 키워드를 사용햏야한다.

> **잘못된 오버라이딩 예시 2**
위의 실수를 만회하고자 super()를 사용했다.

```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log("drive.");
  }
  stop() {
    console.log("stop!");
  }
}

class Bmw extends Car {
  // overriding
  constructor(){
    super();
    this.navigation = 1;
  }
  park(){
    console.log("park!");
  }
}

const z4 = new Bmw("blue");
console.log(z4) // color : undefined navigation:1 wheels:4
```
-> color 값이 사라졌다! blue라는 값이 제대로 동작하기 위해서는 Car에서와 마찬가지로 overriding하는 객체에서도 매개변수로 color를 받아서 상속받는 객체로 넘겨줘야한다.

> **제대로된 오버라이딩**

```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log("drive.");
  }
  stop() {
    console.log("stop!");
  }
}

class Bmw extends Car {
  // overriding
  constructor(color){
    super(color);
    this.navigation = 1;
  }
  park(){
    console.log("park!");
  }
}

const z4 = new Bmw("blue");
console.log(z4) // color :"blue" navigation:1 wheels:4
```
-> 여기에는 숨은 사실이 있다. 상속받는 객체, 즉 자식 객체의 생성자는 반드시 부모 객체의 생성자를 호출해야한다.

constructor를 따로 overriding하지 않는 경우에 Bmw 객체는 다음과 같다. 이를 이해하면 오버라이딩 방식을 이해할 수 있다.

```javascript
class Bmw extends Car{
  construtor(...args){
    super(...args);
  }
  park() {
    console.log("park!")
  }
}
```
