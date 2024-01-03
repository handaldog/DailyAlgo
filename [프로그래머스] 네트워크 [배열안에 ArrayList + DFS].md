# 3️⃣4️⃣ [프로그래머스] 네트워크 </span> 

---
### 📃 문제 설명
네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 
컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/be2de672-c239-4d36-9218-a0c84dfdb9ba)


---
### ❗️ 풀이 
1. 배열안 ArrayList로 네트워크를 형성해서 visit 해가며 진행하다가
2. dfs안에 들어가는 갯수를 같이 세어주면 된다.


--- 
### 👨‍💻 배운 점
1. 다시한번 배열안에 ArrayList를 복기하였다.

---
### 💰 코드
```
import java.util.*;
class Solution {
    
    static ArrayList<Integer>[] list;
    
    static boolean visit[];
    
    public int solution(int n, int[][] computers) {
        
        int size = computers.length;
        
        list = new ArrayList[size];
        
        visit = new boolean[size];
        
        for(int i=0;i<size;i++){
            list[i] = new ArrayList();
        }
        
        for(int i=0;i<size;i++){
            for(int j=0;j<size;j++){
                if(i==j)continue;
                if(computers[i][j] == 1){
                    list[i].add(j);
                }
                
            }
        }
        
         int answer = 0;
        
        // 연결 확인
        for(int i=0;i<size;i++){
            if(!visit[i]){
                answer++;
                visit[i]=true;
                dfs(i);
            
            }

        }
        return answer;
    }
    public static void dfs(int network){
        for(int i=0;i<list[network].size();i++){
            if(!visit[list[network].get(i)]){
                visit[list[network].get(i)] = true;
                dfs(list[network].get(i));
            }
        }
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/ab2f763b-bb6e-48b8-8569-77d40e217dc0)

