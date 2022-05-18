---
layout: post
title: Portfolio site development memoir, with React
image:
  path: https://user-images.githubusercontent.com/61059893/157826432-582d4822-626a-4812-996b-93539f92c845.png
description: >
  포트폴리오 사이트 개발 회고
sitemap: false
categories:
  - study
  - react

---
# 포트폴리오 사이트 개발 회고 (with React) - 개발

* toc
{:toc .large-only}

**포트폴리오 개발 개요** 와 **기술 선정** ~ **기능 정의** (설계)에 대한 이야기는 [이전 글](https://nohhow.github.io/study/react/2022-03-11-19-portfolio-site-dev-memoir/)에 작성되어있습니다.


* 기술 선정
* 화면 설계
* 기능 정의
* **개발**
* **미디어별 대응 - 반응형**


### 개발

> **파일 구조**

기본 골조는 create-react-app 을 따른다.
추가로 생성한 부분은 src 파일 내에 components, pages, images 폴더 정도이다.

* components : 재활용성이 높은 컴포넌트들을 하위에 배치
* images : 이미지 파일들
* pages : router 주소에 따라서 보여질 큰 페이지 단위로 하위에 배치

~~~
/my-portpolio  - 프로젝트 폴더
ㄴ /node_modules
ㄴ /public
ㄴ /src
  ㄴ /components
  ㄴ /images
  ㄴ /pages
    ㄴ /MainPage
  ㄴ App.js
  ㄴ App.css
  ㄴ index.js
  ㄴ index.css
ㄴ package.json
~~~

> **네비게이션 바**

네비게이션 아이템은 다음 3가지로 구성
* About me
* Skills
* Projects

각 아이템 `click` 시 해당 `section`으로 스크롤 이동

별도의 Scroll 관련 동작을 작성하기 보다 `href="#id"`를 이용해서 새로고침 없이 해당 section으로 이동할 수 있게 하였다.

react-bootstrap 모듈에서 Navbar와 Nav를 호출해서 사용했다.
`import { Navbar, Nav } from "react-bootstrap";`

> **인트로**

![intro](/assets/img/blog/my-intro.png)
인트로에는 소개하는 글을 간략하게 담았고
하단으로 전개되는 것을 표시하기 위해서 하단 스크롤 유도 애니메이션을 삽입했다.

transition-timing-function의 각 함수 (ease, linear, ease-in, ease-out, ease-in-out, cubic-bezier, steps)를 이용해서 이미지 두개를 번갈아 깜빡이게 하였다.

```jsx
/* index.js */
<img
  className="d-inline-block blink"
  width="50rem"
  src={arrowSm}
  alt="arrow"
/>
<br />
<img
  className="d-inline-block blink-second"
  width="30rem"
  src={arrowSm}
  alt="arrow"
/>
```
```css
@keyframes blink-effect {
  50% {
    opacity: 0;
  }
}

.blink {
  margin-top: 5rem;
  animation: blink-effect 1s ease-in-out infinite;
}
.blink-second {
  animation: blink-effect 1s ease-in infinite;
}
```

> **자기소개**

![about-me](/assets/img/blog/my-about-me.png)

네비게이션과 마찬가지로 `react-bootstrap`의 grid 시스템에 의존해서 인적사항을 표현했다.

sm 사이즈 이하에서는 각 항목들이 한줄에 하나씩 표시될 수 있게 하였고 그 이상에서는 한줄에 3개씩 표시될 수 있도록 했다.

react-bootstrap에서는 jsx에 맞게 새로운 문법을 제공하는데 다음과 같이 Grid를 작성할 수 있었다.

```jsx
/* index.js */
<Container>
  <Row>
    <Col sm={4} className="about-me-col align-items-center">
      <h4 className="half-highlight">이름</h4>
      <span>노진현</span>
    </Col>
    ...
  </Row>
</Container>
```

> **기술 스택**

![skills](/assets/img/blog/my-skill.png)

당시에 컴포넌트화에 대해서 언제 어떻게 해야할지 제대로 고민하지 못했는데, 회고하는 시점에 다시 보니 기술 스택 data를 return 해주는 컴포넌트를 따로 생성했으면 어땠을까? 싶다.

기술 스택으로 표시될 데이터는 모두 객체 형태로 하드코딩 하여 작성했고, 자기소개 section과 마찬가지로 `react-bootstrap`의 `grid-system`을 이용해서 표현했다.

각 객체는 다음과 데이터를 가진다.
* **id** : 객체 구분 위함 (지금 보니 불필요해 보임)
* **icon** : 아이콘 이미지 url
* **title** : 기술명
* **rating** : 습득정도 표현(0~100)
* **isHover** : 각 Skill에 마우스 오버했을 때 rating 표시될 수 있게 하는데, 이 값이 true가 되면 Hover되었음을 의미

```javascript
const [skillData, setSkill] = useState([
{
  id: "1",
  icon: `${FaJs}`,
  title: "JavaScript",
  rating: 90,
  isHover: false,
},
...
]);
```

기술스택 data들은 state로 관리하여 각 스킬에 Hover했을 때 rating이 화면에 rendering될 수 있도록 하였다.

MouseOver와 MouseOut 이벤트를 핸들링 하기 위해서 다음과 같이 이벤트 핸들링 함수도 작성했다.

```javascript
const handleMouseOver = (id) => {
  let newSkillData = skillData.map((data)=>{
    console.log(id);
    if(data.id === id){
      data.isHover = true;
    }else{
      data.isHover = false;
    }
    return data;
  });
  console.log(newSkillData);
  setSkill(newSkillData);
};

const handleMouseOut = () => {
  let newSkillData = skillData.map((data)=>{
    data.isHover = false;
    return data;
  });

  setSkill(newSkillData);
}
```


> **프로젝트**

![projects](/assets/img/blog/my-project.png)


각 프로젝트는 `react-bootstrap`의 `Card` 모듈을 이용했고 각 `Card`는 `Card.Img` 와 `Card.Body`를 포함하도록 해서 프로젝트 Thumbnail 이미지와 프로젝트명, 프로젝트 간단 설명, 사용한 기술스택을 담았다.

각 프로젝트 카드를 클릭하면 프로젝트 세부 내용을 `modal`창으로 보여주도록 작성하고자 했다.
그런데 포트폴리오를 작성하는 당시가 리액트 프로젝트를 처음으로 작성해보는 것이라 구현 방식을 고민하다가 다른 방식으로 프로젝트 세부 내용을 보여줄 수 있게 했다.

다른 방식이라함은 projects section의 화면을 state로 관리하며 프로젝트가 클릭되면 projects card 화면에서 세부 화면으로 rendering 될 수 있도록 하였다.
구현된 프로젝트 상세 내용 화면은 다음과 같다.

![projects-detail](/assets/img/blog/my-project-detail.png)

프로젝트 카드와 세부내용에 표시되는 내용들은 모두 기술 스택들과 마찬가지로 객체로 하드코딩했다.

각 프로젝트마다 세부내용 화면에서 보여줘야할 사진이 많은데, 그 부분은 `react-bootstrap`의 `Carousel`모듈을 사용할까하다가 `react-slick`의 `Slider` 모듈을 사용했다.

<small>바닐라 javascript로 slick 모듈을 구현했던 것보다 편하게 구현할 수 있어서 놀랐고, react 생태계가 정말 편리하다고 느꼈던 순간이었다.</small>


### 미디어별 대응 - 반응형

미디어별 대응을 위해서 `react-bootstrap`에 많이 의존했다. 아무래도 grid-system이 잘 되어있다 보니 단순한 한 페이지짜리 포트폴리오를 만들 때 적합하다고 생각했다.

bootstrap의 힘이 닿지 않는 부분에는 별도로 bootstrap에서의 BreakPoint 기준에서 Medium 사이즈에 해당하는 768이하의 스크린 사이즈와 그 이상의 스크린 사이즈에 대해서만 구분하여 대응해주었다.

단순한 페이지이기 때문에 브레이크 포인트를 하나만 두었는데 PC와 Mobile에서 큰 어색함이 없었다.
