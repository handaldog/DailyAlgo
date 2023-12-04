# 1️⃣1️⃣ [프로그래머스] N개의 최소공배수 </span> 

---
### 📃 문제 설명
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 
예를 들어 2와 7의 최소공배수는 14가 됩니다. 
정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. 
n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/98c221b0-f36f-4f94-8d6a-18d682fa2c30)

---
### ❗️ 풀이 
1. 바로 보자마자 제일 큰수의 배수에 모든 수가 해당되면 크게 최소 공배수라고 생각했다.
2. 제일 큰수의 배수를 loop로 돌리면서 모둔 작은 수들이 큰것의 배수가 0으로 딱 떨어지면 그 수가 바로 최소공배수라는 것을 깨달았다. 

--- 
### 👨‍💻 배운 점


---
### 💰 코드
```
class Solution {
    public int solution(int[] arr) {
        int answer = 0;
        
        
        int  cnt =0;
        while(true){
            boolean flag = true;
            cnt++;
            int res = arr[arr.length-1]*cnt;
            
            for(int i=0;i<arr.length;i++){
                if(res%arr[i] != 0){
                    flag = false;
                    continue;
                }
            }
            if(flag){
                return res;
            }
        }
       
    }
}

```
