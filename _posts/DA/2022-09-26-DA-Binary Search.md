---
title: '[DA] Binary Search'
excerpt: 'Binary Search'

categories:
  - DA
tags:
  - [DA, Binary Search]

permalink: /da/binary-search/

toc: true
toc_sticky: true

date: 2022-09-26
last_modified_at: 2022-09-26
---

### Binary Search(이진 탐색)

1. 정렬 되어있는 요소들을 반씩 제외하며 찾는 알고리즘
2. 반드시 정렬이 되어있어야 사용 가능
3. Array, Binary Tree 로 구현 가능

### Array 구현

<img width="70%" src="https://user-images.githubusercontent.com/46982959/192236541-a2e5c84c-6170-4995-a42c-ccb45f4478d6.png">

```jsx
const array = [1, 1, 5, 124, 400, 599, 1004, 2876, 8712];

function binarySearch(array, findValue) {
  let left = 0;
  let right = array.length - 1;
  let mid = Math.floor((left + right) / 2);

  while (left < right) {
    if (array[mid] === findValue) {
      return mid;
    }

    if (array[mid] < findValue) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }

    mid = Math.floor((left + right) / 2);
  }

  return -1;
}
```

### Binary Tree 구현

왼쪽 서브 트리는 루트보다 작은 값, 오른쪽 서브 트리는 루트보다 큰 값

<img width="50%" src="https://user-images.githubusercontent.com/46982959/192236789-067b2031-83c1-4bc5-9be8-02fdcbd137e8.png">

```jsx
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(value) {
    const newNode = new Node(value);
    if (this.root === null) {
      this.root = newNode;
      return;
    }

    let currentNode = this.root;
    while (currentNode !== null) {
      if (currentNode.value < value) {
        if (currentNode.right == null) {
          currentNode.right = newNode;
          break;
        }
        currentNode = currentNode.right;
      } else {
        if (currentNode.left === null) {
          currentNode.left = newNode;
          break;
        }
        currentNode = currentNode.left;
      }
    }
  }

  has(value) {
    let currentNode = this.root;
    while (currentNode !== null) {
      if (currentNode.value === value) {
        return true;
      }

      if (currentNode.value < value) {
        currentNode = currentNode.right;
      } else {
        currentNode = currentNode.left;
      }
    }

    return false;
  }
}
```
