# 6️⃣5️⃣ [프로그래머스] 가장 큰 수 </span> 

---
### 📃 문제 설명
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 
이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 
순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/fa874d54-3b1b-41fa-b023-61b0d89cdf4a)


---
### ❗️ 풀이 
1. priorityQueue를 이용해서 정렬했다.
2. 다만, 조건을 달아줘야한다. this + number이 큰 지 아니면 그 반대인지에 따라 return 값을 내뱉으면 된다.
3. 그러고 0,0,0 만 있는 게 있을 수 도 있으니깐 조건을 나중에 또 설정해줘야 한다.


--- 
### 👨‍💻 배운 점
1. 다양한 조건으로도 priorityqueue가 되는 게 신기했다.


---
### 💰 코드
```
import java.util.*;
class Solution {
    
    static class number implements Comparable<number>{
        String num;
        
        number(String num){
            this.num = num;
        }
        
        @Override
        public int compareTo(number n){
          
            if(Long.parseLong(this.num + n.num) >= Long.parseLong(n.num + this.num)){
                return -1;
            }
            else {
                return 1;
            }
         
        }
    }
    public String solution(int[] numbers) {
        String answer = "";
        
        PriorityQueue<number> pq = new PriorityQueue<>();
        
        for(int i=0;i<numbers.length;i++){
            String word = Integer.toString(numbers[i]);
            pq.offer(new number(word));
        }
        
        Long check = 0L;
        
        while(!pq.isEmpty()){
            
            String n = pq.poll().num;
            check += Long.parseLong(n);
            
             answer += n;   
            
        }
        
        if(check == 0){
            answer = "";
            answer += "0";
        }
        
        
        return answer;
    }
}

```
