---
title: '[Algorithms] 가장 먼 노드'
excerpt: 'BFS'

categories:
  - Algorithms
tags:
  - [Algorithms, BFS]

permalink: /Algorithms/long-dist-node/

toc: true
toc_sticky: true

date: 2022-09-28
last_modified_at: 2022-09-28
---

### 문제 설명

가장 멀리 떨어진 노드의 개수 출력

### 입출력 예

| n   | vertex                                                   | return |
| --- | -------------------------------------------------------- | ------ |
| 6   | [[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]] | 3      |

### 제한사항

- 노드의 개수 n은 2 이상 20,000 이하입니다.
- 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
- vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다

### 입출력 예 설명

예제의 그래프를 표현하면 아래 그림과 같고, 1번 노드에서 가장 멀리 떨어진 노드는 4,5,6번 노드입니다.

<img width="40%" src="https://user-images.githubusercontent.com/46982959/192797730-a7ebadfa-9db0-4793-9896-1621eda10fc5.png">

### 문제 풀이

1. BFS 사용
2. 연결 노드, 양방향이므로 정점 양방향 연결 처리
3. 재귀를 사용하면 노드수 2만, 간선 5만이기 때문에 최악의 경우 스택 사이즈가 10만이 되어 while을 사용해야한다.(7, 8, 9 에러남)

```jsx
// while 사용
class Node {
  constructor(value, dist) {
    this.value = value;
    this.dist = dist;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  enQueue(value, dist) {
    let newNode = new Node(value, dist);

    if (this.head == null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }

    this.size += 1;
  }

  deQueue() {
    const value = this.head.value;
    this.head = this.head.next;
    this.size -= 1;

    return value;
  }

  display() {
    let curNode = this.head;
    while (curNode != null) {
      console.log(curNode.value);
      curNode = curNode.next;
    }
  }
}

function solution(n, edge) {
  var answer = 0;

  let graph = {};

  // 연결 노드, 양방향이므로 정점 양방향 연결 처리
  for (let i = 1; i <= n; i++) graph[i] = new Set();
  for (item of edge) {
    graph[item[0]].add(item[1]);
    graph[item[1]].add(item[0]);
  }

  let queue = new Queue();
  let distArr = Array.from({ length: n + 1 }, () => 0);
  distArr[1] = 0;

  let max = 0;
  let maxCnt = 0;

  queue.enQueue(1, 0);

  // Size가 0이 될 때까지 deQueue 값의 연결 정점 enQueue
  while (queue.size !== 0) {
    let dqNum = queue.deQueue();

    for (item of graph[dqNum]) {
      if (distArr[item] === 0 && item != 1) {
        queue.enQueue(item, distArr[dqNum] + 1); // 이전 거리 값 + 1
        distArr[item] = distArr[dqNum] + 1; // 해당 정점의 거리 값 입력

        // Max 값 체크 및 업데이트
        if (max < distArr[item]) {
          max = distArr[item];
          maxCnt = 1;
        } else if (max === distArr[item]) {
          maxCnt++;
        }
      }
    }
  }

  answer = maxCnt;

  return answer;
}
```

```jsx
// 재귀함수 사용
class Node {
  constructor(value, dist) {
    this.value = value;
    this.dist = dist;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  enQueue(value, dist) {
    let newNode = new Node(value, dist);

    if (this.head == null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }

    this.size += 1;
  }

  deQueue() {
    const value = this.head.value;
    this.head = this.head.next;
    this.size -= 1;

    return value;
  }

  display() {
    let curNode = this.head;
    while (curNode != null) {
      console.log(curNode.value);
      curNode = curNode.next;
    }
  }
}

function solution(n, edge) {
  var answer = 0;

  let graph = {};

  // 연결 노드
  for (let i = 1; i <= n; i++) graph[i] = new Set();
  for (item of edge) {
    graph[item[0]].add(item[1]);
    graph[item[1]].add(item[0]);
  }

  console.log(graph);

  let queue = new Queue();
  let distArr = Array.from({ length: n + 1 }, () => 0);
  distArr[1] = 0;
  answer = bfs(graph, queue, 1, distArr, 0, 0);

  console.log(distArr);
  console.log(answer);

  return answer;
}

function bfs(graph, queue, dqNum, distArr, max, maxCnt) {
  for (item of graph[dqNum]) {
    if (distArr[item] === 0 && item != 1) {
      queue.enQueue(item, distArr[dqNum] + 1);
      distArr[item] = distArr[dqNum] + 1;

      if (max < distArr[item]) {
        max = distArr[item];
        maxCnt = 1;
      } else if (max === distArr[item]) {
        maxCnt++;
      }
    }
  }

  if (queue.size === 0) return maxCnt;
  maxCnt = bfs(graph, queue, queue.deQueue(), distArr, max, maxCnt);

  return maxCnt;
}
```
