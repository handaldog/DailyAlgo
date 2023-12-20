# 2️⃣6️⃣ [백준] DNA 비밀번 </span> 

---
### 📃 문제 설명
평소에 문자열을 가지고 노는 것을 좋아하는 민호는 DNA 문자열을 알게 되었다. DNA 문자열은 모든 문자열에 등장하는 문자가 {‘A’, ‘C’, ‘G’, ‘T’} 인 문자열을 말한다. 
예를 들어 “ACKA”는 DNA 문자열이 아니지만 “ACCA”는 DNA 문자열이다. 
이런 신비한 문자열에 완전히 매료된 민호는 임의의 DNA 문자열을 만들고 만들어진 DNA 문자열의 부분문자열을 비밀번호로 사용하기로 마음먹었다.

하지만 민호는 이러한 방법에는 큰 문제가 있다는 것을 발견했다. 
임의의 DNA 문자열의 부분문자열을 뽑았을 때 “AAAA”와 같이 보안에 취약한 비밀번호가 만들어 질 수 있기 때문이다. 
그래서 민호는 부분문자열에서 등장하는 문자의 개수가 특정 개수 이상이여야 비밀번호로 사용할 수 있다는 규칙을 만들었다.

임의의 DNA문자열이 “AAACCTGCCAA” 이고 민호가 뽑을 부분문자열의 길이를 4라고 하자. 
그리고 부분문자열에 ‘A’ 는 1개 이상, ‘C’는 1개 이상, ‘G’는 1개 이상, ‘T’는 0개 이상이 등장해야 비밀번호로 사용할 수 있다고 하자.
이때 “ACCT” 는 ‘G’ 가 1 개 이상 등장해야 한다는 조건을 만족하지 못해 비밀번호로 사용하지 못한다. 
하지만 “GCCA” 은 모든 조건을 만족하기 때문에 비밀번호로 사용할 수 있다.

민호가 만든 임의의 DNA 문자열과 비밀번호로 사용할 부분분자열의 길이, 
그리고 {‘A’, ‘C’, ‘G’, ‘T’} 가 각각 몇번 이상 등장해야 비밀번호로 사용할 수 있는지 순서대로 주어졌을 때 
민호가 만들 수 있는 비밀번호의 종류의 수를 구하는 프로그램을 작성하자. 
단 부분문자열이 등장하는 위치가 다르다면 부분문자열이 같다고 하더라도 다른 문자열로 취급한다.

---
### 🔑 출력 형식
![image](https://github.com/handaldog/DailyAlgo/assets/96431408/66beff02-dcfe-4cc4-84ab-556f022cec05)


---
### ❗️ 풀이 
1. 받은 String 을 따로 arr이라는 배열에 넣고 슬라이딩 윈도우를 시행하면서 빼고 더해나갔다.
2. HashMap 의 containsKey 를 이용하여 갯수를 세면서 그 갯수가 맞지않으면 false 처리를 했다.


--- 
### 👨‍💻 배운 점
1. HashMap 은 contains 가 아니라 containsKey 와 containsValue가 존재함.
2. 맵의 특성을 잘 살린 풀이였다.
3. 맵의 모두 출력을 할 때 이용하는 iterator 을 잘 이해해야겠다.
4. 슬라이딩 윈도우를 이용한 두번째 문제이다. 꽤 재밌었다.


---
### 💰 코드
[첫번째 코드] - 슬라이딩 윈도우 사용 X
```
package 문자열;

import java.util.*;

public class DNA비밀번호 {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int s = sc.nextInt();
		int p = sc.nextInt();
		
		int answer = 0;
		
		String str = sc.next();
		
		int a = sc.nextInt();
		int c = sc.nextInt();
		int g = sc.nextInt();
		int t = sc.nextInt();
		
		for(int i=0;i<=s-p;i++) {
			String part = str.substring(i,i+p);
				
			// A
			if(!check("A", part, a))continue;
			// C
			if(!check("C", part, c))continue;
			// G
			if(!check("G", part, g))continue;
			// T
			if(!check("T", part, t))continue;
			
			answer++;
		}
		
		System.out.println(answer);
			
	}
	public static boolean check(String word, String pstr, int diff) {
		
		int origin = pstr.length();
		
		pstr = pstr.replace(word, "");
		
		int change = pstr.length();
		
		if(origin - change >= diff) {
			return true;
		}
		return false;
		
		
	}

}


```
[두번째 코드] 슬라이딩 윈도우 O
```
package 문자열;

import java.util.*;

public class DNA비밀번호 {
	
	static HashMap<Character, Integer> map = new HashMap<>();

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int s = sc.nextInt();
		int p = sc.nextInt();
		
		int answer = 0;
		
		String str = sc.next();
		
				
		char arr[] = new char [str.length()];
		
		for(int i=0;i<str.length();i++) {
			arr[i] = str.charAt(i);
		}
		
		boolean flag = false;
			
		int a = sc.nextInt();
		int c = sc.nextInt();
		int g = sc.nextInt();
		int t = sc.nextInt();
		
				
		for(int i=0;i<s;i++) {
			
			if(i == p-1) flag =true;
			
			if(i >= p) {
				
				// map 에서 contains는 두가지로 나뉨. (containsKey, containsValue)
				if(map.containsKey(arr[i-p])) {
					int cnt = map.get(arr[i-p]);
					map.put(arr[i-p], cnt-1);
				}
				
			}
			if(map.containsKey(arr[i])) {
				int cnt = map.get(arr[i]);
				map.put(arr[i], cnt+1);
			}
			else {
				map.put(arr[i], 1);
			}
			
			if(flag && check('A', a) && check('C',c) && 
					check('G', g) && check('T', t)) {
				answer++;
			}
			
		}
		
		
		System.out.println(answer);
			
	}
public static boolean check(char word, int diff) {
	
		
		if(map.containsKey(word)) {
			
			if(map.get(word)>= diff) {
			
				return true;
			}
			else {
				 return false;
			}
		}
		else {
			if(diff == 0) return true;
			else return false;
		}
		
		
	}
	

}

```

![image](https://github.com/handaldog/DailyAlgo/assets/96431408/7f27b433-4326-4702-9683-c10e9c79622c)

