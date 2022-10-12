---
title: '[Algorithms] 전화번호 목록'
excerpt: 'Hash'

categories:
  - Algorithms
tags:
  - [Algorithms, Hash]

permalink: /Algorithms/phone-number-list/

toc: true
toc_sticky: true

date: 2022-10-12
last_modified_at: 2022-10-12
---

### 문제 설명

주어진 배열에서 한 요소가 다른 요소의 접두어일 경우 false 아니면 true

### 입출력 예

| phone_book                        | return |
| --------------------------------- | ------ |
| ["119", "97674223", "1195524421"] | false  |
| ["123","456","789"]               | true   |
| ["12","123","1235","567","88"]    | false  |

입출력 예 #2  
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3  
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

### 문제 풀이

- 주어진 배열 정렬 후, i 와 i + 1 요소 체크
- 정렬시에는 아스키코드 크기를 비교하는 정렬로 해야함 그래야 접두어 크기순으로 정렬되어 접두어 체크가 가능함

```java
import java.util.*;

class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;

        Arrays.sort(phone_book); // 아스키코드 크기를 비교하여 정렬됨 1132 113 1024 ...

        for(int i = 0; i < phone_book.length - 1; i++) {

            // 중복 숫자는 없기 때문에 i + 1 더 클 때만 비교
            if(phone_book[i].length() < phone_book[i + 1].length()) {
                if(phone_book[i + 1].startsWith(phone_book[i])) return false;
            }
        }

        return answer;
    }
}
```
