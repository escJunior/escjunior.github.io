---
title: '[Algorithms] 프린터'
excerpt: 'Queue'

categories:
  - Algorithms
tags:
  - [Algorithms, Queue]

permalink: /Algorithms/printer/

toc: true
toc_sticky: true

date: 2022-09-18
last_modified_at: 2022-09-18
---

### 문제 설명

1. 대기열 목록에서 가장 앞에 있는 요소를 꺼낸다.
2. 꺼낸 요소보다 중요도가 높은 요소가 존재할 경우 꺼낸 요소를 마지막으로 보낸다.
3. 그렇지 않으면 요소 출력

### 입출력 예

| priorities         | location | return |
| ------------------ | -------- | ------ |
| [2, 1, 3, 2]       | 2        | 1      |
| [1, 1, 9, 1, 1, 1] | 0        | 5      |

예제 #2

6개의 문서(A, B, C, D, E, F)가 인쇄 대기목록에 있고 중요도가 1 1 9 1 1 1 이므로 C D E F A B 순으로 인쇄합니다.

### 문제 풀이

- Queue 사용
- 우선순위를 정렬한 있는 배열 생성후, priorities 배열에서 요청한 순서가 출력 될 때까지 우선순위를 정렬한 배열 요소를 지우며 EnQueue, DeQueue 반복

```jsx
function solution(priorities, location) {
  var answer = 0;

  let front = 0;
  let rear = priorities.length - 1;
  let locVal = priorities[location]; // 요청한 문서의 우선순위 저장

  let maxArr = Array.from(priorities, (v, i) => v);

  // 내림차순 정렬 - 우선순위을 파악하기 위함
  for (let i = priorities.length - 1; i > 0; i--) {
    for (let j = 0; j < i; j++) {
      if (maxArr[j] < maxArr[j + 1]) {
        let tmp = maxArr[j];
        maxArr[j] = maxArr[j + 1];
        maxArr[j + 1] = tmp;
      }
    }
  }

  let maxIdx = 0; // 정렬한 배열의 시작 Index
  priorities[location] = 0; // 요청한 문서 위치에 마킹처리
  let deQueue = -1; // 반복문 멈추기 위한 deQueue flag

  while (deQueue !== 0) {
    if (priorities[front] === 0) {
      // 내가 요청한 문서 차례가 왔을 경우
      if (maxArr[maxIdx] > locVal) {
        // 내가 요청한 문서보다 우선순위가 높은 문서가 있을 경우
        priorities[rear + 1] = priorities[front]; // front는 맨 뒤로 보냄
        front += 1;
        rear += 1;
      } else {
        // 없을 경우 바로 출력
        deQueue = priorities[front];
        answer++;
        break;
      }
    } else if (maxArr[maxIdx] > priorities[front]) {
      // 현재 차례 보다 우선순위가 높은 문서가 존재할 경우
      priorities[rear + 1] = priorities[front]; // 뒤로 보냄
      front += 1;
      rear += 1;
    } else {
      // 현재 차례가 우선순위가 제일 높은 문서 출력의 경우
      deQueue = priorities[front];
      front += 1;
      maxIdx++; // 출력된 우선순위 제거
      answer++;
    }

    // console.log(priorities.slice(front, rear + 1));
  }

  return answer;
}
```
