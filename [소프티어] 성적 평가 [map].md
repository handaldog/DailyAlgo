# 2️⃣2️⃣ [소프티어] 성적 평가 </span> 

---
### 📃 문제 설명
현주는 N명의 인원이 참여하는 프로그래밍 스터디 그룹을 이끌고 있다.


현주는 스터디를 위해 대회를 세 개 개최하였고, 모든 구성원이 각 대회에 참여하였다. 참가자는 각 대회에서 0 이상 1,000 이하의 정수인 점수를 얻는다. 한 대회에서 둘 이상의 참가자가 동점이 나오는 경우도 있을 수 있다.


현주는 각 대회별 등수 및 최종 등수를 매기고 싶다. 등수는 가장 점수가 높은 사람부터 1등, 2등, ···, N등의 순서대로 붙는다. 만일 동점이 있을 경우 가능한 높은 (등수의 수가 작은) 등수를 부여한다.
즉, 점수가 내림차순으로 10,7,6,6,4의 순서일 경우, 6점을 받은 두 사람은 공동 3등이 되고, 그 다음 순서인 4점을 받은 사람은 5등이 된다. 이 규칙을 다르게 표현하면 다음과 같다: 
각 사람마다 “나보다 점수가 큰 사람”의 수를 세어 1을 더한 것이 자신의 등수가 된다. 대회별 등수는 각 대회에서 얻은 점수를 기준으로 하며 최종 등수는 세 대회의 점수의 합을 기준으로 한다.


각 참가자의 대회별 등수 및 최종 등수를 출력하는 프로그램을 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/ec9c8a2b-5712-4db5-b0e1-f8ad6cf4c133)


---
### ❗️ 풀이 
1. 받은 배열을 그대로 두고 copy 할 것들을 하나씩 만들어준다.
2. calc라는 함수를 따로 만들어서
3. 정렬하고 순위정하고 점수와 순위를 map에 넣고 map을 그대로 둔 배열을 가져와서 돌리면서 key값으로 출력했다.


--- 
### 👨‍💻 배운 점
1. map.containsKey
2. 웃긴건 같은 코드로 제출하면 틀릴때도 있고 맞을때도 있다. 0.0001초 차이로 엇갈리는 듯 웃겼다.
3. 다음에 더 확실한 코드를 가져오겠다.

---
### 💰 코드
```
import java.io.*;
import java.util.*;

public class Main {
    static int n;

    public static void main(String[] args) {

      Scanner sc = new Scanner(System.in);

      n = sc.nextInt();
      int last[] = new int [n];
      int lastcopy[] = new int [n];
      for(int i=0;i<3;i++){
        int people[] = new int [n];
        
        int score[] = new int [n];
        
        for(int j=0;j<n;j++){
          people[j] = sc.nextInt();
          score[j] = people[j];
          last[j] += people[j];
          lastcopy[j] += people[j];
        }
        calc(score, people);
    }
      calc(last, lastcopy);

     } 

  public static void calc(int score[], int people[]){
    
        int grade[] = new int [n];
    
        Arrays.sort(score);

        grade[score.length-1] = 1;
        
        for(int k=score.length-2;k>=0;k--){
          if(score[k+1] == score[k]){
            grade[k] = grade[k+1];
          }
          else{
            grade[k] = score.length-k; 
          }       
      }
      HashMap<Integer, Integer> map = new HashMap<>();

      for(int k=0;k<score.length;k++){
        map.put(score[k], grade[k]);
      }

        for(int k=0;k<people.length;k++){
          if(k == people.length-1){
            System.out.print(map.get(people[people.length-1]));
          }
          else{
            System.out.print(map.get(people[k]) + " ");
          }
        }
        System.out.println();
    
  }
}


```
