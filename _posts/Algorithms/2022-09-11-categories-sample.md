---
title: '[Algorithms] 자동완성'
excerpt: 'Trie'

categories:
  - Algorithms
tags:
  - [Algorithms, Trie]

permalink: /Algorithms/auto-complete/

toc: true
toc_sticky: true

date: 2022-09-26
last_modified_at: 2022-09-26
---

### 문제 설명

입력된 단어를 모두 찾기 위한 입력한 문자의 수를 출력

### 입출력 예제

| words                            | result |
| -------------------------------- | ------ |
| ["go","gone","guild"]            | 7      |
| ["abc","def","ghi","jklm"]       | 4      |
| ["word","war","warrior","world"] | 15     |

### **입출력 설명**

- 첫 번째 예제는 본문 설명과 같다.
- 두 번째 예제에서는 모든 단어들이 공통된 부분이 없으므로, 가장 앞글자만 입력하면 된다.
- 세 번째 예제는 총 `15` 자를 입력해야 하고 설명은 아래와 같다.
  - `word`는 `word`모두 입력해야 한다.
  - `war`는 `war` 까지 모두 입력해야 한다.
  - `warrior`는 `warr` 까지만 입력하면 된다.
  - `world`는 `worl`까지 입력해야 한다. (`word`와 구분되어야 함을 명심하자)

### 문제 풀이

1. Trie 생성(글자 카운트 소유, 각 정점 마다 증가하는 단어가 아닌 한글자 소유)
2. Trie 탐색시 글자의 카운트가 1 이면 마지막 카운트 이므로 탐색 중지

<img width="70%" src="https://user-images.githubusercontent.com/46982959/192228442-1ebd2f04-998d-4f1e-aef8-962bbf811f37.png">

```jsx
function solution(words) {
  var answer = 0;

  let trie = new makeTrie(words);
  let count = 0;

  for (const word of words) {
    let currentNode = trie;

    for (const letter of word) {
      count++;
      // letter의 카운트가 1 이면 마지막 카운트 이므로 더 진행할 필요가 없다.
      if (currentNode[letter][0] === 1) break;

      currentNode = currentNode[letter][1];
    }
  }

  answer = count;
  return answer;
}

function makeTrie(words) {
  let root = {};

  for (const word of words) {
    let currentNode = root;

    // letter 카운트
    for (const letter of word) {
      if (!currentNode[letter]) currentNode[letter] = [0, {}];
      currentNode[letter][0] = 1 + currentNode[letter][0];

      currentNode = currentNode[letter][1];
    }
  }

  return root;
}
```
