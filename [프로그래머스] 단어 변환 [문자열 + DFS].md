# 3️⃣7️⃣ [프로그래머스] 단어 변환 </span> 

---
### 📃 문제 설명
두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/b4e034be-74bb-4db3-9e75-aaa4476787b9)


---
### ❗️ 풀이 
1. DFS함수와 Compare함수를 만들어 단어가 하나만 다른 것을 확인하면서 DFS에 넣었다.
2. 주의 할 점은 visit이 들어갔다 나오는 것을 잘 판단해서 넣어야한다.


--- 
### 👨‍💻 배운 점

---
### 💰 코드
```
import java.util.*;
class Solution {
    
    static boolean visit[];
    static int length;
    static String tar;
    static int min = 100;
    static String word[];
    
    public int solution(String begin, String target, String[] words) {
        
        visit = new boolean[words.length];
        
        word = words;
        
        length = target.length();
        
        tar = target;
        
        dfs(begin, 0);
        
        int answer = 0;
        
        if(min == 100){
            return answer;
        }
        
        
        return min;
    }
    
    public static boolean compare(String origin, String nextword){
        int check =0;
        for(int i=0;i<length;i++){
            if(origin.charAt(i) != nextword.charAt(i)){
                check++;
            }
        }
        if(check == 1){
            return true;
        }
        
        return false;
    }
    
    public static void dfs(String str, int cnt){
        
        System.out.println("3 : " + str);
            System.out.println("4 : " + tar);
        
        if(str.equals(tar)){
            System.out.println("1 : " + str);
            System.out.println("2 : " + tar);
            min = Math.min(min, cnt);
        }
        
        for(int i=0;i<word.length;i++){
            if(visit[i])continue;
            if(compare(str, word[i])){
                visit[i] = true;
                dfs(word[i], cnt+1);
                visit[i] = false;
            }
            
        }
}
       
        
    }


```
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/5c449a6c-8aa9-45b1-9367-30d1598a94f5)

