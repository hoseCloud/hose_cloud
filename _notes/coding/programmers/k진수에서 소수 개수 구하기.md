
#level2 #cpp #writeup  
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/92335)  
template : [[template of writeup]]  

## 문제 설명  

양의 정수 `n`이 주어집니다. 이 숫자를 `k`진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.  

- `0P0`처럼 소수 양쪽에 0이 있는 경우  
- `P0`처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우  
- `0P`처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우  
- `P`처럼 소수 양쪽에 아무것도 없는 경우  
- 단, `P`는 각 자릿수에 0을 포함하지 않는 소수입니다.  
    - 예를 들어, 101은 `P`가 될 수 없습니다.  

예를 들어, 437674을 3진수로 바꾸면 `211`0`2`01010`11`입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 `k`진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 `P0` 형태에서 찾을 수 있으며, 2는 `0P0`에서, 11은 `0P`에서 찾을 수 있습니다.  

정수 `n`과 `k`가 매개변수로 주어집니다. `n`을 `k`진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 **위 조건에 맞는 소수**의 개수를 return 하도록 solution 함수를 완성해 주세요.  

## 제한 조건  

- 1 ≤ `n` ≤ 1,000,000  
- 3 ≤ `k` ≤ 10  

## 입출력 예  

| n      | k   | result |  
| ------ | --- | ------ |  
| 437674 | 3   | 3      |  
| 110011 | 10  | 2      |  

## 풀이  

### 코드  

```  
#include <string>  
#include <vector>  
#include <cmath>  

using namespace std;  

bool is_prime(unsigned long long n);  

int solution(int n, int k) {  
    int answer = 0;  
    string conv = "0";  
    
    while(n >= k) {  
        conv.push_back(n % k + 0x30);  
        n /= k;  
    }  
    conv.push_back(n + 0x30);  
    
    string num = "";  
    for(int i = conv.size()-1; i >= 0; i--) {  
        if(conv[i] == '0') {  
            if(is_prime(stoull(num))) answer++;  
            num.clear();  
        }  
        else {  
            num.push_back(conv[i]);  
        }  
    }  
    
    return answer;  
}  

bool is_prime(unsigned long long n) {  
    if(n <= 1) return false;  
    
    for(int i = 2; i < (unsigned long long)(sqrt(n)+1); i++) {  
        if(n % i == 0) return false;  
    }  
    return true;  
}  
```  

### 설명  

문제의 핵심은 **k진수로 변환하고 소수를 판별하는 것**이다.  
k진수 변환과정에서 나오는 숫자들을 string에 넣는다. 소수 판별을 위한 10진수 변환 과정에서 string을 거꾸로 읽으면 reverse를 안해도 된다. 소수 판별은 2~$\sqrt{n}$까지 비교하면 된다.  
