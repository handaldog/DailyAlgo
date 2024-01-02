# 3️⃣1️⃣ [프로그래머스] 정수 삼각형 </span> 

---
### 📃 문제 설명
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/7ab08cfa-9441-4d18-8fda-4038c74c0e8e)


위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다.
아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

제한사항
삼각형의 높이는 1 이상 500 이하입니다.
삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/09b705a8-8098-48ef-a214-a5d488ac1e7f)


---
### ❗️ 풀이 
1. DP로 큰수를 골라서 더해주면 된다.


--- 
### 👨‍💻 배운 점
1. DP로 푸는 방식에 대해 고민해보는 시간을 가졌다.

---
### 💰 코드
```
class Solution {
    public int solution(int[][] triangle) {
        
        
        
        for(int i=1;i<triangle.length;i++){
            for(int j=0;j<triangle[i].length;j++){
                
                if(j==0){
                triangle[i][j] += triangle[i-1][j];
                }
                
                else if(i == j){
                    triangle[i][j] += triangle[i-1][j-1];
                    
                }
                    
                else{
                    triangle[i][j] += Math.max(triangle[i-1][j-1], triangle[i-1][j]);
                    
                }
            }
        }
         int answer = -1;
        
        for(int i=0;i<triangle.length;i++){
            // System.out.println(triangle[4][i]+ " ");
            answer = Math.max(triangle[triangle.length-1][i], answer);
        }
        
       
        return answer;
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/a42a2e63-329f-4394-b632-a1088f8a7866)

