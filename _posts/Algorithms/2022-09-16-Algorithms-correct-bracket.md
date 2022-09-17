---
title: '[Algorithms] 올바른 괄호'
excerpt: '스택'

categories:
  - Algorithms
tags:
  - [Algorithms]

permalink: /Algorithms/correct-bracket/

toc: true
toc_sticky: true

date: 2022-09-16
last_modified_at: 2022-09-16
---

### 문제 설명

괄호 짝이 맞음 여부에 따라 true, false 리턴

### 입출력 예

| s        | answer |
| -------- | ------ |
| "()()"   | true   |
| "(())()" | true   |
| ")()("   | false  |
| "(()("   | false  |

### 문제 풀이

- Stack 사용
- ‘(’ pop 일 때는 체크 개수를 -1, ‘)’ 일 때는 체크 개수를 +1 이때 체크 개수가 -1 이 된다면 ‘(’ 가 없는 상황이므로 false, 이외 경우는 true

```jsx
function solution(s) {
  var answer = true;
  let taskCnt = 0; // stack () 개수

  // 짝수가 아니면 짝이 안맞아 false
  if (s.length % 2 !== 0) return false;

  // pop
  for (let i = 0; i < s.length; i++) {
    // pop으로 인한 top 위치 변경
    let stackValue = s[s.length - i - 1];

    if (stackValue === '(') {
      // ( 일때 짝이 맞으면 개수 감소
      taskCnt--;
    } else {
      // ( 는 () 개수 증가
      taskCnt++;
    }

    if (taskCnt < 0) return false;
  }

  return answer;
}
```
