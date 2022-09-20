---
title: '[React] React Intro'
excerpt: 'React Intro'

categories:
  - React
tags:
  - [React]

permalink: /React/react-intro/

toc: true
toc_sticky: true

date: 2022-09-20
last_modified_at: 2022-09-20
---

### React

- **React란 User Interface를 만들 수 있는 Library, 사용자에게 보여지는 UI를 만들고 이에 대한 사용자의 클릭 또는 이벤트에 반응하도록 만들어진 Lib**
- React는 components로 이루어진 UI Lib
- 2013년 Face Book 에서 만들어짐
- 페이지를 더 빠르고, 쉽고, 재사용 가능하도록 만들 수 있다.
- 리액트는 트리 형식의 컴포넌트로 구성되어 있다.

<img width='80%' src='https://user-images.githubusercontent.com/46982959/191287894-6be18352-5a43-4600-b45e-59907954c8fa.png'>

### 컴포넌트 구조

```jsx
import React, { Component } from 'react';

// 부모의 state가 변하면 자식의 render()가 호출
class LikeButton extends Component {
  state = {
    numberOfLikes: 0, State
  };
  render() {
    return <button>
      {this.state.numberOfLikes}
      <button/>;
  }
}
```

- React는 Virtual DOM Tree와 previous Virtual DOM Tree와 비교하여 자식의 render()를 모두 호출하는게 아니라 계산하여 필요한 render()만 업데이트 한다.

### 추가내용

프레임워크: 뼈대가 정해져 있고 그 안에서 구현(ANGULAR, Vue)

Lib: 구현하는 도구(React)

components: 서로 독립적(independent), 고립(isolated), 재사용 가능(resusable)

최상위 component = root
