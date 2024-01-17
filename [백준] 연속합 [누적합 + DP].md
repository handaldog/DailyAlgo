# 5️⃣3️⃣ [백준] 연속  </span> 

---
### 📃 문제 설명
n개의 정수로 이루어진 임의의 수열이 주어진다. 우리는 이 중 연속된 몇 개의 수를 선택해서 구할 수 있는 합 중 가장 큰 합을 구하려고 한다. 단, 수는 한 개 이상 선택해야 한다.

예를 들어서 10, -4, 3, 1, 5, 6, -35, 12, 21, -1 이라는 수열이 주어졌다고 하자. 여기서 정답은 12+21인 33이 정답이 된다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/3e86cb29-41eb-4089-831c-c095ed5e1053)


---
### ❗️ 풀이 
1. 앞에것과 계산했을 때 현재의 값과 계산했을때의 값중 더 큰 거를 두면서 누적합으로 계산해나가고
2. 모든 계산 후에 제일 큰 값을 출력하면 된다.


--- 
### 👨‍💻 배운 점
1. DP의 누적합에 대해 좀 이해하고 있는 것 같다.
2. DP의 좋은 점은 짧은 코딩으로 효율적으로 계산할 수 있다는 것이 매력적인 것 같다.

---
### 💰 코드
```

import java.util.*;

public class 연속합 {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		long arr[] = new long [n];
		
		for(int i=0;i<n;i++) {
			arr[i] = sc.nextInt();
			
			if(i > 0) {
				arr[i] = Math.max(arr[i], arr[i] + arr[i-1]);
			}
		}
		
		Arrays.sort(arr);
		
		System.out.println(arr[n-1]);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/b93165c2-807a-4b87-8da3-b4d2257f4f20)
