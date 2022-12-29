
#level2 #cpp #writeup  
[문제](https://school.programmers.co.kr/learn/courses/30/lessons/12951)  
template : [[template of writeup]]  

## 문제 설명  

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)  
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.  

## 제한 조건  

- s는 길이 1 이상 200 이하인 문자열입니다.  
- s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.  
	- 숫자는 단어의 첫 문자로만 나옵니다.  
	- 숫자로만 이루어진 단어는 없습니다.  
	- 공백문자가 연속해서 나올 수 있습니다.  

## 입출력 예  

| s                       | return                  |  
| ----------------------- | ----------------------- |  
| "3people unFollowed me" | "3people Unfollowed Me" |  
| "for the last week"     | "For The Last Week"     |  

## 풀이  

### 코드  

```  
#include <string>  
#include <vector>  

using namespace std;  

string solution(string s) {  
    string answer = "";  
    bool flag = true;  
    
    for(int i = 0; i < s.length(); i++) {  
        if(s[i] == ' ') {  
            flag = true;  
        }  
        else if(flag && s[i] >= 'a' && s[i] <= 'z') {  
            s[i] -= 0x20;  
            flag = false;  
        }  
        else if(!flag && s[i] >= 'A' && s[i] <= 'Z') {  
            s[i] += 0x20;  
        }  
        else {  
            flag = false;  
        }  
    }  
    
    answer.append(s);  
    
    return answer;  
}  
```  

### 설명  

1. 주어진 문자열을 처음부터 끝까지 읽는다.  
2. 공백 다음에 오는 소문자는 대문자로 변경한다.  
3. 그 외 대문자는 모두 소문자로 변경한다.  
4. 숫자는 위 조건 1, 2에 해당되지 않는다.  

**공백을 찾아 다음 문자를 변경하는게 핵심이다.**  
**그 외 경우는 모두 소문자로 변경한다. (숫자 제외)**  

1. 공백을 발견하면 flag를 설정한다.  
2. flag가 설정되면 다음문자를 대문자로 변경한다.  
3. flag가 없을때는 문자를 소문자로 변경한다.  
