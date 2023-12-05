# 1️⃣3️⃣ [프로그래머스] 의상 </span> 

---
### 📃 문제 설명
코니는 매일 다른 옷을 조합하여 입는것을 좋아합니다.

예를 들어 코니가 가진 옷이 아래와 같고, 오늘 코니가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야합니다.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/43c4c3d7-95ec-468b-a62a-b3aba9e10bc0)

코니는 각 종류별로 최대 1가지 의상만 착용할 수 있습니다. 예를 들어 위 예시의 경우 동그란 안경과 검정 선글라스를 동시에 착용할 수는 없습니다.
착용한 의상의 일부가 겹치더라도, 다른 의상이 겹치지 않거나, 혹은 의상을 추가로 더 착용한 경우에는 서로 다른 방법으로 옷을 착용한 것으로 계산합니다.
코니는 하루에 최소 한 개의 의상은 입습니다.
코니가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/4c9d0ebc-d72c-4376-ad51-3e2204c47818)


---
### ❗️ 풀이 
[첫번째 풀이]
1. HashMap에 담아서 키값이 같으면 ++ 되게 한다.
2. HashMap Value 꺼내서 배열에 넣기 (배열의 크기는 size)
3. 배열 크기만큼 조합돌리기 (1,2,3,,,) 이 방식으로
4. 근데 1번 케이스가 자꾸 시간초과가 난다.

[두번째 풀이]
1. 해쉬에 담는 거 까지는 같다.
2. 배열에 안담고 조합도 빼고
3. 공식을 이용해서 구한다. -> 다른 풀이를 보고 배웠다.. 나였으면 못 구했을 공식..ㅠ


--- 
### 👨‍💻 배운 점
1. Hash containsKey, Map.Entry 이용해서 value 값 뽑아내는 방법.
2. 한번 더 공식이 있나 생각해보기.... (문제를 풀때..)

---
### 💰 코드
[첫번째 코드]
```
import java.util.*;

class Solution {
    
    static int result[];
    static int sum, x;
    static int arr[];
    
    public int solution(String[][] clothes) {
        int answer = 0;
        
        
        HashMap<String, Integer> map = new HashMap<>();
        
        for(int i=0;i<clothes.length;i++){
            if(map.containsKey(clothes[i][1])){
                int cnt = map.get(clothes[i][1]);
                map.put(clothes[i][1], cnt+1);
            }
            else{
                map.put(clothes[i][1], 1);
            }
            
        }
        
        arr = new int [map.size()];
        
        result = new int [arr.length];
        
        int cnt = 0;
        x=1;
        for(Map.Entry<String, Integer> entrySet : map.entrySet()){
            x *= (entrySet.getValue()+1);
            
        }
        
        for(int i=1;i<=arr.length;i++){
            comb(0,0,i);
        }
        
        
        
        return x-1;
    }
    public static void comb(int idx, int start, int num){
        if(idx == num){
            x = 1;
            for(int i=0;i<idx;i++){
                x *= arr[result[i]];
            }
            sum += x;
            return;
        }
        
        for(int i=start;i<arr.length;i++){
            result[idx] = i;
            comb(idx+1, i+1, num);
        }
    }
}

```
[두번째 코드]
```
import java.util.*;

class Solution {
    
    static int result[];
    static int sum, x;
    static int arr[];
    
    public int solution(String[][] clothes) {
        int answer = 0;
        
        
        HashMap<String, Integer> map = new HashMap<>();
        
        for(int i=0;i<clothes.length;i++){
            if(map.containsKey(clothes[i][1])){
                int cnt = map.get(clothes[i][1]);
                map.put(clothes[i][1], cnt+1);
            }
            else{
                map.put(clothes[i][1], 1);
            }
            
        }
        
        // arr = new int [map.size()];
        
        // result = new int [arr.length];
        
        // int cnt = 0;
        x=1;
        for(Map.Entry<String, Integer> entrySet : map.entrySet()){
            x *= (entrySet.getValue()+1);
            
        }
        
        // for(int i=1;i<=arr.length;i++){
        //     comb(0,0,i);
        // }
        
        
        
        return x-1;
    }
    public static void comb(int idx, int start, int num){
        if(idx == num){
            x = 1;
            for(int i=0;i<idx;i++){
                x *= arr[result[i]];
            }
            sum += x;
            return;
        }
        
        for(int i=start;i<arr.length;i++){
            result[idx] = i;
            comb(idx+1, i+1, num);
        }
    }
}
```
