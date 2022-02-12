---
layout: post
title: Browser Rendering & Virtual Dom
image:
  path: /assets/img/blog/jeremy-bishop@0,5x.jpg
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---

# 브라우저 렌더링 원리와 가상돔
리액트의 주요 특징 중 하나는 가상돔(Virtual DOM)을 사용한다는 것이다.
가상돔이 무엇인지 알기 전에 가상돔을 '왜' 사용하는지 이해해야하는데, 브라우저가 렌더링하는 과정을 살피면서 이를 파악할 수 있다.

## 웹 페이지 빌드 과정(Critical Rendering Path CRP)

**웹 페이지 빌드 과정** : 웹 브라우저가 HTML 문서를 읽고, 스타일을 입히고 뷰포트에 표시하는 과정  

브라우저가 서버에서 페이지에 대한 HTML 응답을 받고 화면에 표시하기 전까지 여러 단계가 있다.  
단계는 이미지 참고

![CRP](https://dimension85.com/images/critical-render-path-large.jpg)
> 출처 : https://dimension85.com/glossary/critical-render-path

1. **DOM Tree 생성** : 렌더 엔진이 HTML문서를 읽고 그것을 파싱하여 어떤 내용을 페이지에 렌더링할 지 결정 [More. About DOM](https://poiemaweb.com/js-dom)
2. **Render Tree 생성** : 브라우저가 DOM과 CSSOM을 결합한다. 화면에 보이는 모든 콘텐츠와 스타일 정보를 모두 포함한 최종 렌더링 트리를 출력
3. **Layout(reflow)** : 브라우저가 페이지에 표시되는 각 요소의 크기와 위치를 계산하는 단계
4. **Paint** : 실제 화면에 그림

`여기서 문제 발생!!!`
어떤 인터렉션에 의해서 DOM에 변화가 생길 때마다 Render Tree를 재생성 해야하는데 인터렉션이 많아졌을 때, **모든 요소들의 스타일을 재계산**하고 **Layout, Repaint 과정을 재실행**하는 것이 **비효율적**이다.  
> 요즘 Single Page Application 같은 경우는 인터렉션이 매우 많다.

## 비효율 문제를 해결하기 위해서 나온 '가상 돔'
가상 돔(Virtual DOM) : 실제 DOM을 메모리에 복사해준 것

### 가상 돔 동작 방식
데이터가 바뀌면 가상돔에 렌더링되고 이전에 생긴 가상돔과 비교해서 바뀐 부분만 실제 돔에 적용 시킨다.  
바뀐 부분을 찾는 과정을 **Diffing**이라고 부르며, 바뀐 부분만 실제 돔에 적용시키는 것을 **재조정(reconciliation)**이라고 한다.

=> 만약 요소 30개가 변화하였다고 하더라도 한 번에 묶어서 한 번의 실제 돔 수정으로 처리하게 돼서 돔을 조작하는 비용 감소  
