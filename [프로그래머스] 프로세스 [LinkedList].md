#  1️⃣5️⃣ [프로그래머스] 프로세스 </span> 

---
### 📃 문제 설명
운영체제의 역할 중 하나는 컴퓨터 시스템의 자원을 효율적으로 관리하는 것입니다. 
이 문제에서는 운영체제가 다음 규칙에 따라 프로세스를 관리할 경우 특정 프로세스가 몇 번째로 실행되는지 알아내면 됩니다.

1. 실행 대기 큐(Queue)에서 대기중인 프로세스 하나를 꺼냅니다.
2. 큐에 대기중인 프로세스 중 우선순위가 더 높은 프로세스가 있다면 방금 꺼낸 프로세스를 다시 큐에 넣습니다.
3. 만약 그런 프로세스가 없다면 방금 꺼낸 프로세스를 실행합니다.
  3.1 한 번 실행한 프로세스는 다시 큐에 넣지 않고 그대로 종료됩니다.
예를 들어 프로세스 4개 [A, B, C, D]가 순서대로 실행 대기 큐에 들어있고, 우선순위가 [2, 1, 3, 2]라면 [C, D, A, B] 순으로 실행하게 됩니다.

현재 실행 대기 큐(Queue)에 있는 프로세스의 중요도가 순서대로 담긴 배열 priorities와, 몇 번째로 실행되는지 알고싶은 프로세스의 위치를 알려주는 location이 매개변수로 주어질 때, 
해당 프로세스가 몇 번째로 실행되는지 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/8e820586-716c-4b76-82d5-7a15c6874f80)


---
### ❗️ 풀이 
1. 큐/스택을 써야 한다고 해서 쓸려했지만 indexOf 하는 부분에서 막혀버림.
2. 또한 큐는 한번 꺼내면 다시 제자리에 넣기 힘들고 get을 못하기 때문에
3. 이 두가지 문제점을 한번에 해결해줄 LinkedList 를 사용했다.
4. 그냥 기본적인 구현이기때문에 딱히 풀이가 없고, 말 그대로 구현을 했다.


--- 
### 👨‍💻 배운 점
1. indexOf 가 Arraylist 에서만 사용할 수 있다는 것이 다소 충격적이었다.

---
### 💰 코드
```
import java.util.*;
class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 0;
        
        LinkedList<Integer> que = new LinkedList<>();
        LinkedList<Integer> quecopy = new LinkedList<>();
        
        for(int i=0;i<priorities.length;i++){
            que.add(priorities[i]);
            quecopy.add(i);
        }
        
        for(int i=9;i>=2;i--){
            
            while(true){
                int edge = -1;
                
            for(int k=0;k<que.size();k++){
                if(que.get(k) == i){
                    edge = k;
                    break; 
                }
                edge = -1;
            }
            
            if(edge == -1){
                break;
            }
            else {
                for(int j=0;j<edge;j++){
                    int q = que.get(0);
                    que.remove(0);
                    int qc = quecopy.get(0);
                    quecopy.remove(0);
                    que.add(q);
                    quecopy.add(qc);
                } 
                
                que.remove(0);
                int point = quecopy.get(0);
                quecopy.remove(0);
                answer++;
                if(point == location) return answer;
            }
               
                
            
            }
        }
        while(!que.isEmpty()){
                que.remove(0);
                int poi = quecopy.get(0);
                quecopy.remove(0);
                answer++;
                if(poi == location) return answer;
        }
        return 0;
    }
   
}


```
