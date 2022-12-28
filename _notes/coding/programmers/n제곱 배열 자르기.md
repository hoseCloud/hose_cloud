
#level2 #cpp #writeup
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/87390)
template : [[template of writeup]]

## 문제 설명

정수 `n`, `left`, `right`가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

1. `n`행 `n`열 크기의 비어있는 2차원 배열을 만듭니다.
2. `i = 1, 2, 3, ..., n`에 대해서, 다음 과정을 반복합니다.
    - 1행 1열부터 `i`행 `i`열까지의 영역 내의 모든 빈 칸을 숫자 `i`로 채웁니다.
3. 1행, 2행, ..., `n`행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.
4. 새로운 1차원 배열을 `arr`이라 할 때, `arr[left]`, `arr[left+1]`, ..., `arr[right]`만 남기고 나머지는 지웁니다.

정수 `n`, `left`, `right`가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.

## 제한 조건

- 1 ≤ `n` ≤ 10$^7$
- 0 ≤ `left` ≤ `right` < n$^2$
- `right` - `left` < 10$^5$

## 입출력 예

| n   | left | right | result                     |
| --- | ---- | ----- | -------------------------- |
| 3   | 2    | 5     | `[3, 2, 2, 3]`             |
| 4   | 7    | 14    | `[4, 3, 3, 3, 4, 4, 4, 4]` |

## 풀이

### 코드

```
#include <string>
#include <vector>
#define MAX(a, b) (a > b ? a : b)

using namespace std;

vector<int> solution(int n, long long left, long long right) {
    vector<int> answer;
    long long row, col;
    
    for(long long i  = left; i <= right; i++) {
        row = i / n + 1;
        col = i % n + 1;
        
        answer.push_back(MAX(row, col));
    }
    
    return answer;
}
```

### 설명

입출력 예 설명에 있는 애니메이션처럼 만든다면 공간복잡도가 엄청나게 커서 불가능할 것이다. 배열의 규칙을 찾아서 새로운 배열을 추가하는 것으로 문제를 해결했다.

### 후기

입력값의 데이터 크기를 고려해 데이터 타입을 잘 고르도록 하자! long long 대신 int 썻다가 시간초과 나서 제시한 수식이 잘못된줄 알아서 삽지할 뻔 했다.
