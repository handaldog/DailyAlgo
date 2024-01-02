# 2️⃣9️⃣ [백준] 쉬운 최단거리 </span> 

---
### 📃 문제 설명

지도가 주어지면 모든 지점에 대해서 목표지점까지의 거리를 구하여라.

문제를 쉽게 만들기 위해 오직 가로와 세로로만 움직일 수 있다고 하자.

---
### 🔑 출력 형식

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/c979f30d-dddc-4a11-be77-4f8ab6d4ba6d)

---
### ❗️ 풀이 
1. 그냥 간단하게 BFS를 사용하여 구현하면된다.
2. 주의해야 할 점은 방문안했으면서 갈 수 있는 길을 -1 처리하는 부분을 조건문 달아서 처리해줘야 한다.


--- 
### 👨‍💻 배운 점
1. Arrays.fill (배열이름, 채울 수 );
- 2차원 배열일때는 for문 돌면서 채워야한 ex) Arrays.fill(arr[i], -1);

---
### 💰 코드
```
package 문자열;


import java.util.*;

public class 쉬운최단거리 {
	
	static Queue<Point> que = new LinkedList<>();
	
	static int di[] = {0,0,1,-1};
	static int dj[] = {1,-1,0,0};
	
	static class Point {
		int x;
		int y;
		int cnt;
		
		Point(int x, int y, int cnt){
			this.x = x;
			this.y = y;
			this.cnt = cnt;
		}
	}

	static int area[][];
	static int resultarea[][];
	static int n,m;
	static boolean visit[][];
	
	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int beforex = 0;
		int beforey = 0;
		
		 n = sc.nextInt();
		 m = sc.nextInt();

		 area = new int[n][m];
		 visit = new boolean[n][m];
		
		for(int i=0;i<n;i++) {
			for(int j=0;j<m;j++) {
				area[i][j] = sc.nextInt();
				if(area[i][j] == 2) {
					beforex = i;
					beforey = j;
				}
			}
		}
		
		que.offer(new Point(beforex, beforey, 0));
		visit[beforex][beforey] = true;
		bfs();
		
				
		for(int i=0;i<n;i++) {
			for(int j=0;j<m;j++) {
				if(!visit[i][j] && area[i][j] == 1) {
					System.out.print(-1 + " ");
				}
				else {
					System.out.print(resultarea[i][j] + " ");
					
				}
			}
			System.out.println();
		}
		
	}
	
	public static void bfs() {
		
		resultarea = new int [n][m];
		
		while(!que.isEmpty()) {
			
			Point p = que.poll();
			
			visit[p.x][p.y] = true;
			
			resultarea[p.x][p.y] = p.cnt;
		
		for(int i=0;i<4;i++) {
			int nexti = p.x + di[i];
			int nextj = p.y + dj[i];
			
			if(nexti >= 0 && nextj >= 0 && nexti < n && nextj < m 
					&& area[nexti][nextj] == 1 && !visit[nexti][nextj]) {
				que.offer(new Point(nexti, nextj, p.cnt + 1));
				visit[nexti][nextj] = true;
			}
		}
		
		}
	
	}

}


```

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/a5216905-1d38-4576-913c-0d9ccad3a4d8)

