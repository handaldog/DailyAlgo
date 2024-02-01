# 6️⃣7️⃣ [소프티어] 함께하는 효도 </span> 

---
### 📃 문제 설명
남우는 m명의 친구를 불러 나무에서 열매를 수확하는 일을 맡겼습니다. 나무들은 n * n 크기의 격자 모양의 땅 위의 모든 칸에 심어져 있고, 
각 나무마다 가능한 열매 수확량이 주어져 있습니다.

친구들은 n * n 크기의 격자 내의 서로 다른 위치에서 출발하여 1초에 1칸씩 상하좌우 인접한 칸 중 한 곳으로 움직일 수 있으며, 
최종적으로 모든 열매 수확량의 합을 최대로 만들고자 합니다. 이때 각 칸에서 열매를 수확하는데 걸리는 시간은 0초이며, 
한 나무에 여러 친구가 방문하게 되더라도 열매는 딱 한 번만 수확이 가능합니다. 또, 친구들끼리 이동하는 도중 만나게 되는 것 역시 가능합니다.

m명의 친구들이 3초 동안 최대로 얻을 수 있는 열매 수확량의 총 합을 구하는 프로그램을 작성해보세요.

본 문제의 저작권은 (주)브랜치앤바운드에 있으며, 저작자의 동의 없이 무단 전재/복제/배포를 금지합니다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5f1e2fb5-68a4-4f4e-a306-9fc5312c1d1d)


---
### ❗️ 풀이 
1. DFS를 돌면서 완전탐색을 하는 것이 방법이다.
2. 그대신, 주의할 점은 하나의 점이 4개를 다 채우면 그다음거를 돌수 있게 재귀를 2개나 설정해 놓아야 한다.



--- 
### 👨‍💻 배운 점
1. 디버깅이 너무 어려워서 포기할까도 했지만 그냥 했다.
2. just do it!

---
### 💰 코드
```
import java.io.*;
import java.util.*;

public class Main {

    static class person{
        int x;
        int y;

        person(int x, int y){
            this.x=x;
            this.y=y;
        }
    }

    static int area[][];
    static int di[] = {0,1,0,-1};
    static int dj[] = {1,0,-1,0};
    static int n, m;
    static boolean visit[][];
    static int max = 0;
    static person per[];
    
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

         n = sc.nextInt();
         m = sc.nextInt();

         area = new int [n][n];
         visit = new boolean[n][n];

        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                area[i][j] = sc.nextInt();
            }
        }
         per = new person[m];

        int sum = 0;
        
        for(int i=0;i<m;i++){
            int xx = sc.nextInt()-1;
            int yy = sc.nextInt()-1;

            // System.out.println(xx);

            visit[xx][yy] = true;
            // System.out.println(area[xx][yy]);
            sum += area[xx][yy];
            per[i] = new person(xx,yy);
        }
         // System.out.println(sum);

        dfs(per[0].x, per[0].y, sum, 1);

        System.out.println(max);
    }
    public static void dfs(int x, int y, int sum, int depth){

//         for(int i=0;i<n;i++){
//             for(int j=0;j<n;j++){
//                 System.out.print(visit[i][j] + " ");
//             }
//             System.out.println();
//         }
//
//         System.out.println("--------------");
        
        if(depth == (4*m)){
             // System.out.println("최종 : " + sum);
            max = Math.max(max, sum);
            return;
        }
        
        if(depth%4 == 0){
            dfs(per[depth/4].x, per[depth/4].y, sum, depth+1);
            return;
        }
        
        for(int k=0;k<4;k++){
            int nexti = di[k] + x;
            int nextj = dj[k] + y;

            if(nexti >=0 && nextj >= 0 && nexti < n && nextj < n && !visit[nexti][nextj]){
                visit[nexti][nextj] = true;
                dfs(nexti, nextj, sum+area[nexti][nextj], depth+1);
                visit[nexti][nextj] = false;
            }
        }
    }
}

/*
 * 
 * 
 * 4 2
20 26 185 80
100 20 25 80
20 20 88 99
15 32 44 50
1 2
2 3
 * 
 * 
 * */

```
