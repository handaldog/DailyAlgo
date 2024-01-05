# 4️⃣4️⃣ [백준] 회의실 배정 </span> 

---
### 📃 문제 설명
한 개의 회의실이 있는데 이를 사용하고자 하는 N개의 회의에 대하여 회의실 사용표를 만들려고 한다. 각 회의 I에 대해 시작시간과 끝나는 시간이 주어져 있고, 
각 회의가 겹치지 않게 하면서 회의실을 사용할 수 있는 회의의 최대 개수를 찾아보자. 
단, 회의는 한번 시작하면 중간에 중단될 수 없으며 한 회의가 끝나는 것과 동시에 다음 회의가 시작될 수 있다. 회의의 시작시간과 끝나는 시간이 같을 수도 있다. 
이 경우에는 시작하자마자 끝나는 것으로 생각하면 된다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/2d48d0d1-60c3-4992-9341-d445aafef576)


---
### ❗️ 풀이 
1. 우선순위 큐를 사용하여 끝나는 수로 오름차순하였다.
2. 주의할 점은 끝나는 수가 같을때는 시작시간으로 오름차순하는 것이다.
3. 맨 처음 center를 정하는데 이 수는 큐의 맨 앞 의 end 타임으로 지정한다.
4. 그리고 pq.poll 하면서 center보다 끝나는 수가 작으면 continue 하고 나머지는 모두 채택해서 center을 끝나는 수로 바꾸고, answer++ 해준다.


--- 
### 👨‍💻 배운 점
1. comparable을 오랜만에 해서 다시 복기했다. -> 시험전에 한번봐서 암기해야할 듯.
2. 수가 크다 싶으면 Long을 쓰는게 나을 것 같다.

---
### 💰 코드
```

import java.util.*;

public class Main {
	
	static class Time implements Comparable<Time>{
		Long start;
		Long end;
		
		Time(Long start, Long end){
			this.start = start;
			this.end = end;
		}

		@Override
		public int compareTo(Time t) {
			if(this.end == t.end) {
				return (int) (this.start - t.start);
			}
			return (int) (this.end - t.end);
		}

		
	}

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);

		PriorityQueue<Time> pq = new PriorityQueue<>();
		
		Long n = sc.nextLong();
		
		int answer = 1;
		
		for(int i=0;i<n;i++) {
			pq.offer(new Time(sc.nextLong(), sc.nextLong()));
		}
		Time ti = pq.poll();
		Long center = ti.end;
		
		while(!pq.isEmpty()) {
			
			Time t = pq.poll();
			
			if(center > t.start)continue;
			center = t.end;
			answer++;
			
			
		}
		
		System.out.println(answer);

	}

}


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/c276c957-bc6e-410a-baab-2f77f5990979)
