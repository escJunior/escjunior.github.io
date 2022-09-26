---
title: '[DA] Hash Table'
excerpt: 'Hash Table'

categories:
  - DA
tags:
  - [DA]

permalink: /da/Hash Table/

toc: true
toc_sticky: true

date: 2022-09-19
last_modified_at: 2022-09-19
---

Hash Table: 키와 값을 받아 키를 해싱하여 나온 index에 값을 저장하는 선형 자료구조

Hash Func: 입력받은 값을 특정 범위 내 숫자로 변경하는 함수

Array, Map, Set 으로 표현 가능

<img width='40%' src='https://user-images.githubusercontent.com/46982959/190913981-f1f0ceb4-b07a-436d-84dc-5cf8ef3aacbb.png'>
<img width='40%' src='https://user-images.githubusercontent.com/46982959/192270694-db395a0b-76ca-407f-95ce-8bdbe6922ecc.png'>

### Code

```jsx
// Array
const table = [];
table['key'] = 100;
console.log(table['key']);

// Map
const table2 = new Map();
table2.set('key', 100);
console.log(table2['key']); // 잘못된 방법
console.log(table2.get('key'));
console.log(table2.keys());
console.log(table2.values());
table2.clear();
console.log(table2.keys());
console.log(table2.values());

// Set
const table3 = new Set();
table3.add('key');
console.log(table.has('key'));
```
