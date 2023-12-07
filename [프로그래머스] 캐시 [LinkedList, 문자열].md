# 1️⃣4️⃣ [프로그래머스] 캐시 </span> 

---
### 📃 문제 설명
지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.
이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 
제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.
어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 
제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.
어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/bb813048-b338-4d97-bbf3-e0b2e9b69b0a)

### 💨조건
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/2d693e4e-7d9a-4b09-ab19-c1010925d103)

---
### ❗️ 풀이 
1. 포함된 것, 포함 안 된 것으로 1차로 나누고 3이 넘는 것 안넘는 것으로 2차로 나누어서 계산했다.
2. 포함 안된 부분은 그냥 기본적은 연산으로 가능해서 쉽게 했지만
3. 포함 된 부분에서 빼는 연산이 너무 헷갈려서 엄청 그리면서 풀었던 것 같다.
4. 자세하게 설명해보자면
   - 포함 된 부분에서 3 미만이면 그냥 넣었다.
   - 3이면 해당 단어 삭제하고 넣었다.
   - 내가 헷갈렸던 것은 LRU 알고리즘때문에 같은 단어 일때 빼고 다시 넣어줘야 하는 지 아니면 같은 단어여도 각 각 다르게 봐야하는 지에 대해 많이 고민했었던 것 같다.


--- 
### 👨‍💻 배운 점
1. LinkedList는 엄청나게 편리한 친구이다.

---
### 💰 코드
[첫번째 코드] - 실패
```
import java.util.*;

class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        
        int a = 'a';
        int A = 'A';
        
        System.out.println("a :" + a);
        System.out.println("A :" + A);
        Queue<String> que = new LinkedList<>();
            
        for(int i=0;i<cities.length;i++){
            if(que.contains(cities[i])){

```

[두번째 코드] - 성공

```
import java.util.*;

class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        
        LinkedList<String> list = new LinkedList<>();
        
        if(cacheSize == 0){
            return cities.length * 5;
        }
        
        for(int i=0; i<cities.length;i++){
            String str = cities[i].toUpperCase();
            
            if(list.contains(str)){
                
                if(list.size() < cacheSize){
                    list.add(str);
                    answer+=1;
                    
                }
                else {
                    // 들어온거 해당되는 단어 삭제 들어온거 넣고, 삭제한 단어 넣기
                    list.remove(str);
                    list.add(str);
                    answer+=1;
                }
            }
            // 포함 안되있으면
            else {
                if(list.size() < cacheSize){
                    // 맨 앞 삭제후 넣기
                    list.add(str);
                    answer+=5;
                }
                else {
                    // 그냥 넣기.
                    list.remove(0);
                    list.add(str);
                    answer+=5;
                    
                }
            }
            
        }
        return answer;
    }
}
```
