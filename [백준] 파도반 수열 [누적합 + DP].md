# 5️⃣4️⃣ [백준] 파도반 수열 </span> 

---
### 📃 문제 설명
오른쪽 그림과 같이 삼각형이 나선 모양으로 놓여져 있다. 
첫 삼각형은 정삼각형으로 변의 길이는 1이다. 그 다음에는 다음과 같은 과정으로 정삼각형을 계속 추가한다.
나선에서 가장 긴 변의 길이를 k라 했을 때, 그 변에 길이가 k인 정삼각형을 추가한다.

파도반 수열 P(N)은 나선에 있는 정삼각형의 변의 길이이다. P(1)부터 P(10)까지 첫 10개 숫자는 1, 1, 1, 2, 2, 3, 4, 5, 7, 9이다.

N이 주어졌을 때, P(N)을 구하는 프로그램을 작성하시오.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/bd32e93d-ff6b-48df-9db5-78914f8d87ae)


---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/30360d74-60af-4966-99df-9884045b2597)


---
### ❗️ 풀이 
1. 누적합을 이용한 DP방식으로 풀면된다.

--- 
### 👨‍💻 배운 점
1. long을 잘 쓰기.

---
### 💰 코드
```

import java.util.*;

public class Main {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		long dp[] = new long [101];
		
		dp[0] = 1;
		dp[1]=1;
		dp[2] = 1;
		
		for(int i=0;i<n;i++) {
			int number = sc.nextInt();
			
			
			
			if(number > 2) {
				for(int j=3;j<number;j++) {
					dp[j] = dp[j-3] + dp[j-2];
				}
			}
			
			System.out.println(dp[number-1]);
			
			
		}

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/72f4af5b-e48c-4cc8-8745-3a9b8ec3281a)
