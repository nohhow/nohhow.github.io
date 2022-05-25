---
layout: post
title: Code Editor와 친해지기 (vscode, atom, pycharm)
image:
  path: https://source.unsplash.com/random
description: >
  Sql 기초 문법
sitemap: false
categories:
  - study
  - etc

---
# Code Editor와 친해지기 (vscode, atom, pycharm)

* toc
{:toc .large-only}

## 개요
<img src="http://image.yes24.com/goods/107077663/XL" alt="실용주의 프로그래머" width="50%"/>


**실용주의 프로그래머** [Topic 18. 파워 에디팅] 파트를 읽다가 `에디터를 유창하게 사용할 수 있는가?` 에 대한 도전을 받았고, 지금 사용하고 있는 **에디터**들의 Editing 기능들을 익히기 위해서 정리한다.


## 현재 사용하는 코드 에디터 종류

1. **visual studio code**
    - React 관련 플러그인을 모두 셋팅해두고 React 코드 작성시 주로 사용하는 중
2. **atom**
    - markdown preview 기능이 만족스러워서 md 문서를 작성할 때 주로 사용하는 중
3. **pycharm**
    - python IDE, 코딩테스트에 대비하며 python을 익히는데 주로 사용하는 중
    - 사용한지 몇 주 되지 않아서 가장 친숙하지 못한 녀석

## 어떤 것이 '유창'한 것인가?

다음의 각 `도전 과제`들을 수행할 수 있어야 한다.

## 도전 과제

실행 환경이 `macOS`이다 보니 `macOS`에 맞는 실행방식을 작성한다.
key mapping에 따라서 설정이 조금씩 달라질 수 있겠다. <small>(혹은 버전에 따라 상이할 듯 하다.)</small>

#### 문자, 단어, 줄, 문단 단위로 커서를 이동하거나 내용을 선택

* 문자 단위 이동

|공통|
|--|
|이동 : `left, right`<br/>선택 : `shift+left,right`|

* 단어/문단 단위 이동 또는 선택

|공통|
|--|
|이동 : `opt+left,right`<br/>선택 : `opt+shift+left,right`|

* 줄 단위 이동 또는 선택

|공통|
|--|
|이동 : `up,down`, `cmd+left,right`<br/>선택(커서 맨앞 or 맨뒤) : `cmd+shift+left, right`|


#### 반대쪽 괄호로 이동, 함수, 모듈 등 다양한 문법 단위로 커서 이동

* 각 괄호의 시작점이나 끝점으로 이동

|vscode|atom|pycharm|
|--|--|--|
| `cmd+shift+\` | `ctrl+m` | `ctrl+m` |

* 문법 단위로 이동

|vscode|atom|pycharm|
|--|--|--|
| `???` | `???` | `opt+cmd+[,]` |


#### 변경한 코드의 들여쓰기를 자동으로 맞추기
개인적인 생각으로는 Beautify 나 Prettier 플러그인을 설치해서 단축키 사용하는 것이 이로울 것 같다.
- **atom**은 사전에 설정이 필요하다.
    - 자동 정렬 : edit > line > auto indent
    - 수동 정렬
      - 세팅
        keymapping file에 다음 코드 추가
        ~~~
        'atom-text-editor':
          'ctrl-f' : 'editor:auto-indent'
        ~~~
      - 동작 : 영역 지정 후 `ctrl-f` (임의 지정 가능)


|vscode|atom|pycharm|
|--|--|--|
| 영역 지정 후 `cmd+k`+`cmd+f` | `아래 내용 참고` | `cmd+opt+l` |

#### 여러 줄의 코드를 명령 하나로 주석 처리했다가 다시 주석을 해제하기

|공통|
|--|
|토글 : `cmd+/`|

#### 실행 취소를 여러 번 했다가 취소한 명령을 재실행 기능으로 다시 수행하기

역으로 실행하는 명령에는 주로 shift를 붙이면 된다.
|공통|
|--|
|실행취소 : `cmd+z`<br/>재실행 : `cmd+shift+z`|

#### 에디터 창을 여러 구역으로 쪼개기. 각 구역 사이를 이동하기

* 창 분할 및 이동

|vscode|atom|pycharm|
|--|--|--|
| 분할 : `cmd+\`<br/>이동 : `cmd+숫자` | 분할: `cmd+k 방향키`<br/>이동 : `cmd+k`+`cmd+방향키` | 분할 : `cmd+shift+a` + `split 명령 실행` |


* 탭 제어

|공통|
|--|
|다음 탭 : `ctrl+tab`<br/>이전 탭 : `ctrl+shift+tab`<br/>탭 닫기 : `cmd+w`|

#### 특정 줄 번호로 이동하기

|공통|
|--|
| `ctrl+g+숫자입력` |

#### 문자열로, 또 정규 표현식으로 검색하기. 이전에 검색했던 것 다시 검색하기

* 문자열 검색

|공통|
|--|
|`cmd+f`|

* 정규 표현식 검색

|vscode|atom|pycharm|
|--|--|--|
| `cmd+f`+`opt+cmd+r` | `cmd+f`+`opt+cmd+/` | `cmd+f`+`ctrl+opt+x` |


#### 선택 영역이나 패턴 검색을 이용하여 일시적으로 여러 개의 커서를 만든 다음, 동시에 여러 곳의 텍스트를 편집하기

* 선택된 단어를 기준으로 다중 선택

|vscode|atom|pycharm|
|--|--|--|
| `cmd+d` | `cmd+d` | `cmd+g` |
