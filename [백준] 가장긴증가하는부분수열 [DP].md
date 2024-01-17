# 5️⃣2️⃣ [백준] 가장긴증가하는부분수열 </span> 

---
### 📃 문제 설명
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.


---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5467b2fe-d189-45d1-af6e-40df0a67fc67)


---
### ❗️ 풀이 
ㅜㅡㅜㅡㅜ
1. 다시 한번 풀어봐야 할 문제


--- 
### 👨‍💻 배운 점
1. LIS에 대해 공부를 했다.

---
### 💰 코드
```
package 문자열;
import java.util.*;

public class 가장긴증가하는부분수열 {

	public static void main(String[] args) {
	
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		long arr[] = new long [n];
		
		long dp[] = new long [n];
		
		dp[0]=1;
		
		for(int i=0;i<n;i++) {
			arr[i] = sc.nextInt();
		}
//		
//		for(int i=1;i<n;i++) {
//			if(arr[i] > arr[i-1])dp[i] = dp[i-1]+1;
//			else {
//				dp[i] = dp[i-1];
//			}
//		}
		
		for(int i=1;i<n;i++) {
			long max = 0;
			for(int j=0;j<i;j++) {
				if(arr[i] > arr[j]) {
					max = Math.max(dp[j], max);
				}
			}
			dp[i] = max+1;
			
		}
		
		long max = 0;
		for(int i=0;i<n;i++) {
			
			max = Math.max(dp[i], max);
		}
		
		System.out.println(max);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/b48b6bae-b412-4deb-8a72-de03eda46795)
