# 4️⃣7️⃣ [백준] 수 찾기 </span> 

---
### 📃 문제 설명
N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/381fc0b5-c989-4e0b-ad60-2928342a8ad8)


---
### ❗️ 풀이 
1. 수가 너무 크기때문에 무조건 이분탐색으로 해야한다.
2. 또한 long 으로도 처리해줘야 시간초과가 안 난다.


--- 
### 👨‍💻 배운 점
1. 수가 클때는 long 인지 살펴봐야함.

---
### 💰 코드
```

import java.util.*;

public class Main {
	
	static int origin[];

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		 origin = new int [n];
		
		for(int i=0;i<n;i++) {
			origin[i] = sc.nextInt();
		}
		
		Arrays.sort(origin);
		
		int m = sc.nextInt();
		
		for(int i=0;i<m;i++) {
			
			long find = sc.nextInt();
			
			binarySearch(find, 0, n-1);
			
		}
		
		
	}
	
	public static void binarySearch(long find, int front, int back) {
		
		if(front > back) {
			System.out.println("0");
			return;
		}
		
		int index = (front + back) /2;
		
				
		if(origin[index] == find) {
			System.out.println("1");
			return;
		}
		if(origin[index] < find) {
			binarySearch(find, index+1, back);
		}
		else {
			binarySearch(find, front, index-1);
		}
		
	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/f2a3f732-1525-40fa-b7c4-a5ac659a2e5c)
