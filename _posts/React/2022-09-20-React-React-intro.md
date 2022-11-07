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
last_modified_at: 2022-11-06
---

### React

- **React란 UI(User Interface)를 Components 단위로 보여주고 Event에 반응하도록 만들어 나가는 Library**
- React는 components로 이루어진 UI Lib
- 2013년 Face Book 에서 만들어짐
- 페이지를 더 빠르고, 쉽고, 재사용 가능하도록 만들 수 있다.
- 리액트는 트리 형식의 컴포넌트로 구성되어 있다.

<img width='80%' src='https://user-images.githubusercontent.com/46982959/191287894-6be18352-5a43-4600-b45e-59907954c8fa.png'>

### 컴포넌트 구조

- 데이터 내부 상태 State, 외부로 부터 전달받은 상태 Props, 나타내는 render로 구성
- 상태가 변경될 때마다 re-render, 리액트의 Virtual DOM Tree, Previous DOM Tree 를 비교하여 DOM tree에 실제로 변경된 부분만 화면에 업데이트
- 2019년 부터 함수형 컴포넌트를 많이 사용

```jsx
// Function Copmonent
// React Hooks 를 이용해 로직 재사용 가능
function LikeButton(props) {
  const [likes, setLikes] = useState(0);
  return <button>{likes}</button>;
}
```

```jsx
// Class Component
// 클래스의 어려움, this 바인딩 이슈, 로직들을 재사용하기 어려워 함수형 컴포넌트 사용
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

### 추가내용

1. 프레임워크  
   뼈대가 정해져 있고 그 안에서 구현(ANGULAR, Vue)
2. Lib  
   구현하는 도구(React)
3. components  
   서로 독립적(independent), 고립(isolated), 재사용 가능(resusable)
4. 최상위 component = root
5. BABEL  
   최신 자바 문법을 → 옛날 브라우저에서도 돌 수 있도록 옛날 버전으로 변환
   타입스크립트, JSX 를 자바스크립트로 변환
6. Webpack  
   작성한 소스 코드를 사용자에게 간편하게 전달할 수 있도록 모듈을 Bundling 하는 역할
7. ESLint  
   코드에 잘못된 부분이 있다면 경고를 표시
8. Jest  
   JavaScript를 Unit 테스트 할 수 있도록 도와주는 테스팅 framework
9. PostCSS  
   CSS 전처리기, 유용한 플러그인이 많아 강력하게 쓸 수 있다.
10. nodeJS  
    Browser 밖에서 JavaSript를 실행 가능하게 해주는 JavaScript 실행 환경(FrameWork)
11. npm  
    필요한 Lib를 쉽게 관리(설치, 버전 업데이트), package.json
12. npx  
    원하는 Lib또는 Package를 실행 할 수 있도록 함
13. yarn  
    facebook에서 만든 package manager, npm을 보완하여 만듦
14. 브라우저는 HTML, CSS, JS를 이해할 수 있다. 그래서 리액트 소스를 Babel이 순수 JS로 변환, 변환된 소스를 HTML과 연결할 수 있는 작업을 해주는 것이 react-dom
