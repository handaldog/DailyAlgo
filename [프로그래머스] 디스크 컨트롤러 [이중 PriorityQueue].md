# 5️⃣7️⃣ [프로그래머스] 디스크 컨트롤러 </span> 

---
### 📃 문제 설명
하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 
가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어

- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청
와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/7afcc304-36ea-45c2-bfae-4339ada4f1de)
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/4e7ad87b-7ea2-4e87-bf42-5b0f2fdee94d)

- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)

- 이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 
작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)


---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/b08bf4bd-776a-4659-ac86-ecd49079ded8)


---
### ❗️ 풀이 
1. PriorityQueue 두개를 이용해서 구현했다.
2. 소요시간과 진짜 시간을 두개로 나눠서 계산했다.
3. 우선, 모든 것을 요청시간으로 오름차순을 한다.
4. 하나를 빼서 기준으로 해놓은 다음
5. 기준 시간 안에 들어올 수 있는 작업들을 다른 큐에 넣는다.
6. 다른 큐가 비어있으면 작업돌리고 다시 모든 작업을 넣는다.
7. 이런식으로 구현해 나갔다.


--- 
### 👨‍💻 배운 점
1. 테스트 케이스는 되는데 제출만 하면 틀리길래 거의 하루를 버렸다.
2. 알고보니,, priorityqueue조건을 잘못해서 그랬다..ㅠ

---
### 💰 코드
```
import java.util.*;

class Solution {
    
    static class node implements Comparable<node>{
        int respon;
        int amount;
        
        node(int respon, int amount){
            this.respon = respon;
            this.amount = amount;
        }
        
        @Override
        public int compareTo(node n){
            if(this.respon > n.respon)return 1;
            else if(this.respon == n.respon){
                return this.amount - n.amount;
            }
            return -1;
            
            
                }
    }
    
    static class edge implements Comparable<edge>{
        int respon;
        int amount;
        
        edge(int respon, int amount){
            this.respon = respon;
            this.amount = amount;
        }
        
        @Override
        public int compareTo(edge e){
           return this.amount - e.amount;
                }
    }
    
    public int solution(int[][] jobs) {
        int answer = 0;
        
        int time = 0;
        
        int realtime = 0;
        
        PriorityQueue<node> nodepq = new PriorityQueue<>();
        
        PriorityQueue<edge> edgepq = new PriorityQueue<>();
        
        for(int i=0;i<jobs.length;i++){
          
            nodepq.offer(new node (jobs[i][0], jobs[i][1]));
          
        }
        
        node no = nodepq.poll();
        
        realtime+= no.amount + no.respon;
        
        time+=no.amount;
     
    while(!nodepq.isEmpty()){
        
        no = nodepq.peek();

            while(!nodepq.isEmpty() && realtime - no.respon >= 0){
                
            edgepq.offer(new edge(no.respon, no.amount));
             
            nodepq.poll();
                
            no = nodepq.peek();
            
            }
        
            if (!edgepq.isEmpty()){
                
            edge ed = edgepq.poll();
                    
            time += (realtime-ed.respon) + ed.amount;
            
            realtime += ed.amount;
            }
        
            else if(!nodepq.isEmpty() && edgepq.isEmpty()){
            
            no = nodepq.poll();
            realtime += no.amount + (no.respon-realtime);
            time += no.amount;
        }
    }
        
        if (!edgepq.isEmpty() && nodepq.isEmpty()){
            
            while(!edgepq.isEmpty()){
                
            edge ed = edgepq.poll();
                    
            time += (realtime-ed.respon) + ed.amount;
            
            realtime += ed.amount;
                
            }
            
            }
    
        return (int)Math.floor(time/jobs.length);
    }
}

```
