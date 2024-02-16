# 7️⃣0️⃣ [코드 트리] 바이러스 검사 </span> 

---
### 📃 문제 설명
바이러스의 확산을 막기 위해 총 n개의 식당에 있는 고객들의 체온을 측정하고자 합니다. 
체온을 측정하는 검사자는 검사팀장과 검사팀원으로 나뉘어집니다. 팀장과 팀원이 검사할 수 있는 고객의 수가 다르며, 
한 가게당 팀장은 오직 한 명, 팀원은 여러명 있을 수 있습니다. 하지만 가게당 팀장 한 명은 무조건 필요합니다. 
가게에 검사팀원만 존재하는 경우는 있을 수 없습니다. 팀장이든 팀원이든 담당한 가게에 대해서만 검사합니다.

n개의 식당 고객들의 체온을 측정하기 위해 필요한 검사자 수의 최솟값을 구하는 프로그램을 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/3d5dc83a-b1ba-4f66-ae7d-fa371d2c2c88)


---
### ❗️ 풀이 
1. 그냥 말 그대로 구현했다.
2. 하지만 핵심은 일일히 빼주는 것이아닌 남은 사람수/검사팀원으로 정해야한다.


--- 
### 👨‍💻 배운 점
1. 수가 크다 생각하면 long 을 잘 사용하자.

---
### 💰 코드
```
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        
        // Scanner sc = new Scanner(System.in);
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        long answer = 0L;
        
        long custom[] = new long[n];

        StringTokenizer st = new StringTokenizer(br.readLine());

        for(int i=0;i<n;i++){
            custom[i] = Long.parseLong(st.nextToken());
        }

        st = new StringTokenizer(br.readLine());

        int team = Integer.parseInt(st.nextToken());
        int teamone = Integer.parseInt(st.nextToken());

        for(int i=0;i<n;i++){
            if(custom[i] <= team){
                answer++;
            }
            else if(custom[i] > team){
                custom[i] -= team;

                answer += custom[i]/teamone+1;

                if(custom[i]%teamone > 0){
                    answer++;
                }
                
            }
        }

        System.out.println(answer);

    }
}

```
