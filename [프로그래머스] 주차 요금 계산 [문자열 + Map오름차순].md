# 7️⃣1️⃣ [프로그래머스] 주차 요금 계산 </span> 

---
### 📃 문제 설명
- 문제가 너무 길어서 링크 붙임.
https://school.programmers.co.kr/learn/courses/30/lessons/92341

---
### 🔑 출력 형식


---
### ❗️ 풀이 
1. 먼저 차에 대한 map과 계산될 요금에 대한 맵을 따로 둔다.
2. 기록을 돌면서 "IN"이면 carmap에 들어가고 "OUT"이면 그 해당되는 번호의 in시간을 찾아서 계산해서 fee맵에 넣어준다.
3. 입차만하고 출차기록은 없는 차량이 있을 수도 있기 때문에 carmap.size() > 0 보다 크면 마지막 출차시간 1439 기준으로 계산해서 feemap에 넣어준다.
4. 그리고 feemap에 자동차 번호에 다른 오름차순으로 정렬한 후에 뽑으면서 요금 계산을 하여 답을 도출해 낸다.


--- 
### 👨‍💻 배운 점
1. 나누기를 하면 무조건 정수로 나온다. 그렇기 때문에 소수점을 가진 나누기를 하고 싶다면 둘중 하나는 double로 놔야 한다는 점.
2. ceil - 올림, round - 반올림, floor - 내림

---
### 💰 코드
```
import java.util.*;

class Solution {
    public int[] solution(int[] fees, String[] records) {
        
        
        Map<String, Integer> carmap = new HashMap<>();
        
        Map<String, Integer> feemap = new HashMap<>();
        
        for(int i=0;i<records.length;i++){
            if(records[i].substring(11).equals("IN")){
               carmap.put(records[i].substring(6,10), (Integer.parseInt(records[i].substring(0,2))*60) + Integer.parseInt(records[i].substring(3,5))); 
            }
            else{
                int intime = carmap.get(records[i].substring(6,10));
                
                // 계산
                int outtime = Integer.parseInt(records[i].substring(0,2))*60 
                    + Integer.parseInt(records[i].substring(3,5));
                
                feemap.put(records[i].substring(6,10), feemap.getOrDefault(records[i].substring(6,10), 0) + outtime - intime);
                
                carmap.remove(records[i].substring(6,10));
                
            }
            
        }
        
        // carmap 에 남아있는 애들 계산
        
        
        if(carmap.size() > 0){
            
            for(String number : carmap.keySet()){
                
            int intime = carmap.get(number);
            int outtime = 1439;
                
            feemap.put(number, 
                       feemap.getOrDefault(number, 0) + outtime - intime);
            } 
            
        }
        
//             for(String number : feemap.keySet()){
                
//             System.out.println("1 : " + feemap.get(number));
//             } 
            
        
        
        List<String> keySet = new ArrayList<>(feemap.keySet());
        
        keySet.sort((o1,o2) -> o1.compareTo(o2));
        
        int result[] = new int [feemap.size()];
        int cnt = 0;
        for(String number : keySet){
            int answer = 0;
            int total = feemap.get(number);
            // System.out.println("2 : " + total);
            if(total > fees[0]){
                
                answer += fees[1];
                // System.out.println("3 : " + answer);
                total -= fees[0];
                // System.out.println("4 : " + total);
                answer += (int)(Math.ceil((total/(double)fees[2])))*fees[3];
                // System.out.println("올린 : " + (Math.ceil(total/fees[2])));
                // System.out.println("5 : " + answer);
            }
            else{
                answer = fees[1];
            }
            
            result[cnt] = answer;
            cnt++;
        }
        return result;
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/eb3de466-0efa-4cee-a8c5-650e23b6598b)

