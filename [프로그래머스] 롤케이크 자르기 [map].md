# 7️⃣8️⃣ [프로그래머스] 롤케이크 </span> 

---
### 📃 문제 설명
철수는 롤케이크를 두 조각으로 잘라서 동생과 한 조각씩 나눠 먹으려고 합니다. 
이 롤케이크에는 여러가지 토핑들이 일렬로 올려져 있습니다. 철수와 동생은 롤케이크를 공평하게 나눠먹으려 하는데,
그들은 롤케이크의 크기보다 롤케이크 위에 올려진 토핑들의 종류에 더 관심이 많습니다. 
그래서 잘린 조각들의 크기와 올려진 토핑의 개수에 상관없이 각 조각에 동일한 가짓수의 토핑이 올라가면 공평하게 롤케이크가 나누어진 것으로 생각합니다.

예를 들어, 롤케이크에 4가지 종류의 토핑이 올려져 있다고 합시다. 
토핑들을 1, 2, 3, 4와 같이 번호로 표시했을 때, 케이크 위에 토핑들이 [1, 2, 1, 3, 1, 4, 1, 2] 순서로 올려져 있습니다. 
만약 세 번째 토핑(1)과 네 번째 토핑(3) 사이를 자르면 롤케이크의 토핑은 [1, 2, 1], [3, 1, 4, 1, 2]로 나뉘게 됩니다. 
철수가 [1, 2, 1]이 놓인 조각을, 동생이 [3, 1, 4, 1, 2]가 놓인 조각을 먹게 되면 철수는 두 가지 토핑(1, 2)을 맛볼 수 있지만, 
동생은 네 가지 토핑(1, 2, 3, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것이 아닙니다. 
만약 롤케이크의 네 번째 토핑(3)과 다섯 번째 토핑(1) 사이를 자르면 [1, 2, 1, 3], [1, 4, 1, 2]로 나뉘게 됩니다. 
이 경우 철수는 세 가지 토핑(1, 2, 3)을, 동생도 세 가지 토핑(1, 2, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것입니다. 
공평하게 롤케이크를 자르는 방법은 여러가지 일 수 있습니다. 위의 롤케이크를 [1, 2, 1, 3, 1], [4, 1, 2]으로 잘라도 공평하게 나뉩니다. 
어떤 경우에는 롤케이크를 공평하게 나누지 못할 수도 있습니다.

롤케이크에 올려진 토핑들의 번호를 저장한 정수 배열 topping이 매개변수로 주어질 때, 
롤케이크를 공평하게 자르는 방법의 수를 return 하도록 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/4f956758-764d-44c2-83d4-c2184ec61087)


---
### ❗️ 풀이 
1. 철수와 동생맵을 따로 만든다.
2. 처음 시작하기 전에 철수map에 topping[0] 을 넣고 나머지 토핑들은 동생map에 넣어준다.
3. 그리고 1부터 topping.length -1까지 돈다.
4. 해당 토핑을 철수map에는 넣고, 동생 맵에는 뻰다.
5. 그리고 사이즈가 같은지 체크한다. 같으면 answer++ 


---
### 💰 코드
```
import java.util.*;

class Solution {
    public int solution(int[] topping) {
        int answer = 0;
        
        HashMap<Integer, Integer> chulsu = new HashMap<>();
        
        HashMap<Integer, Integer> dongsang = new HashMap<>();
        
        chulsu.put(topping[0], 1);
        
        for(int i=1;i<topping.length;i++){
            dongsang.put(topping[i], dongsang.getOrDefault(topping[i], 0) +1);
        }
        
        if(chulsu.size() == dongsang.size()){
            answer++;
        }
        
        for(int i=1;i<topping.length-1;i++){
            chulsu.put(topping[i], chulsu.getOrDefault(topping[i], 0) +1);
            
            if(dongsang.get(topping[i]) == 1){
                dongsang.remove(topping[i]);
            }
            else{
                dongsang.put(topping[i], dongsang.getOrDefault(topping[i], 0) -1);
            }
            
            if(chulsu.size() == dongsang.size()){
            answer++;
        }
        }
        return answer;
    }
}
```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/7ab179ab-c096-4184-9b10-d05d0a1a1d76)

