---
title: '[Algorithms] 유용한 코드'
excerpt: '유용한 코드'

categories:
  - Algorithms
tags:
  - [Algorithms]

permalink: /Algorithms/useful-code/

toc: true
toc_sticky: true

date: 2022-09-15
last_modified_at: 2022-09-15
---

## 배열생성 및 초기화

```jsx
let arr = Array.from({ length: 52 }, () => 0);
```

## 배열 정렬

```jsx
/* 그냥 sort() 사용하면 
then comparing their sequences of UTF-16 code units values */

/* ASC */
arr.sort((a, b) => a - b);

/* DESC */
arr.sort((a, b) => b - a);
```

## 배열 내 중복 제거

```jsx
const names = ['Lee', 'Kim', 'Park', 'Lee', 'Kim'];
const uniqueNamesWithArrayFrom = Array.from(new Set(names));
const uniqueNamesWithSpread = [...new Set(names)];
```
