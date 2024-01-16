# 4️⃣6️⃣ [백준] 노드사이의 거리 </span> 

---
### 📃 문제 설명
N개의 노드로 이루어진 트리가 주어지고 M개의 두 노드 쌍을 입력받을 때 두 노드 사이의 거리를 출력하라.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/24c9a11e-9477-45cb-847b-210b8b0293fa)


---
### ❗️ 풀이 
1. 우선 양방향 그래프를 배열안 ArrayList를 만들어준다.
2. 그리고 bfs를 돌면서 거리를 더해주는데
3. 주의할 점은 계속 거리를 더해주면 안되고 지나온 거리만 더해야 함으로 que에 넣을때 그 전꺼랑 합해서 넣어줘야 모든 거리가 합해지는 것을 막을 수 있다.


--- 
### 👨‍💻 배운 점
1. bfs 의 주의점. 

---
### 💰 코드
```

import java.util.*;

public class 노드사이의거리 {
	
	static class node{
		int num;
		int weight;
		
		
		node(int num, int weight){
			this.num = num;
			this.weight = weight;
			
		}
	}
	
	
	static ArrayList<node>[] list;
	static boolean visit[];
	static long answer;

	public static void main(String[] args) {
		
		 Scanner sc = new Scanner(System.in);
		 
		 int n = sc.nextInt();
		 int m = sc.nextInt();
		 
		 
		 list = new ArrayList[n+1];
		 
		 
		 for(int i=0;i<=n;i++) {
			 list[i] = new ArrayList();
		 }
		 
		 for(int i=0;i<n-1;i++) {
			 int x = sc.nextInt();
			 int y = sc.nextInt();
			 int w = sc.nextInt();
			 
			 list[x].add(new node(y,w));
			 list[y].add(new node(x,w));
			 
		 }
		 
		 for(int i=0;i<m;i++) {
			 int a = sc.nextInt();
			 int b = sc.nextInt();
			 
			 visit = new boolean[n+1];
			 answer = 0;
			 dfs(a,b);
			 System.out.println(answer);
		 }
	}
	
	public static void dfs(int a, int b) {
		Queue<node> que = new LinkedList<>();
		
		que.offer(new node(a, 0));
		visit[a] = true;
		
		while(!que.isEmpty()) {
			
			node no = que.poll();
			
			for(int i=0;i<list[no.num].size();i++) {
				if(visit[list[no.num].get(i).num])continue;
				visit[list[no.num].get(i).num] = true;
								
				if(list[no.num].get(i).num == b) {
					answer = no.weight + list[no.num].get(i).weight;
					return;
				}
				
				que.offer(new node (list[no.num].get(i).num, no.weight + list[no.num].get(i).weight));
			}
		}
		
	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/802e71a1-71e6-451a-b488-7a57b62e0ea1)
