---
title: '[Algorithms] 베스트앨범'
excerpt: 'Hash Table'

categories:
  - Algorithms
tags:
  - [Algorithms, Hash Table]

permalink: /Algorithms/best-album/

toc: true
toc_sticky: true

date: 2022-09-21
last_modified_at: 2022-09-21
---

### 문제 설명

속한 노래가 많이 재생된 장르를 먼저 수록합니다.

1. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
2. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

### 입출력 예

classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

- 고유 번호 3: 800회 재생
- 고유 번호 0: 500회 재생
- 고유 번호 2: 150회 재생

pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

- 고유 번호 4: 2,500회 재생
- 고유 번호 1: 600회 재생

따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.

- 장르 별로 가장 많이 재생된 노래를 최대 두 개까지 모아 베스트 앨범을 출시하므로 2번 노래는 수록되지 않습니다.

| genres                                          | plays                      | return       |
| ----------------------------------------------- | -------------------------- | ------------ |
| ["classic", "pop", "classic", "classic", "pop"] | [500, 600, 150, 800, 2500] | [4, 1, 3, 0] |

### 문제풀이

1. genres 별 분류 및 합 생성, genres 별 내림차순 정렬
2. 모든 genres 총 재생횟수 내림차순 정렬
3. 2번에서 정렬 한 순서로 genres 별 최상위 2개 또는 1개 출력

```jsx
function solution(genres, plays) {
  var answer = [];

  let mapGenres = new Map();

  // genres 별 분류 및 합 생성
  // 고유번호가 낮은 순부터 생성하므로 기준 3은 자동 만족
  for (let i = 0; i < genres.length; i++) {
    if (!mapGenres.has(genres[i])) {
      let arr = new Array();
      arr.push(plays[i]);
      arr.push([plays[i], i]);
      mapGenres.set(genres[i], arr);
    } else {
      let temp = mapGenres.get(genres[i]);
      temp[0] = temp[0] + plays[i];
      temp.push([plays[i], i]);
      mapGenres.set(genres[i], temp);
    }
  }

  // 기준 1을 위한 속한 노래가 많이 재생된 정렬로 만든 배열
  let arrGenres = new Array();
  let arrGenresSum = new Array();

  // 1. genres 이름만 가진 arr, genres 합만 가진 arr 생성 (순서 동일)
  // 2. 기준 2를 위한 genres 별 정렬 실행 내림차순
  mapGenres.forEach((value, key) => {
    arrGenres.push(key);
    arrGenresSum.push(value[0]);

    for (let i = value.length - 1; i > 0; i--) {
      for (let j = 1; j < i; j++) {
        if (value[j][0] < value[j + 1][0]) {
          let temp = value[j];
          value[j] = value[j + 1];
          value[j + 1] = temp;
        }
      }
    }
  });

  // 조건 1을 위한 arr 정렬 내림차순
  for (let i = arrGenresSum.length - 1; i > 0; i--) {
    for (let j = 0; j < i; j++) {
      if (arrGenresSum[j] < arrGenresSum[j + 1]) {
        let temp = arrGenresSum[j];
        arrGenresSum[j] = arrGenresSum[j + 1];
        arrGenresSum[j + 1] = temp;

        let temp2 = arrGenres[j];
        arrGenres[j] = arrGenres[j + 1];
        arrGenres[j + 1] = temp2;
      }
    }
  }

  // 속한 노래가 많이 재생된 장르부터 수록
  for (genre of arrGenres) {
    let temp = mapGenres.get(genre);
    if (temp.length > 2) {
      // 0번째는 총합이므로 2를 초과해야 노래가 2개 이상임
      for (let i = 0; i < 2; i++) answer.push(temp[i + 1][1]);
    } else answer.push(temp[1][1]); // 노래가 1개일 때
  }

  return answer;
}
```
