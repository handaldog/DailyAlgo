# 4️⃣6️⃣ [프로그래머스] 불량 사용자 </span> 

---
### 📃 문제 설명
개발팀 내에서 이벤트 개발을 담당하고 있는 "무지"는 최근 진행된 카카오이모티콘 이벤트에 비정상적인 방법으로 당첨을 시도한 응모자들을 발견하였습니다. 
이런 응모자들을 따로 모아 불량 사용자라는 이름으로 목록을 만들어서 당첨 처리 시 제외하도록 이벤트 당첨자 담당자인 "프로도" 에게 전달하려고 합니다. 
이 때 개인정보 보호을 위해 사용자 아이디 중 일부 문자를 '*' 문자로 가려서 전달했습니다. 가리고자 하는 문자 하나에 '*' 문자 하나를 사용하였고 아이디 당 최소 하나 이상의 '*' 문자를 사용하였습니다.
"무지"와 "프로도"는 불량 사용자 목록에 매핑된 응모자 아이디를 제재 아이디 라고 부르기로 하였습니다.

예를 들어, 이벤트에 응모한 전체 사용자 아이디 목록이 다음과 같다면

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/1a6696a4-06f8-4aa9-b856-2d86932e039a)

다음과 같이 불량 사용자 아이디 목록이 전달된 경우,
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/103c70e7-6fb7-4109-b2e3-e27ae5f0d062)

불량 사용자에 매핑되어 당첨에서 제외되어야 야 할 제재 아이디 목록은 다음과 같이 두 가지 경우가 있을 수 있습니다.

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/628eddf1-94ca-443e-9e9a-b84ee0a67b1f)

이벤트 응모자 아이디 목록이 담긴 배열 user_id와 불량 사용자 아이디 목록이 담긴 배열 banned_id가 매개변수로 주어질 때, 
당첨에서 제외되어야 할 제재 아이디 목록은 몇가지 경우의 수가 가능한 지 return 하도록 solution 함수를 완성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/082f6a15-c220-40f7-850c-a4c730918750)


---
### ❗️ 풀이 
1. 다양한 생각을 하다 결국 찾지 못해 해설을 참고했다.
2. 하지만 참고만 하고 나만의 방식으로 풀긴 했다.

3. 우선, 최대 가지수가 적기 때문에 완탐을해도 시간초과가 나지 않는다.
4. 순열로 모든 가지수를 구한 후, 조건에 맞는 것인지 확인했다.
5. 조건에 맞으면 똑같은 종류를 걸러내기 위해 sort를 했다.
6. 그리고 중복이 안되는 set에 넣고
7. 다 돌면 set.size만 구했다.


--- 
### 👨‍💻 배운 점
1. 우선, 디버깅하는데 무척 어려웠다. -> sort를 한 배열가지고 계속 순열을 만들고 있었기 때문이다...ㅠㅠㅠㅠㅠㅠ(대략 2시간 쓴듯..)
2. arr = word 하면 -> arr이 변경 되면 같이 변경된다. 그러니깐 for문을 돌면서 따로 만들어줘야 따로 변경된다.

---
### 💰 코드
```
import java.util.*;
class Solution {
    
    static String[] users;
    static String[] bans;
   
    static boolean visit[];
    static String word[];
    static HashSet<String> set = new HashSet<>();
    
    public int solution(String[] user_id, String[] banned_id) {
       
        
        users = user_id;
        bans = banned_id;
        
        visit = new boolean [users.length];
        word = new String [bans.length];
        check(0);
        
        
        return set.size();
    }
    
    public static void check(int idx){
        if(idx == bans.length){
            
            int cnt = 0;
            for(int i=0;i<idx;i++){
                // System.out.print(word[i] + " ");
                if(please(bans[i], word[i]) == true){
                   
                   cnt++;
                }
            }
            
            
            System.out.println();
            if(cnt == idx){
                
            String arr[] = new String [idx];
                
            for(int i=0;i<idx;i++){
                arr[i] = word[i];
            }
                
            Arrays.sort(arr);
                
            String str = "";
            for(int i=0;i<idx;i++){
                
                str+= arr[i];
            }
            
            set.add(str);
            }
            return;
            
        }
        for(int i=0;i<users.length;i++){
            if(visit[i])continue;
            visit[i] = true;
            word[idx] = users[i];
            check(idx+1);
            visit[i] = false;
        }
        
    }
    
    public static boolean please(String ban, String user){
        
        if(ban.length() != user.length()){
            return false;
        }
        int c = 0;
        for(int i=0;i<ban.length();i++){
            
            if(ban.charAt(i) == '*' || (ban.charAt(i) == user.charAt(i))){
                c++;
            }
        }
        if(c == ban.length()){
            return true;
        }
        
        return false;
    }
}

```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/75665a97-552f-42b8-833f-a7d3f0159a1b)

