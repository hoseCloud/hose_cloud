
#level2 #cpp #writeup
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/42747)
template : [[template of writeup]]

## 문제 설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. [위키백과](https://school.programmers.co.kr/learn/courses/30/lessons/42747#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

## 제한 조건

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

## 입출력 예

| citations         | return |
| ----------------- | ------ |
| `[3, 0, 6, 1, 5]` | 3      |

## 풀이

### 코드

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    int answer = 0;
    bool flag = false;
    
    sort(citations.begin(), citations.end());
    
    for(int i = citations.size(); i >= 0; i--) {
        for(int j = 0; j <= citations.size()-i; j++) {
            if(citations[j] >= i) {
                answer = i;
                flag = true;
                break;
            }
        }
        if(flag) break;
    }
    
    return answer;
}
```

### 설명

주어진 벡터를 오름차순으로 정렬하고 조건에 맞는 값을 찾으면 되는 간단한 문제이다. 최소한의 반복을 위해 H-Index의 경계값을 넘어선 값부터는 읽지 않게 코드를 작성했다.

### 후기

C++를 몰랐던 1년전의 나였다면 정렬을 직접 만드느라 시간을 많이 소비했을 것 같다.
