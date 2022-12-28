# N개의 최소공배수

#level2 #cpp #writeup
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/12953)
template : [[template of writeup]]

## 문제 설명

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

## 제한 조건

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

## 입출력 예

| arr             | result |
| --------------- | ------ |
| `[2, 6, 8, 14]` | 168    |
| `[1, 2, 3]`     | 6      |

## 풀이

### 코드

```
#include <string>
#include <vector>

using namespace std;

int lcm(int a, int b);
int gcd(int a, int b);

int solution(vector<int> arr) {
    int answer = 1;
    
    for(auto n : arr) {
        answer = lcm(answer, n);
    }
    
    return answer;
}

int lcm(int a, int b) {
    return (a*b) / gcd(a, b);
}

int gcd(int a, int b) {
    return a % b == 0 ? b : gcd(b, a % b);
}
```

### 설명

최대공약수(GCD)와 최소공배수(LCM) 문제다. GCD 연산을 쉽게 떠올려서 쉽게 풀었다.

### 후기

간단한 GCD연산을 어떻게 하는지 잊어서 구글링했다... 자주 쓰는 수식이나 공식은 정리해야겠다.
