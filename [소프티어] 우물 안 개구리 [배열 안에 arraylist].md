# 2️⃣4️⃣ [소프티어] 우물 안 개구리 </span> 

---
### 📃 문제 설명
헬스장에서 N명의 회원이 운동을 하고 있다. 각 회원은 1에서 N사이의 번호가 부여되어 있고, i번 회원이 들 수 있는 역기의 무게는 Wi이다. 
회원들 사이에는 M개의 친분관계 (Aj, Bj)가 있다. (Aj, Bj)는 Aj번 회원과 Bj번 회원이 친분 관계가 있다는 것을 의미한다. 
i번 회원은 자신과 친분 관계가 있는 다른 회원보다 들 수 있는 역기의 무게가 무거우면 자신이 최고라고 생각한다. 단, 누구와도 친분이 없는 멤버는 본인이 최고라고 생각한다.

이 헬스장에서 자신이 최고라고 생각하는 회원은 몇 명인가?

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5a8b7e73-e272-4c9d-b997-38461f9224dd)


---
### ❗️ 풀이 
1. 간단히 배열안에 arraylist를 만들어서 관계들을 집어넣으면 된다.
2. 주의할 점은 1,3 이 관계면 3,1도 관계이므로 중복으로 넣어줘야 한다.


--- 
### 👨‍💻 배운 점
1. 까먹고 있었던 배열 안에 arraylist를 넣는 방법을 다시 상기시켰다.
   - ArrayList<>[] list = new ArrayList[숫자];
   - list[0] = new ArrayList();  -> 이렇게 생성해줘야함.

---
### 💰 코드
```
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) {

      Scanner sc = new Scanner(System.in);

      int answer = 0;

      int n = sc.nextInt();
      int m = sc.nextInt();

      ArrayList<Integer>[] relation = new ArrayList[n+1]; 

      int weight[] = new int[n+1];

      // 무게 배열
      for(int i=1;i<=n;i++){
        weight[i] = sc.nextInt();
      }

      // arraylist 생성
      for(int i=0;i<=n;i++){
        relation[i] = new ArrayList();
      }

      for(int i=0;i<m;i++){
        int a = sc.nextInt();
        int b = sc.nextInt();
        
        relation[a].add(b);
        relation[b].add(a);
      }

      for(int i=1;i<=n;i++){
        boolean flag = true;
        for(int j=0;j< relation[i].size();j++){
          if(weight[i] <= weight[relation[i].get(j)]) {
            flag = false;
            continue;
          }
        }
        if(flag){
          answer++;
        }
      }

      System.out.println(answer);

      
    }
}


```
