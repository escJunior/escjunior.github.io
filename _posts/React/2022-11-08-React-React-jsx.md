---
title: '[React] React JSX'
excerpt: 'React JSX'

categories:
  - React
tags:
  - [React]

permalink: /React/react-jsx/

toc: true
toc_sticky: true

date: 2022-11-09
last_modified_at: 2023-03-07
---

### JSX 문법 정리

```jsx
import logo from './logo.svg';
import './App.css';

function App() {
  const name = '승민';
  const list = ['우유', '딸기', '바나나'];
  return (
    <>
      <h1 className='orange'>{`Hello! ${name}`}</h1>
      <h2>Hellow!</h2>
      <p>{name}</p>
      <ul>
        <li>우유</li>
        <li>딸기</li>
        <li>바나나</li>
      </ul>
      <ul>
        {list.map((item) => (
          <li>{item}</li>
        ))}
      </ul>
      <img
        style={{ width: '400px', height: '200px' }}
        src='https://images.unsplash.com/photo-1667849006991-5b759790fcfb?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHw1MXx8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60'
        alt='nature'
      />
    </>
  );
}

export default App;
```

### 구조

1. 함수명은 대문자로 시작
2. 반환 return은 어떻게 UI를 표기할지 JSX를 return 해주어야 한다.

### JSX 문법

1. Component는 하나의 태그만 반환 해야함 → 따라서 다수의 태그를 반환하고 싶다면 부모 태그로 감싸주어야 한다.<></>
2. 태그에 클래스를 적용할 때는 className을 사용
3. HTML부분에 자바스크립트 코드를 사용할 때는 {} 중괄호 사용

### Component 만드는 팁

1. global.code-snippets.json.code-snippets 에 해당 Snippet 입력

```json
"reactFunction": {
  "prefix": "rfc",
  "body": "import React from 'react';\n\nexport default function ${1:${TM_FILENAME_BASE}}() {\n\treturn (\n\t\t<div>\n\t\t\t\n\t\t</div>\n\t);\n}\n\n",
  "description": "Creates a React Function component"
},
"reactStatelessImplicitReturn": {
  "prefix": "rsi",
  "body": "import React from 'react';\n\nexport const ${1:${TM_FILENAME_BASE}} = (props) => (\n\t\t\t$0\n\t);",
  "description": "Creates a React Function component"
}
```

2. rfc 또는 rfi 입력하면 컴포넌트 구조 자동완성!
