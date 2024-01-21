# 5️⃣9️⃣ [프로그래머] 햄버거 만들기 </span> 

---
### 📃 문제 설명
햄버거 가게에서 일을 하는 상수는 햄버거를 포장하는 일을 합니다. 함께 일을 하는 다른 직원들이 햄버거에 들어갈 재료를 조리해 주면 조리된 순서대로 상수의 앞에 아래서부터 위로 쌓이게 되고, 
상수는 순서에 맞게 쌓여서 완성된 햄버거를 따로 옮겨 포장을 하게 됩니다. 상수가 일하는 가게는 정해진 순서(아래서부터, 빵 – 야채 – 고기 - 빵)로 쌓인 햄버거만 포장을 합니다. 
상수는 손이 굉장히 빠르기 때문에 상수가 포장하는 동안 속 재료가 추가적으로 들어오는 일은 없으며, 재료의 높이는 무시하여 재료가 높이 쌓여서 일이 힘들어지는 경우는 없습니다.

예를 들어, 상수의 앞에 쌓이는 재료의 순서가 [야채, 빵, 빵, 야채, 고기, 빵, 야채, 고기, 빵]일 때, 상수는 여섯 번째 재료가 쌓였을 때, 
세 번째 재료부터 여섯 번째 재료를 이용하여 햄버거를 포장하고, 아홉 번째 재료가 쌓였을 때, 
두 번째 재료와 일곱 번째 재료부터 아홉 번째 재료를 이용하여 햄버거를 포장합니다. 즉, 2개의 햄버거를 포장하게 됩니다.

상수에게 전해지는 재료의 정보를 나타내는 정수 배열 ingredient가 주어졌을 때, 상수가 포장하는 햄버거의 개수를 return 하도록 solution 함수를 완성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/63d61267-2ccd-44a2-ae88-b9aeb3083391)


---
### ❗️ 풀이 
1. 처음엔 linkedlist 만들어서 1-2-3-4 가 되면 삭제하는 방식으로 할려 했는데
2. linkedlist의 특징이 삭제하면 앞에꺼 들이 그 자리로 가는 특성이 있어서 너무 헷갈렸다.
3. 그래서 ArrayList로 다시 바꿔서 했더니 시간초과도 안났다.
4. 그것보단 이 문제는 아이디어 싸움인 것 같았다.


--- 
### 👨‍💻 배운 점


---
### 💰 코드
```
import java.util.*;

class Solution {
    public int solution(int[] ingredient) {
        int answer = 0;
        
        ArrayList<Integer> list = new ArrayList<>();
        
        for(int i=0;i<ingredient.length;i++){
            list.add(ingredient[i]);
            
            if(list.size() >=4){
                
                if(list.get(list.size()-1) == 1 && list.get(list.size()-2) == 3 && 
                   list.get(list.size()-3) == 2 && list.get(list.size()-4) == 1){
                    
                    for(int j=0;j<4;j++){
                      list.remove(list.size()-1);   
                    }
                    answer++;
                }
                
            }
           
        }
        return answer;
    }
}

```
