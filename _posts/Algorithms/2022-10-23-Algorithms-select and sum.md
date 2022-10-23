---
title: '[Algorithms] 두 개 뽑아서 더하기'
excerpt: '조합'

categories:
  - Algorithms
tags:
  - [Algorithms]

permalink: /Algorithms/select-and-sum/

toc: true
toc_sticky: true

date: 2022-10-23
last_modified_at: 2022-10-23
---

### 문제 설명

Numbers의 2개의 수 합을 중복 없이 오름차순으로 출력

### 입출력 예

| numbers     | result        |
| ----------- | ------------- |
| [2,1,3,4,1] | [2,3,4,5,6,7] |
| [5,0,2,7]   | [2,5,7,9,12]  |

### 문제 풀이

- 순회하며 합을 set에 담고, sort

```jsx
function solution(numbers) {
  var answer = [];

  var set = new Set();

  // 합을 set에 담는다.
  for (let i = 0; i < numbers.length - 1; i++) {
    for (let j = i + 1; j < numbers.length; j++) {
      set.add(numbers[i] + numbers[j]);
    }
  }

  // 배열에 담고 정렬
  for (element of set) {
    answer.push(element);
  }
  answer.sort((a, b) => a - b);

  return answer;
}
```

### 추가내용

순열: 순서가 있는 상태에서 전체에서 N개를 선택

```jsx
function permutations(arr, n) {
  // 1개만 뽑는다면 그대로 순열을 반환한다. 탈출 조건으로도 사용된다.
  if (n === 1) return arr.map((v) => [v]);
  let result = [];

  // 요소를 순환한다
  arr.forEach((fixed, idx, arr) => {
    // 현재 index를 제외한 요소를 추출한다.
    // index번째는 선택된 요소
    const rest = arr.filter((_, index) => index !== idx);
    // 선택된 요소를 제외하고 재귀 호출한다.
    const perms = permutations(rest, n - 1);
    // 선택된 요소와 재귀 호출을 통해 구한 순열을 합쳐준다.
    const combine = perms.map((v) => [fixed, ...v]);
    // 결과 값을 추가한다.
    result.push(...combine);
  });

  // 결과 반환
  return result;
}
```

조합: 순서가 없는 상태에서 전체에서 N개를 선택

```jsx
function combinations(arr, n) {
  // 1개만 뽑는다면 그대로 조합을 반환한다. 탈출 조건으로도 사용된다.
  if (n === 1) return arr.map((v) => [v]);
  const result = [];

  // 요소를 순환한다
  arr.forEach((fixed, idx, arr) => {
    // 현재 index 이후 요소를 추출한다.
    // index번째는 선택된 요소
    const rest = arr.slice(idx + 1);
    // 선택된 요소 이전 요소들을 제외하고 재귀 호출한다.
    const combis = combinations(rest, n - 1);
    // 선택된 요소와 재귀 호출을 통해 구한 조합을 합쳐준다.
    const combine = combis.map((v) => [fixed, ...v]);
    // 결과 값을 추가한다.
    result.push(...combine);
  });

  // 결과 반화
  return result;
}
```
