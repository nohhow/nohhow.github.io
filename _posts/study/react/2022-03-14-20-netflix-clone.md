---
layout: post
title: (To-do-List) Project Optimization with React.memo
image:
  path: https://image.tmdb.org/t/p/original/wwemzKWzjKYJFfCeiB57q3r4Bcm.svg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# Netflix Clone (with React)

* toc
{:toc .large-only}

## 활용 기술 및 API
1. HTML
2. CSS
3. Javascript
4. React
5. The Movie DB API

## 개발 순서
1. The Movie DB API 세팅
2. 기본 골격 잡기


---


## The Movie DB API 활용
[themoviedb.org](https://themoviedb.org)

### API URL

1. GET Movie BY Latest
```
https://api.themoviedb.org/3/movie/latest?api_key=<api_key>
```

2. GET Movie Detail
```
https://api.themoviedb.org/3/movie/{movie_id}?api_key=<api_key>

```

3. GET Movie Reviews
```
https://api.themoviedb.org/3/movie/{movie_id}/reviews?api_key=<api_key>
```

4. GET Images
```
https://image.tmdb.org/t/p/original/wwemzKWzjKYJFfCeiB57q3r4Bcm.svg
```
* original은 이미지 사이즈를 말함. w500과 같은 값을 줘서 이미지 크기 조절하여 호출가능


### The Movie DB API 요청을 위한 Axios 인스턴스 생성 및 요청 보내기

> **인스턴스란?**
비슷한 특징을 가진 여러 개의 객체를 만들기 위해서 생성자 함수(Constructor)를 만들어 양산할 수 있는데, 이 생성자 함수로부터 생성된 객체를 인스턴스라 부른다고 한다. 객체지향언어에서 흔히 사용되는 클래스(Class)가 자바스크립트에서는 프로토타입(prototype)이며 생성자 함수가 사용된다.

인스턴스화가 필요한 이유는 API를 다양하게 호출할텐데, 그 때마다 계속해서 반복되는 코드, 문장의 작성을 줄이기 위해서이다.

#### Axios 란?
* Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 **HTTP 비동기 통신** 라이브러리이다.

> **요약**
서버에 데이터 요청을 보내기위해서는 통신을 보내야 하는데, 이를 가능하게 해주는 것이 Axios이다.
npm 방식이나 cdn 방식으로 사용가능하다.

> **비동기 통신 이란?**
비동기 방식 : 웹페이지를 리로드 하지 않고, 데이터를 불러오는 방식이다. 서버에 요청을 보내고 멈춰있는 것이 아니라 그 프로그램이 계속 돌아가고 있다.

* 설치
`npm install axios --save`

#### Axios 인스턴스화

1. 인스턴스 생성할 폴더 파일 생성
* src
  * api folder
    * axios.js
    * requests.js

2. 인스턴스 사용자 Config 작성
axios는 사용자 지정 config로 새로운 Axios 인스턴스를 만들 수 있다.

```javascript
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

이를 활용해서 다음과 같이 the Movie DB axios 인스턴스 생성

```javascript
// axios.js
import axios from "axios";

const instance = axios.create({
    baseURL : "https://api.themoviedb.org/",
    params : {
        api_key: "e14409facdc2c58de314693efe970e32",
        language: "ko-KR",
    },
});

export default instance;
```

또한 다음과 같이 서버에 보낼 요청들을 객체화하여 복잡한 코드들을 간소화하여 사용할 수 있게 한다.

```javascript
// requests.js
const requests = {
    fetchNowPlaying : "movie/now_Playing",
    fetchNetflixOriginals : "/discover/tv?with_networks=213",
    fetchTrending: "/trending/all/week",
    fetchTopRated: "/movie/top_rated",
    fetchActionMovies: "/discover/movie?with_genres=28",
    fetchComedyMovies: "/discover/movie?with_genres=35",
    fetchHorrorMovies: "/discover/movie?with_genres=27",
    fetchRomanceMovies: "/discover/movie?with_genres=10749",
    fetchDocumentaries: "/discover/movie?with_genres=99",
}

export default requests;
```

## 기본 골격 잡기
* NavBar
* Banner
* Rows
  * Row
  * Row
* Footer

각 항목은 component로 생성하여 관리
