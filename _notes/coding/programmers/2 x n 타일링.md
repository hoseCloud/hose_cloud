
#level2 #cpp #writeup  
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/12900)  
template : [[template of writeup]]  

## 문제 설명  

가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.  

- 타일을 가로로 배치 하는 경우  
- 타일을 세로로 배치 하는 경우  

예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.  

![Imgur](https://i.imgur.com/29ANX0f.png)  

직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.  

## 제한 조건  

- 가로의 길이 n은 60,000이하의 자연수 입니다.  
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.  

## 입출력 예  

| n   | result  |  
| --- | ------- |  
| 4   | 5 |  

## 풀이  

### 코드  

```  
#include <string>  
#include <vector>  
#define MAX 1000000007  

using namespace std;  

int dp[3][60001];  

int solution(int n) {  
    int answer = 0;  
    
    dp[1][1] = 1;  
    dp[2][2] = 1;  
    
    if(n > 1) {  
        for(int i = 2; i <= n; i++) {  
            dp[1][i] += dp[1][i-1] + dp[2][i-1];  
            dp[1][i] %= MAX;  
            dp[2][i] += dp[1][i-2] + dp[2][i-2];  
            dp[2][i] %= MAX;  
        }  
    }  
    
    answer = dp[1][n] + dp[2][n];  
    answer %= MAX;  
    
    return answer;  
}  
```  

### 설명  

[[동적 계획법(Dynamic Programming)]]를 이용해 문제를 해결했다.  

### 후기  

처음에는 경우의 수로 계산하려 했으나 큰 수일경우 팩토리얼 계산이 힘들어서 포기했다. 큰 두 수의 곱셈이 가능한 알고리즘을 찾긴 했지만 DP로 풀 수 있는 방법을 생각해 풀었다. 첫 풀이로는 DFS로 해결하려 했지만 역시나 시간초과가 발생했다.  
