# 6️⃣2️⃣ [프로그래머스] 땅따먹기 </span> 

---
### 📃 문제 설명
땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 
1행부터 땅을 밟으며 한 행씩 내려올 때, 
각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. 단, 땅따먹기 게임에는 한 행씩 내려올 때, 
같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.

예를 들면,

| 1 | 2 | 3 | 5 |

| 5 | 6 | 7 | 8 |

| 4 | 3 | 2 | 1 |

로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.

마지막 행까지 모두 내려왔을 때, 얻을 수 있는 점수의 최대값을 return하는 solution 함수를 완성해 주세요. 
위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/bfb4ec83-3c1c-4dc8-a72b-41c844eef922)


---
### ❗️ 풀이 
1. 맨처음 행은 아무거나 처음 밟는 거기때문에 다음 행부터 시작한다.
2. 한 행을 선택하게 되면 자기자신 바로 위의 칸 제외하고 자기자신 + 위의 칸 더한것 중 가장 큰 것을 골라서 dp에 저장하면 된다.
3. 그리고 그 전 행의 기록이 그다음에 쓰일 수 있도록 land = dp 해준 후
4. 끝까지 돌면 된다.
5. 그리고 dp의 마지막 칸 중 가장 큰 수가 답이다.


--- 
### 👨‍💻 배운 점
1. 예전에 못 푼 문제인데 다시 돌아와서 풀리니 기부닝 좋다.

---
### 💰 코드
[DP사용 안한 코드]
```
import java.util.*;
class Solution {
    
    static int recurs[];
    static int max = -1;
    
    int solution(int[][] land) {
        
        int answer = 0;
        
        recurs = new int [land.length];
        
        int length = land.length;
        
        recur(0,length, land);
    

        return max;
    }
    
     public static void recur(int idx, int length, int land[][]){

        if(idx == length){
            
          
            
            for(int j=0;j<length-1;j++){
                if(recurs[j] == recurs[j+1]){
                   return;
                }
            }
            
           
                int sum = 0;
            
                for(int h=0;h<length;h++){
                    sum += land[h][recurs[h]];
                }
                
                max = Math.max(max, sum);
            
            
            return;
        }
        for(int i=0;i<4;i++){
            recurs[idx] = i;
            
            recur(idx+1,length,land);
        }
        
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/074febab-7f64-4164-b574-27eb81116bcd)
[DP 사용 한 코]
```
import java.util.*;

class Solution {
    int solution(int[][] land) {
        int answer = 0;
        
        int dp[][] = new int [land.length][4];
        
        for(int i=1;i<land.length;i++){
            for(int k=0;k<4;k++){
               for(int j=0;j<4;j++){
                if(k == j)continue;
                   dp[i][k] = Math.max(land[i][k] + land[i-1][j], dp[i][k]);
                    } 
                }
            for(int j=0;j<4;j++){
                land[i][j] = dp[i][j];
            }
            
        }
        
        for(int i=0;i<4;i++){
            answer = Math.max(answer, dp[land.length-1][i]);
        }

        return answer;
    }
}
```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/4740449f-69c7-4b08-85a9-9fda797fa76b)
