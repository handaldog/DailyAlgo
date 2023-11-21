# 4️⃣ [백준] 1로 만들기 </span> 

---
### 📃 문제 설명

정수 X에 사용할 수 있는 연산은 다음과 같이 세 가지 이다.

1. X가 3으로 나누어 떨어지면, 3으로 나눈다.
2. X가 2로 나누어 떨어지면, 2로 나눈다.
3. 1을 뺀다.

정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.

---
### 🔑 출력 형식

첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

---
### ❗️ 풀이 

숫자가 주어지면 4부터 주어진 숫자까지 arraylist에 저장해 놓는다.
이런 방식으로 해야 한번만 계산하면 과거 수가 최적합으로 저장되어 있기 때문에 그곳에 +1을 하면 답이 된다.

신경써야 했던 부분은 6같이 주어진 수로 다 나뉘어 질 수 있는 수는 if문을 적절히 써서 min을 잘 뽑아 내야 한다.

--- 
### 👨‍💻 배운 점

DP문제를 스스로 생각하고 풀고싶어 나름 생각을 많이 했다.
DP는 감이 필요한거 같다 그렇기 위해서는 많은 문제를 풀어야 할 것 같다.

스스로 손으로 풀면서 규칙이나 유사한 것들을 예리하게 찾아내야한다. 누적합, 과거수,, 등등을 생각해야 한다.


---
### 💰 코드
```
package dailyalgo;

import java.util.*;

public class 일로만들기 {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);


        ArrayList<Integer> list = new ArrayList();

        list.add(0,0);
        list.add(1,0);
        list.add(2,1);
        list.add(3,1);

        int num = sc.nextInt();

        for(int i=4;i<=num;i++){
            int min = Integer.MAX_VALUE;

            if(i%2 == 0 ){
                min = Math.min(list.get(i/2), min);
            }
            if(i%3 == 0){
                min = Math.min(list.get(i/3), min);

            }
            if(i-1 > 0){
                min = Math.min(list.get(i-1), min);

            }

            list.add(i, min+1);
//            System.out.println(min+1);
        }

        System.out.println(list.get(num));

    }
}


```
