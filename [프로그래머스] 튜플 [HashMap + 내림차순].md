# 6️⃣1️⃣ [프로그래머스] 튜플 </span> 

---
### 📃 문제 설명
셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. 
n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.

(a1, a2, a3, ..., an)
튜플은 다음과 같은 성질을 가지고 있습니다.

중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
튜플의 원소 개수는 유한합니다.
원소의 개수가 n개이고, 중복되는 원소가 없는 튜플 (a1, a2, a3, ..., an)이 주어질 때(단, a1, a2, ..., an은 자연수), 
이는 다음과 같이 집합 기호 '{', '}'를 이용해 표현할 수 있습니다.

{{a1}, {a1, a2}, {a1, a2, a3}, {a1, a2, a3, a4}, ... {a1, a2, a3, a4, ..., an}}
예를 들어 튜플이 (2, 1, 3, 4)인 경우 이는

{{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
와 같이 표현할 수 있습니다. 이때, 집합은 원소의 순서가 바뀌어도 상관없으므로

{{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
{{2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
{{1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}
는 모두 같은 튜플 (2, 1, 3, 4)를 나타냅니다.

특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, 
s가 표현하는 튜플을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/ec4c7c05-ea30-4eac-ab46-c29171d6309e)


---
### ❗️ 풀이 
1. 먼저 숫자만 골라내기 위해서 ,을 기준으로 split을 했다.
2. 그리고 배열을 돌면서 숫자가 아닌 부분은 모두 ""으로 변환시키면 숫자만 남는다.
3. 그 숫자를 map에 넣어 나온 갯수를 셌고
4. 개수에 따른 내림차순을 통해
5. 답을 도출해냈다.


--- 
### 👨‍💻 배운 점
1. HashMap의 내림차순 오름차순을 배웠다. 시험보기전에 꼭 암기 해갈것.
2. 참고 https://velog.io/@dev-easy/Java-Map%EC%9D%84-Key-Value%EB%A1%9C-%EC%A0%95%EB%A0%AC%ED%95%98%EA%B8%B0#2value-%EA%B0%92%EC%9D%84-%EA%B8%B0%EC%A4%80%EC%9C%BC%EB%A1%9C-%EC%A0%95%EB%A0%AC%ED%95%98%EA%B8%B0
List<Integer> keySet = new ArrayList<>(map.keySet());
        
        keySet.sort((o1, o2) -> map.get(o2).compareTo(map.get(o1))); // 내림차
---
### 💰 코드
```
import java.util.*;

class Solution {
    
  
    public int[] solution(String s) {
        
        
        HashMap<Integer, Integer> map = new HashMap<>();
        
        String[] word = s.split(",");
    
        for(int i=0;i<word.length;i++){
            
            word[i] = word[i].replaceAll("[^0-9]", "");
            
            int number = Integer.parseInt(word[i]);
            
            map.put(number, map.getOrDefault(number,0)+1);
            
        }
        
        List<Integer> keySet = new ArrayList<>(map.keySet());
        
        // List<Integer> keySet = new ArrayList<>(map.keySet());
        
        keySet.sort((o1, o2) -> map.get(o2).compareTo(map.get(o1)));
        
        // keySet.sort((o1, o2) -> map.get(o2).compareTo(map.get(o1)));
        
        int[] answer = new int [map.size()];
        
        int cc = 0;
        for(int i : keySet){
            answer[cc] = i;
            cc++;
            
        }
        
        return answer;
    }
}

```
