# 8️⃣9️⃣ [프로그래머스] 2 x n 타일링 </span> 

---
### 📃 문제 설명
가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

타일을 가로로 배치 하는 경우
타일을 세로로 배치 하는 경우
예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5ce31874-8411-46e0-ab07-4ca84c8d7b5e)


직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/67f0f787-d76d-4050-83af-4d89d5c7778a)


---
### ❗️ 풀이 
1. 현재 타일의 경우의 수는 그 전과 그 전전의 타일의 경우의 수와 같다.


---
### 💰 코드
```
class Solution {
    public int solution(int n) {
      
        
        int block[] = new int [n+1];
        
        block[1] = 1;
        block[2] = 2;
        
        for(int i=3;i<=n;i++){
            block[i] = (block[i-1] + block[i-2])%1000000007;
        }
        
    
        return block[n];
    }
}
```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/fd4cbc02-bce8-4add-a596-ee5718735f13)

