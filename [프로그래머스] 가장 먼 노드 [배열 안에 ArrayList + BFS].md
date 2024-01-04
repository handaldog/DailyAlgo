# 4️⃣1️⃣ [프로그래머스] 가장 먼 노드 </span> 

---
### 📃 문제 설명
n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 
1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 
1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/d4c24be6-1081-48ca-a223-e53e1993890e)


---
### ❗️ 풀이 
1. 배열 안에 ArrayList를 넣어 노드를 돌아가면서 확인한다.
2. 여기서 주의해야 할 점은 양방향으로 넣어야 한다는 것.
3. 그리고 BFS를 돌면서 가장 짧은 단위를 따로 배열을 만들어 넣었고
4. 그 배열을 Arrays.sort를 해서 마지막꺼와 같은 거 숫자를 세서 답을 도출했다.


--- 
### 👨‍💻 배운 점
1. 그래프 심화에 대해 더욱 더 고민해 보는 시간이었다.

---
### 💰 코드
```
import java.util.*;

class Solution {
    
    static class Point{
        int number;
        int cnt;
        
        Point(int number, int cnt){
            this.number = number;
            this.cnt = cnt;
        }
    }
    
    static Queue<Point> que;
    static ArrayList<Integer>[] list;
    static boolean visit[];
    static int arr[];
    
    public int solution(int n, int[][] edge) {
        
        int answer = 1;
        
        visit = new boolean[n+1];
        
        arr = new int [n+1];
        
        list = new ArrayList[n+1];
        
        for(int i=0;i<=n;i++){
            list[i] = new ArrayList();
        }
        
        for(int i=0;i<edge.length;i++){
            list[edge[i][0]].add(edge[i][1]);
            list[edge[i][1]].add(edge[i][0]);
        }
        visit[1] = true;
        
        que = new LinkedList<>();
        
        que.offer(new Point(1,1));
        
        bfs();
        
        Arrays.sort(arr);
        
        // System.out.println("1 : " + arr[6]);
        
        for(int i=0;i<arr.length;i++){
            // System.out.println("2 : " + arr[i]);
        }
        
        for(int i=arr.length-2;i>0;i--){
            if(arr[arr.length-1] == arr[i]){
                answer++;
            }
        }
        
        return answer;
    }
    
    public static void bfs(){
        
        while(!que.isEmpty()){
            Point po = que.poll();
            // System.out.println("poll은 ? : " + po.number + " " + po.cnt);
            for(int i=0;i<list[po.number].size();i++){
                // System.out.println("4 : " + list[po.number].size());
                // System.out.println("5 : " + list[po.number].get(i));
                
                if(visit[list[po.number].get(i)])continue;
                visit[list[po.number].get(i)] = true;
                if(arr[list[po.number].get(i)] > 0){
                    // System.out.println("6 : ");
                    arr[list[po.number].get(i)] = Math.min(arr[list[po.number].get(i)], po.cnt);
                }
                else{
                  arr[list[po.number].get(i)] = po.cnt;  
                }
                
                que.offer(new Point(list[po.number].get(i), po.cnt+1));
            }
        }
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/e770341a-211f-4197-88f3-18cca821a57b)

