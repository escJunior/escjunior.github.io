---
title: '[Algorithms] 타겟 넘버'
excerpt: 'DFS / BFS'

categories:
  - Algorithms
tags:
  - [Algorithms]

permalink: /Algorithms/target-number/

toc: true
toc_sticky: true

date: 2022-09-19
last_modified_at: 2022-09-19
---

### 문제 설명

주어진 숫자 배열의 덧셈, 뺄셈 모든 경우의 수에서 타겟 넘버를 만드는 방법의 수 출력

### 입출력 예

numbers target return

[1, 1, 1, 1, 1] 3 5

[4, 1, 2, 1] 4 2

입출력 예 #2

+4+1-2+1 = 4

+4-1+2-1 = 4

### 문제 풀이

- DFS 사용
- Binary Tree를 생각하며 뻗어 나간다.

```jsx
function solution(numbers, target) {
  var answer = 0;

  // Binary Tree를 생각하며 뻗어 나간다.
  function dfsFunc(numbers, idx, sum) {
    let lSum = sum; // - 숫자
    let rSum = sum; // + 숫자

    lSum += -numbers[idx];
    if (numbers.length - 1 === idx) {
      // 마지막 인덱스
      if (lSum === target) answer++;
    } else dfsFunc(numbers, idx + 1, lSum); // 계속 탐색

    rSum += numbers[idx];
    if (numbers.length - 1 === idx) {
      if (rSum === target) answer++;
    } else dfsFunc(numbers, idx + 1, rSum);
  }

  dfsFunc(numbers, 0, 0);

  return answer;
}
```
