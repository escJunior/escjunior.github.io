---
title: '[Algorithms] 소수 구하기'
excerpt: 'Prime Number'

categories:
  - Algorithms
tags:
  - [Algorithms]

permalink: /Algorithms/get-prime-number/

toc: true
toc_sticky: true

date: 2022-10-10
last_modified_at: 2022-10-10
---

### 소수

1 제외, 1과 자기 자신만을 약수로 갖는 정수

### 구현방법

#1. 2부터 **N의 제곱근까지만** 체크하며, 체크하는 방식은 2부터 현재 자기 자신의 숫자이외 나누어 떨어지는 숫자가 있는지 체크, **하지만 효율성에서 통과 못함**

```jsx
// O(sqrt(n))
function isPrime(num) {
  for (let i = 2; i * i <= num; i += 1) {
    if (num % i == 0) {
      return false;
    }
  }

  return true;
}

function solution(n) {
  let answer = 0;
  for (let i = 2; i <= n; i += 1) {
    if (isPrime(i)) {
      answer += 1;
    }
  }

  return answer;
}
```

#2. 에라토스테네스의 체를 이용, N의 범위 만큼 만든 후 배수가 되는 Index는 제외

| 0(Except)  | 1(Except) | 2          | 3          |
| ---------- | --------- | ---------- | ---------- |
| 4(Except)  | 5         | 6(Except)  | 7          |
| ---------- | --------- | ---------- | ---------- |
| 8(Except)  | 9(Except) | 10(Except) | 11         |
| ---------- | --------- | ---------- | ---------- |
| 12(Except) | 13        | 14(Except) | 15(Except) |

```jsx
function solution(n) {
  var answer = n - 1; // 소수는 1 제외

  // 숫차 체크할 배열 생성
  let chkArr = Array.from({ length: n + 1 }, () => 0);

  // 2부터 시작
  for (let i = 2; i * i < n; i++) {
    if (chkArr[i] === 1) continue;

    // 자기 자신은 제외, 2부터 시작
    for (let j = 2; j * i <= n; j++) {
      if (chkArr[j * i] === 0) {
        chkArr[j * i] = 1;
        answer--;
      }
    }
  }

  //console.log(chkArr);
  return answer;
}
```
