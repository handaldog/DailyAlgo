# 8️⃣ [프로그래머스] 괄호 회전하기 </span> 

---
### 📃 문제 설명
다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.

(), [], {} 는 모두 올바른 괄호 문자열입니다.
만약 A가 올바른 괄호 문자열이라면, (A), [A], {A} 도 올바른 괄호 문자열입니다. 예를 들어, [] 가 올바른 괄호 문자열이므로, ([]) 도 올바른 괄호 문자열입니다.
만약 A, B가 올바른 괄호 문자열이라면, AB 도 올바른 괄호 문자열입니다. 예를 들어, {} 와 ([]) 가 올바른 괄호 문자열이므로, {}([]) 도 올바른 괄호 문자열입니다.
대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 s가 매개변수로 주어집니다. 이 s를 왼쪽으로 x (0 ≤ x < (s의 길이)) 칸만큼 회전시켰을 때 s가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/dailyalgo/assets/96431408/e8261e16-bb9d-48ef-a551-3c7102067701)



---
### ❗️ 풀이 
1. 처음에는 list 와 stack 만 써서 확인을 했지만 통과하지 못했다.
2. 디버깅 하면서 하나하나 따져보니 내가 했던 방식은 '()' 이것만 존재할 때 하는 방식이고 이 문제는 '()', '[]', '{}' 가 존재하므로
3. map을 써서 키 값으로 비교하게 했다.
4. 백트래킹을 위해 flag 를 넣었다.

--- 
### 👨‍💻 배운 점
1. map 과 stack list 를 모두 사용하여 코드를 짜 본 적은 처음이다.
2. 결론 : 재밌다. ㅎ

---
### 💰 코드
```
import java.util.*;

class Solution {
    public int solution(String s) {
        
        HashMap<Character, Character> map = new HashMap<>();
        
        map.put('(', ')');
        map.put('[', ']');
        map.put('{', '}');
        
        int answer = 0;
        
        boolean flag = true;
        
       ArrayList<Character> list = new ArrayList<>();
        
         int len = s.length();
        
        for(int i=0;i<len;i++){
            list.add(s.charAt(i));
        }
        
        for(int j=0;j<len;j++){
            flag = true;
            
                     
            Stack<Character> stack = new Stack<>();
            
         for(int i=0;i<len;i++){
            
            if(list.get(i) == '(' || list.get(i) == '[' || list.get(i) == '{'){
                    
                stack.push(list.get(i));
            }
            else if(!stack.isEmpty()){
                char str = stack.peek();
              
                if(map.get(str) == list.get(i)){
                    
                    stack.pop();
                }
                else{
                        flag = false;
                }
                
            }
             else{
                 flag = false;
             }
        }
            
            if(stack.isEmpty() && flag){
                answer++;
            }
            
            list.add(list.get(0));
            list.remove(0);
            
        }
        
        return answer;
    }
}

```
