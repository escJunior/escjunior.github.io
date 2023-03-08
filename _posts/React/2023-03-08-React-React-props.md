---
title: '[React] React props'
excerpt: 'React props'

categories:
  - React
tags:
  - [React]

permalink: /React/react-props/

toc: true
toc_sticky: true

date: 2023-03-08
last_modified_at: 2023-03-08
---

### props

1. props는 상위 컴포넌트에서 전달해 준 값
2. Component 속성으로 Key = Value 명시하면 Key, Value 가 props란 객체로 전달

상위 컴포넌트

```jsx
import logo from './logo.svg';
import './App.css';
import Profile from './components/Profile';

function AppProfile() {
  return (
    <>
      <Profile
        image='https://images.unsplash.com/photo-1580489944761-15a19d654956?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=922&q=80'
        name='kim'
        title='프론트 엔드 개발자'
        isNew={false}
      />
    </>
  );
}

export default AppProfile;
```

하위 컴포넌트

```jsx
import React from 'react';

export default function Profile(props) {
  return (
    <div className='profile'>
      <img className='photo' src={props.image} alt='avatar' />
      {isNew && <span className='new'>New</span>}
      <h1>{props.name}</h1>
      <p>{props.title}</p>
    </div>
  );
}
```

\* props 부분을 JS object deconstructing 이용도 가능!

```jsx
import React from 'react';

export default function Profile({ image, name, title, isNew }) {
  return (
    <div className='profile'>
      <img className='photo' src={image} alt='avatar' />
      {props.isNew && <span className='new'>New</span>}
      <h1>{name}</h1>
      <p>{title}</p>
    </div>
  );
}
```
