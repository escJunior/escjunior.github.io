---
title: '[Algorithms] 큰 수 만들기'
excerpt: 'Greedy'

categories:
  - Algorithms
tags:
  - [Greedy]

permalink: /Algorithms/make-big-number/

toc: true
toc_sticky: true

date: 2022-10-07
last_modified_at: 2022-10-07
---

### 문제 설명

k 개의 숫자를 제거하여 최대값 출력

### 제한 조건

- number는 2자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 `number의 자릿수` 미만인 자연수입니다.

### 입출력 예

| number       | k   | return   |
| ------------ | --- | -------- |
| "1924"       | 2   | "94"     |
| "1231234"    | 3   | "3234"   |
| "4177252841" | 4   | "775841" |

### 문제풀이

1. 조건에 맞는 가장 큰 수를 하나씩 추출하여 결과 완성

```jsx
function solution(number, k) {
  var answer = '';
  let answerLength = number.length - k; // 결과 자릿수
  let maxIdx = 0;
  let maxArr = [...number].sort((a, b) => b - a); // 큰 수부터 찾기 위해 내림차순 정렬
  //let maxArr = [...new Set(number.split('').sort((a, b) => b - a))];

  // 결과 자릿수를 만족하면 반복 종료
  while (answer.length !== answerLength) {
    let tempIdx = number.indexOf(maxArr[maxIdx]); // Max Nubmer Index

    if (
      // 찾는 수가 마지막이 아니고, 결과 자릿수 부족하지 않고, 현재 number 에 찾는 Max Number 가 없는 경우
      (answerLength - answer.length !== 1 &&
        number.length - tempIdx < answerLength - answer.length) ||
      tempIdx === -1
    ) {
      maxIdx++; // Max index 증가
    } else {
      // 조건에 만족하는 경우
      answer += maxArr[maxIdx];
      number = number.slice(tempIdx + 1); // 선택된 Max number의 앞의 숫자는 필요없기 때문에 날림
      maxIdx = 0; // Max Idx 초기화
    }

    // 남은 숫자의 개수와 남은 결과 자릿수가 같으면 바로 출력
    if (answerLength === answer.length + number.length) {
      answer += number;
    }
  }

  return answer;
}
```
