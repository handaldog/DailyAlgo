# 6️⃣0️⃣ [프로그래머스] JadenCase </span> 

---
### 📃 문제 설명
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 
단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5e4339af-bbb9-46b9-937d-ed42224535b1)


---
### ❗️ 풀이 
1. 먼저 모든 문자열을 소문자로 바꿔준다.
2. LinkedList에 substring 해서 하나하나 넣어준다. (" " 연속이 있을 수 도 있기 때문에 split 을 안한다.)
3. 무조건 맨 처음꺼는 upperCase를 해준다.
4. list 사이즈만큼 돌면서 " "을 만나면 그 다음거를 uppercase()한거를 끼워넣고 그 전꺼를 삭제한다.
5. 이렇게 반복작업하면 끝. 


--- 
### 👨‍💻 배운 점
1. uppercase, lowercase는 문자열만 됨. char형태 안됨.
2. 안 풀리던 문제였는데 오랜만에 푸니 풀렸다 !!!

---
### 💰 코드
```
import java.util.*;

class Solution {
    public String solution(String s) {
        
        String answer = "";
        
      s = s.toLowerCase();
        
        LinkedList<String> list = new LinkedList<>();
        
      for(int i=0;i<s.length();i++){
          list.add(s.substring(i,i+1));
      }
        
        // if(list.size() )
        
        list.add(0, list.get(0).toUpperCase());
        list.remove(1);
        int size = list.size();
        
        for(int i=0;i<size;i++){
            if(list.get(i).equals(" ") && i < size -1 ){
                list.add(i+1, list.get(i+1).toUpperCase());
                list.remove(i+2);
            }
        }
        
        for(int i=0;i<list.size();i++){
            answer += list.get(i);
        }
        return answer;
    }
}

```
