# 7️⃣3️⃣ [프로그래머스] 방문 길이 </span> 

---
### 📃 문제 설명
문제 길이가 길어서 
링크로 대체합니다.

https://school.programmers.co.kr/learn/courses/30/lessons/49994

---
### 🔑 출력 형식


---
### ❗️ 풀이 
1. 방문 할 수 있는 부분들은 10 x 10 이라고 생각할 수도 있다.
2. 우선 방향키에 대한 부분을 map에 집어넣고 객체를 만들어서 입력한다.
3. dirs의 길이만큼 돌면서 방향에 대한 키를 map에서 꺼내 사용한다.
4. 그리고 중복값을 해결해 주기 위해 set에 String 형태로 집어넣어준다.
5. 여기서 주의할 점은 URU도 신경써야 하기때문에 양쪽 다 set에 넣어줘야 한다.
6. 그리고 둘다 포함이 안되있으면 set에 넣고 answer++한다.


--- 
### 👨‍💻 배운 점
1. 방향에 대해 고민을 많이 했다. set을 이용하는 법 그리고 방향을 String 으로 바꾸는 방법을 배웠다.

---
### 💰 코드
```
import java.util.*;
class Solution {
    
    static class point{
        int x;
        int y;
        
        point(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
    
    public int solution(String dirs) {
        int answer = 0;
        
      
        
        int curx = 5;
        int cury = 5;
        
        HashMap<Character, point> map = new HashMap<>();
        
        HashSet<String> set = new HashSet<>();
        
        map.put('U', new point(1,0));
        map.put('D', new point(-1,0));
        map.put('R', new point(0,1));
        map.put('L', new point(0,-1));
        
        for(int i=0;i<dirs.length();i++){
            char ch = dirs.charAt(i);
            point po = map.get(ch);
            int nexti = po.x + curx;
            int nextj = po.y + cury;
            String str1 = Integer.toString(curx) + Integer.toString(cury) + 
                Integer.toString(nexti) + Integer.toString(nextj);
            
            String str2 = Integer.toString(nexti) + Integer.toString(nextj) + 
                Integer.toString(curx) + Integer.toString(cury);
            
            if(nexti >=0 && nextj >= 0 && nexti <= 10 && nextj <= 10){
                if(!set.contains(str1) && !set.contains(str2)){
                    set.add(str1);
                    set.add(str2);
                    answer++;
                }
                curx = nexti;
                cury = nextj;
                
            }
        }
        
        return answer;
    }
}

```
