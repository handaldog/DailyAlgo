# 4️⃣2️⃣ [백준] 게임을 만든 동준이 </span> 

---
### 📃 문제 설명
학교에서 그래픽스 수업을 들은 동준이는 수업시간에 들은 내용을 바탕으로 스마트폰 게임을 만들었다. 게임에는 총 N개의 레벨이 있고, 
각 레벨을 클리어할 때 마다 점수가 주어진다. 플레이어의 점수는 레벨을 클리어하면서 얻은 점수의 합으로, 
이 점수를 바탕으로 온라인 순위를 매긴다. 동준이는 레벨을 난이도 순으로 배치했다. 하지만, 실수로 쉬운 레벨이 어려운 레벨보다 점수를 많이 받는 경우를 만들었다.

이 문제를 해결하기 위해 동준이는 특정 레벨의 점수를 감소시키려고 한다. 이렇게해서 각 레벨을 클리어할 때 주는 점수가 증가하게 만들려고 한다.

각 레벨을 클리어할 때 얻는 점수가 주어졌을 때, 몇 번 감소시키면 되는지 구하는 프로그램을 작성하시오. 
점수는 항상 양수이어야 하고, 1만큼 감소시키는 것이 1번이다. 항상 답이 존재하는 경우만 주어진다. 
정답이 여러 가지인 경우에는 점수를 내리는 것을 최소한으로 하는 방법을 찾아야 한다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/30cadb42-ce92-4adf-a65f-b057efadcc0e)


---
### ❗️ 풀이 
1. 그리디를 연습하고 싶어서 쉬운 문제부터 풀어봤다.
2. 맨 뒤 부분부터 계산해나가면서 뒤에가 자신보다 크면 continue, 같거나 작으면 자신 - 뒤친구 -1 을 하게 되면 내가 빼야할 수가 나온다.
3. 이 수를 가지고 answer에 축적하고
4. 자신 - 빼야할 수 를 빼면 된다.


--- 
### 👨‍💻 배운 점
1. Greedy를 연습을 왕창해서 잘할 거다!!

---
### 💰 코드
```
import java.util.*;

public class Main {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n =  sc.nextInt();
		
		int answer = 0;
		
		int arr[] = new int [n];
		
		for(int i=0;i<n;i++) {
			arr[i] = sc.nextInt();
		}
		
		for(int i=arr.length-1;i>0;i--) {
			if(arr[i] > arr[i-1])continue;
			
			int dif = arr[i] - arr[i-1] -1;
			
			arr[i-1] -= dif * -1;
			
			answer += dif *-1;
			
		}
		
		System.out.println(answer);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/c37ff722-eb02-448c-857a-a6f2bb0d61bb)
