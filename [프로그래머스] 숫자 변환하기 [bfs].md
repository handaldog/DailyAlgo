# 8️⃣3️⃣ [프로그래머스] 숫자 변환하기 </span> 

---
### 📃 문제 설명
자연수 x를 y로 변환하려고 합니다. 사용할 수 있는 연산은 다음과 같습니다.

x에 n을 더합니다.
x에 2를 곱합니다.
x에 3을 곱합니다.
자연수 x, y, n이 매개변수로 주어질 때, x를 y로 변환하기 위해 필요한 최소 연산 횟수를 return하도록 solution 함수를 완성해주세요. 
이때 x를 y로 만들 수 없다면 -1을 return 해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/7e49dd0b-9801-4b86-82b4-d863d8b1dd79)


---
### ❗️ 풀이 
1. edge라는 클래스를 만들어서 que에 넣어둔다.
2. bfs를 돌리면서, que에 +n, *2, *3한 값을 넣어주고
3. set을 해주는 이유는 중복값 걸러내기 위함. (시간 초과 예방)

---
### 💰 코드
```
import java.util.*;

class Solution {
    static int answer;
    static HashSet<Long> set = new HashSet<>();
    
    static class edge{
        long number;
        int cnt;
        
        edge(long number, int cnt){
            this.number = number;
            this.cnt = cnt;
        }
    }   
    
    
    public int solution(int x, int y, int n) {
        
        
        answer = 1000000;
        
        if(x == y){
            answer = 0;
            return answer;
        }
        
        bfs(x,y,n,0);
        
        return answer;
    }
    public void bfs(long x, long y, long n, int cnt){        
        
        Queue<edge> que = new LinkedList<>();
        
        que.offer(new edge(x,0));
        
        while(!que.isEmpty()){
            
            edge num = que.poll();
            
            if(num.number == y){
            answer = num.cnt;
            return;
            }
            
            if(set.contains(num.number))continue; 
            
                set.add(num.number);
            
                if(num.number+n <= y){
                  que.offer(new edge((num.number+n), num.cnt+1));  
                }
                if(num.number*2 <= y){
                   que.offer(new edge(num.number*2, num.cnt+1)); 
                }
                if(num.number*3 <= y){
                    que.offer(new edge(num.number*3, num.cnt+1));
                }
          
            
        }
        answer = -1;
        return;
        
    }
}
```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/efe38aec-8a55-49ab-b07e-6ececebda69d)

