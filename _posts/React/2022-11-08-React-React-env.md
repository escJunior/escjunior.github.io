---
title: '[React] React Env'
excerpt: 'React Env'

categories:
  - React
tags:
  - [React]

permalink: /React/react-env/

toc: true
toc_sticky: true

date: 2022-11-08
last_modified_at: 2022-11-08
---

### React 환경설정

1. VS Code: [https://visualstudio.microsoft.com/ko/downloads/](https://visualstudio.microsoft.com/ko/downloads/)
2. Node JS: [https://nodejs.org/ko/](https://nodejs.org/ko/)
3. git: [https://git-scm.com/downloads](https://git-scm.com/downloads)
4. yarn: Node.js 16.10 이상인 경우 터미널에서 corepack enable 명령어로 설치

<img width='80%' src='https://user-images.githubusercontent.com/46982959/200343031-7aec181c-3d64-4e4e-9c75-b76676af0ac9.png'>

### 리액트 개발 참고 사이트

React 공식 사이트: [https://reactjs.org/](https://reactjs.org/)

React 베타 문서: [https://beta.reactjs.org/](https://beta.reactjs.org/)

Create React App: [https://create-react-app.dev/](https://create-react-app.dev/)

### 프로젝트 생성

1. yarn create react-app 프로젝트명  
   (Babel, Webpack등 기본적으로 필요한 파일 설치와 설정이 된다.)
   <img width='80%' src='https://user-images.githubusercontent.com/46982959/200343399-da7cd11f-9f04-4b45-8372-fa7732eae073.png'>
   <img width='80%' src='https://user-images.githubusercontent.com/46982959/200343594-a3d13bb1-11e7-4aa6-b8c4-d1e7ad383775.png'>

2. terminal 에서 code . 으로 VS Code 실행
   <img width='80%' src='https://user-images.githubusercontent.com/46982959/200343795-6f402f6f-802d-4f81-b0b8-0ff61140cffe.png'>

3. terminal 또는 VS Code의 terminal 에서 yarn start 로 리액트 프로젝트 실행확인
   <img width='80%' src='https://user-images.githubusercontent.com/46982959/200344119-95a75c6f-7a17-4777-80f1-2cd71a5b8dca.png'>

### 프로젝트 구조

1. .yarn, node_modules, .pnp.cjs, .pnp.loader.mjs, yarn.lock 외부 라이브러리 관련 파일로 건드릴 일이 거의 없음!
2. public: Static 리소스들이 있는 폴더
3. src: Dynamic 소스들이 저장되는 폴더
4. package.json: 프로젝트의 관련 정보가 있는 파일

### 추가 Extension

1. Chrome Web Store  
   React Developer Tools: 크롬 개발자 도구에서 리액트 구조를 보여줌
2. VS Code  
   Auto Import: 다른 파일 Import 시 자동으로 완성  
   Material Theme: 테마적용  
   Material Icon Theme: 프로젝트의 파일 및 폴더 아이콘 테마  
   Prittier - Code formatter: 코드를 포맷팅  
   CSS Modules: PostCSS 관련  
   IntelliSense for CSS class names in HTML  
   HTML to CSS autocompletion  
   HTML CSS Support  
   CSS Peek  
   Auto Rename Tag
