# 0️⃣ [프로그래머스] 더 맵 </span> 

---
### 📃 문제 설명
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/2a9c306b-97b9-4a2f-8c1a-5bbda92beb0b)


---
### ❗️ 풀이 
1. 10분만에 해결책이 떠올랐던 쉬운 문제였다.
2. 조건 맞추는 것 때문에 10분 더 소요된거 같지만 금방 푼 문제이다.
3. 조건을 잘 보는 것이 중요한 것 같다.
4. PrioirtyQueue는 넣자마자 바로 정렬을 해주기 때문에 pq를 사용했다.
5. 맨 앞에가 무조건 작은 것이기 때문에 앞에꺼를 뺐을 때 K보다 크면 그 뒤는 무조건 큰 것이므로 조건을 첫번째꺼로만 확인했다.
6. 스코빌 지수 이상일때까지 반복했다.


--- 
### 👨‍💻 배운 점
1. 조건을 잘 보자.
2. 큐의 remove도 poll과 같은 역할을 한다. 

---
### 💰 코드
```
import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        for(int i=0;i<scoville.length;i++){
            pq.add(scoville[i]);
        }
        
        while(true){
            
            int one = pq.peek();
            
            if(one >= K){
                return answer;
            }
            
            if(pq.size() == 1){
                return -1;
            }
            
            one = pq.poll();
            int two = pq.poll();
                        
            answer++;
            int spicy = one + (two * 2);
            
            pq.add(spicy);
        }
        
    }
}

```
