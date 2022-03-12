---
layout: post
title: State and Props
image:
  path: /assets/img/thumbnail/react.png
description: >
  John Ahn님의 [Project-Lion] The Origin-React 강의를 듣고 정리한 내용입니다.
sitemap: false
categories:
  - study
  - react

---
# State와 Props

## State
1. 부모 컴포넌트에서 자녀 컴포넌트로 데이터를 보내는게 아닌 해당 컴포넌트 내부에서 데이터를 전달 할 때 사용
2. State는 변경이 가능하다. (mutable)
3. State가 변하면 re-render 된다.

## Props
1. Props는 Properties의 줄임말
2. Props는 상속하는 부모 컴포넌트로부터 자녀 컴포넌트에 데이터 등을 전달하는 방법
3. Props는 읽기 전용(immutable)으로 컴포넌트 입장에서는 변하지 않는다. (변하게 하고자 하면 부모 컴포넌트에서 state를 변경해주어야 한다.)
