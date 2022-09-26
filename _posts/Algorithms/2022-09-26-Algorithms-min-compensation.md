---
title: '[Algorithms] 배상비용 최소화'
excerpt: 'Heap'

categories:
  - Algorithms
tags:
  - [Algorithms, Heap]

permalink: /Algorithms/min-compensation/

toc: true
toc_sticky: true

date: 2022-09-26
last_modified_at: 2022-09-26
---

### 문제 설명

일할 수 있는 시간 N 만큼 works 를 차감하여 남은 일 works 요소의 제곱을 더한 합이 최소가 되도록 구현

### 입출력 예

| N   | works   | result |
| --- | ------- | ------ |
| 4   | [4,3,3] | 12     |
| 2   | [3,3,3] | 17     |

### 입출력 예 설명

입출력 예 #1문제의 예제와 같습니다.

입출력 예 #2배상 비용을 최소화하기 위해 일을 한 결과는 [2, 2, 3]가 되고 배상 비용은 22 + 22 + 32 = 17가 되어 17를 반환해 줍니다.

### 문제 풀이

- 현재 works 의 가장 큰 값을 계속 감소하는 것이 포인트
- Max Heap 사용
- 일할 수 있는 시간만큼 루트 값 삭제, 루트 값 - 1 삽입 반복

```jsx
function solution(no, works) {
  var result = 0;

  // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
  console.log('Hello Javascript');

  class MaxHeap {
    constructor() {
      this.heap = [null];
    }

    push(pushValue) {
      let curIdx = this.heap.length;
      this.heap[curIdx] = pushValue;

      let parentIdx = Math.floor(curIdx / 2);

      while (parentIdx !== 0 && this.heap[curIdx] > this.heap[parentIdx]) {
        let temp = this.heap[parentIdx];
        this.heap[parentIdx] = this.heap[curIdx];
        this.heap[curIdx] = temp;

        curIdx = parentIdx;
        parentIdx = Math.floor(curIdx / 2);
      }
    }

    pop() {
      if (this.heap.length === 2) return this.heap.pop();

      let returnValue = this.heap[1];
      this.heap[1] = this.heap.pop();
      let curIdx = 1;
      let leftIdx = curIdx * 2;
      let rightIdx = curIdx * 2 + 1;

      while (
        this.heap[curIdx] < this.heap[leftIdx] ||
        this.heap[curIdx] < this.heap[rightIdx]
      ) {
        if (this.heap[leftIdx] < this.heap[rightIdx]) {
          let temp = this.heap[curIdx];
          this.heap[curIdx] = this.heap[rightIdx];
          this.heap[rightIdx] = temp;

          curIdx = rightIdx;
        } else {
          let temp = this.heap[curIdx];
          this.heap[curIdx] = this.heap[leftIdx];
          this.heap[leftIdx] = temp;

          curIdx = leftIdx;
        }
        leftIdx = curIdx * 2;
        rightIdx = curIdx * 2 + 1;
      }

      return returnValue;
    }
  }

  // 일을 끝낼 수 있는 시간이 충분한 경우
  if (works.reduce((a, b) => a + b) <= no) return 0;

  const maxHeap = new MaxHeap();
  // Max Heap 생성
  for (element of works) {
    maxHeap.push(element);
  }

  // 루트 값 삭제 후 루트 값 - 1 삽입
  for (let i = 0; i < no; i++) {
    maxHeap.push(maxHeap.pop() - 1);
  }

  // 배상비용 구하기
  for (const element of maxHeap.heap) {
    if (element !== null) result += element ** 2;
  }

  return result;
}
```
