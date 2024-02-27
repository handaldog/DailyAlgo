# 7️⃣5️⃣ [코드 트리] 조삼 모사 </span> 

---
### 📃 문제 설명
https://www.codetree.ai/training-field/frequent-problems/problems/three-at-dawn-and-four-at-dusk/description

문제 내용이 많아 코드로 대체합니다.

---
### 🔑 출력 형식


---
### ❗️ 풀이 
1. 처음엔 순열로 다 돌려서 브루투포스를 했지만 시간초과가 났다.
2. 그래서 조합으로 n/2개만 true 하고 나머지는 false로 두어
3. true는 true끼리만 계산, false는 false끼리만 계산해서 min을 뽑았다.


--- 
### 👨‍💻 배운 점
1. 조합을 int로 안뽑고 boolean으로 뽑는 것을 배웠다.

---
### 💰 코드
```
import java.util.*;

public class Main {

    // static boolean visit[];
    static int area[][];
    static boolean result[];
    static int n;
    static int min = 1000000;

    public static void main(String[] args) {
        
        Scanner sc = new Scanner(System.in);

        n = sc.nextInt();

        area  = new int [n][n];
        // visit = new boolean[n];
        result = new boolean [n];

        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                area[i][j] = sc.nextInt();
            }
        }
        comb(0,0);

        System.out.println(min);

    }

    public static void comb(int idx, int start){
        if(idx == n/2){
            int cal1 = 0;
            int cal2 = 0;
            for(int i=0;i<n;i++){
                // System.out.print(i + ":" + result[i] + " ");
                for(int j=0;j<n;j++){
                    if(i == j) continue;
                    if(!result[i] && !result[j]){
                        cal1 += area[i][j];
                    }
                    else if(result[i] && result[j]){
                        cal2 += area[i][j];
                    }
                }
                
            }
                min = Math.min(min, Math.abs(cal1 - cal2));
            // System.out.println();
            return;
        }
        for(int i=start;i<n;i++){

            result[i] = true;
            comb(idx+1, i+1);
            result[i] = false;
            
        }

    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/f147c953-53ab-4d83-84ed-ad5d4175a1ce)

