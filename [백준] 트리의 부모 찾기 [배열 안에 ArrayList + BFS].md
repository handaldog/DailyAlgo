# 4️⃣5️⃣ [백준] 트리의 부모 찾기 </span> 

---
### 📃 문제 설명
루트 없는 트리가 주어진다. 이때, 트리의 루트를 1이라고 정했을 때, 각 노드의 부모를 구하는 프로그램을 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/48dddc2f-e4db-4ac4-98da-69c155e1e9d4)


---
### ❗️ 풀이 
1. 간단히 배열안에 ArrayList만들어서
2. 지나간 곳은 continue 하고
3. 안지난 곳은 그곳이 현재 대장의 숫자를 주고 queue에 넣어준다.


--- 
### 👨‍💻 배운 점
1. 메모리랑 시간이 너무 커서 다른 사람들의 방식을 찾아보았다.

---
### 💰 코드
```
package 문자열;
import java.util.*;

public class 트리의부모찾기 {
	
	static int arr[];
	static ArrayList<Integer>[] list;

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
					
		int n = sc.nextInt();
		
		list = new ArrayList[n+1];
		
		arr = new int [n+1];
		
		arr[1] = 1;
		
		for(int i=0;i<=n;i++) {
			list[i] = new ArrayList();
		}
		 
		 for(int i=0;i<n-1;i++) {
			 int x = sc.nextInt();
			 int y = sc.nextInt();
			 
			 list[x].add(y);
			 list[y].add(x);
		 }
		 
		 bfs();
		 
		 for(int i=2;i<=n;i++) {
			 System.out.println(arr[i]);
		 }
		
	}
	static public void bfs() {
		Queue<Integer> que = new LinkedList<>();
		
		que.offer(1);
		
		while(!que.isEmpty()) {
			
			int num = que.poll();
			
			for(int i=0;i<list[num].size();i++) {
				if(arr[list[num].get(i)] > 0)continue;
				arr[list[num].get(i)] = num;
				que.offer(list[num].get(i));
			}
		}
	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/efd4810e-e8e1-4abd-9407-61a7d9c8279f)
