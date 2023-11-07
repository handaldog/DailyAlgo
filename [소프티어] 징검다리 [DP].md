# 1️⃣ [소프티어] [징검다리](https://softeer.ai/practice/6293) </span>

---
### 📃 문제 설명
- #### 남북으로 흐르는 개울에 동서로 징검다리가 놓여져 있다.
- #### 이 징검다리의 돌은 들쑥날쑥하여 높이가 모두 다르다. 철수는 개울의 서쪽에서 동쪽으로 높이가 점점 높은 돌을 밟으면서 개울을 지나가려고 한다.
- #### 돌의 높이가 서쪽의 돌부터 동쪽방향으로 주어졌을 때 철수가 밟을 수 있는 돌의 최대 개수는?

---
### 🔑 출력 형식
- #### 첫 번째 줄에 철수가 밟을 수 있는 돌의 최대 개수를 출력하라.


---
### ❗️ 풀이 
- #### dp를 예전부터 공부해보고 싶었기 때문에 이 글을 참조하여 먼저 학습한 다음에 스스로 풀었다. https://cocoon1787.tistory.com/713
- #### 공식을 외우지말고 문제에 따라 응용해 내는 것이 중요한것 같다.
- #### 이 문제도 응용해서 풀었다.


--- 
### 👨‍💻 배운 점
- #### dp를 처음 공부하고 내 손으로 "성공"이라는 문구를 보니 기분이 좋았다.
- #### dp는 배우기엔 어렵지만 터득하고 나면 아주 쉽고 좋은 기술이라고 하는데 빨리 익숙해지고 쉬울정도로 연습해야겠다.


---
### 💰 코드
```
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) {

      Scanner sc = new Scanner(System.in);

      int n = sc.nextInt();

      int arr[] = new int [n];

      int dp[] = new int [n];

      dp[0] = 1;
      
      for(int i=0;i<n;i++){
        arr[i] = sc.nextInt();
      }

      for(int i=1;i<n;i++){
        int max = 0;
        for(int j=0;j<i;j++){
          if(arr[i] > arr[j]) 
            max = Math.max(max, dp[j]);
          
          }
          dp[i] = max + 1;
      }

      int result = 0;
      for(int i=0;i<n;i++){
        // System.out.print(dp[i] + " ");
         result = Math.max(result, dp[i]);  
      }

      System.out.print(result);
      
    }
}


```
