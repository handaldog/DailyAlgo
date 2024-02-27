# 7️⃣6️⃣ [프로그래머스] 스킬 트리 </span> 

---
### 📃 문제 설명
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 
라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 
따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 
가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/98918cd0-3463-41e4-8052-5bc7e1364d5d)


---
### ❗️ 풀이 
1. 우선 스킬 순서를 map에 담는다. -> char, 스킬 인덱스로
2. 그리고 스킬트리 길이를 돌면서 우선 맵에 스킬이 있는 있는 지 확인하기
3. 있다면 그 바로 선행 스킬이 있는 지 확인
4. 없다면 flag를 false로 두고 break
5. flag 가 true면 answer++ 하


--- 
### 👨‍💻 배운 점


---
### 💰 코드
```
import java.util.*;
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        
        HashMap<Character, Integer> wordmap = new HashMap<>();
        
        
        
        for(int i=0;i<skill.length();i++){
            wordmap.put(skill.charAt(i), i);
        }
        
        for(int i=0;i<skill_trees.length;i++){
            boolean flag = true;
            HashSet<Character> powerset = new HashSet<>();
            for(int j=0;j<skill_trees[i].length();j++){
                
              if(wordmap.containsKey(skill_trees[i].charAt(j))){
                  int num = wordmap.get(skill_trees[i].charAt(j));
                  
                  if(num == 0){
                      powerset.add(skill.charAt(num));
                  }
                  else{
                      if(powerset.contains(skill.charAt(num-1))){
                          powerset.add(skill.charAt(num));
                   
                        }
                      else{
                          flag = false;
                          break;
                      }
                      
                  }
                  
              }  
            }
            
            if(flag){
                // System.out.println("1 : " + i);
                answer++;
            }
            
        }
        return answer;
    }
}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/bb6b6592-1940-41bb-9b6e-d7ba3fc522d4)

