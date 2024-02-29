# 7️⃣9️⃣ [코드 트리] 불안한 무빙워크 </span> 

---
### 📃 문제 설명
문제가 길어 링크로 대체 합니다.

https://www.codetree.ai/training-field/frequent-problems/problems/unstable-moving-walk

---
### 🔑 출력 형식


---
### ❗️ 풀이 
1. work 클래스를 따로 만들어 숫자, 안정성, 사람 수를 나타낸다.
2. 그리고 말 그대로 구현하면 되는데
3. 주의할 점은 안정성 구할때 지속적으로 체크하면서 return 시켰다.


---
### 💰 코드
```
import java.util.*;

public class Main {

    static class work{
        int num;
        int safe;
        int person;

        work(int num, int safe, int person){
            this.num = num;
            this.safe = safe;
            this.person = person;
        }
    }

    static int safecheck;

    public static void main(String[] args) {
       
       Scanner sc = new Scanner(System.in);

       int n = sc.nextInt();

       int k = sc.nextInt();

       LinkedList<work> moving = new LinkedList<>();

       for(int i=0;i<n*2;i++){
        int safe = sc.nextInt();
        if(safe == 0)safecheck++;
        moving.add(new work(i,safe, 0));
       }

        int answer = 0;

        // 이미 안정성 0이 k개 일 때 확인하기
        if(safecheck == k){
            System.out.println(answer);
            return;
        }
        

        while(true){
            
            answer++;

            // 1.
            
            moving.addFirst(moving.get((n*2)-1));
            // System.out.println("야" + moving.get(0).num);
            moving.remove(n*2);

            if(moving.get(n-1).person > 0){
                moving.add(n-1, new work(moving.get(n-1).num, moving.get(n-1).safe, moving.get(n-1).person-1));
                moving.remove(n);
            }

            // 2.
            for(int i=n-2;i>=0;i--){
                if(moving.get(i).person > 0 ){
                    // 옮겨갈 자리에 안정성이 0이거나 person수 0보다 크면 continue
                    if(moving.get(i+1).person == 0 && moving.get(i+1).safe > 0){

                    // 원래자리 person 수 없애고
                    moving.add(i, new work(moving.get(i).num, moving.get(i).safe, moving.get(i).person-1));
                    moving.remove(i+1);

                    // 옮겨간 자리에 person +1, 안정성 -1
                    if(i+1 == n-1){
                        moving.add(i+1, new work(moving.get(i+1).num, moving.get(i+1).safe-1, moving.get(i+1).person));
                        if(moving.get(i+1).safe == 0){
                            safecheck++;
                            if(safecheck >= k){
                                System.out.println(answer);
                                return;
                        }
                    }
                    }
                    else{
                        moving.add(i+1, new work(moving.get(i+1).num, moving.get(i+1).safe-1, moving.get(i+1).person+1));
                        if(moving.get(i+1).safe == 0){
                            safecheck++;
                            if(safecheck >= k){
                                System.out.println(answer);
                                return;
                        }
                        }
                    }

                    moving.remove(i+2);
                    }
                }
            }
            
            // 3.
            if(moving.get(0).person == 0 && moving.get(0).safe > 0){
                // System.out.println("1 :" + "사람 올린다.");
                moving.add(0, new work(moving.get(0).num, moving.get(0).safe-1, moving.get(0).person+1));
                if(moving.get(0).safe == 0){
                            safecheck++;
                            if(safecheck >= k){
                                System.out.println(answer);
                                return;
                        }
                }
                moving.remove(1);
            }

                    }
            
       }
    }


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/2bb352af-c36b-4eb2-ab62-788563ce488d)

