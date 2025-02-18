# 0️⃣ [백준] 게임닉네임 </span> 

---
### 📃 문제 설명
스타트링크에서 매우 재미있는 게임을 만들었다. 이 게임은 정말 재미있다.

게임에는 유저가 접속하는 기능이 있고, 각 유저는 가입할 때, 자신의 닉네임을 정해야 한다. 
닉네임은 알파벳 소문자로만 이루어져 있고, 두 유저가 같은 닉네임을 정하는 것도 가능하다.

이 게임은 유저의 닉네임을 이용해서 내부에 저장할 별칭을 만든다. 
별칭은 유저에게 보여지지는 않고, 내부에서만 사용된다. 저장 공간을 최소로 하기 위해서 별칭의 길이를 최소로 하려고 한다.

별칭은 유저 닉네임의 접두사(Prefix) 중에서 가장 길이가 짧은 것을 사용한다. 
이때, 접두사가 이전에 가입한 닉네임의 접두사가 아니어야 한다. 가능한 별칭이 없는 경우에는 유저가 가입한 시점까지 같은 닉네임으로 가입한 사람의 수 x를 계산해야 한다. 
x가 1인 경우에는 닉네임을 별칭으로 사용하고, x가 2 이상인 경우에는 닉네임의 뒤에 x를 붙여서 별칭으로 사용한다.

예를 들어, 닉네임을 "baekjoon"으로 정한 유저가 가입하면, 이 유저의 별칭은 "b"가 된다. 

그 다음, 닉네임이 "startlink"로 정한 유저가 가입하면, 이 유저의 별칭은 "s"이다. 
"bakejoon"이 닉네임인 유저가 가입하면, 별칭은 "bak"가 되고, "beakjoon"인 유저가 가입하면, 별칭은 "be"가 된다. 
마지막으로 "baekjoon"으로 유저가 가입하면 별칭은 "baekjoon2"가 된다.

유저가 가입한 순서대로 닉네임이 주어졌을 때, 각 유저의 별칭을 구해보자. 위의 규칙을 이용해 별칭을 정하면 두 유저가 같은 별칭을 갖는 것도 가능하다.

---
### 🔑 출력 형식
![image](https://github.com/user-attachments/assets/b1393ce5-b313-420a-b4b8-c84799cb6711)


---
### ❗️ 풀이 
1. Trie 를 이용했고
2. 조건을 다르게 했다.
3. trie에 넣는데 없다면 result에 저장하고 그 이후는 저장 no
4. 있다면 없을때까지 boolean 체크랑 함께 확인하면서 result에 저장
5. 같은 이름은 아예 trie 를 거치지 않고 애초에 map에서 확인해서 출력.


---

### 👩‍💻 배운 점
1. trie 문제를 5문제 푸니 이제 좀 응용이된다.

---
### 💰 코드
```
package Test;

import java.util.*;

public class 백준_게임닉네임 {
	
	static class Node{
		HashMap<String, Node> child;
		boolean endword;
		
		Node(){
			child = new HashMap<>();
			endword = false;
		}
		
	}
	
	static HashMap<String, Integer> map = new HashMap<>();

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		Trie trie = new Trie();
		
		for(int i=0;i<n;i++) {
			String str = sc.next();
			
			// 맵체크부터, 맵에 없으면 넣기 value:1 로
			if(map.containsKey(str)) {
				int cnt = map.get(str)+1;
				System.out.println(str + cnt);
				map.put(str, cnt);
				
				continue;
			}
			else {
				map.put(str, 1);
			}
			// tri에 넣기
			System.out.println(trie.insert(str));
			
			
		}
		
	}
	public static class Trie{
		Node root = new Node();
		
		Trie(){};
		
		public String insert(String name) {
			
			Node node = this.root;
			
			String names[] = name.split("");
			
			String result = "";
			boolean check = false;
			
			for(int i=0;i<name.length();i++) {
				
				
				// 없으면
				if(!node.child.containsKey(names[i])) {
					node.child.put(names[i], new Node());
					
					if(i == 0) {
						result+=names[i];
						check = true;
					}
					else if (i > 0 && !check){
						check = true;
						result += names[i];
					}
					
					node = node.child.get(names[i]);
				}
				// 있으면
				else {
					
					result+=names[i];
					node = node.child.get(names[i]);
				}
			}
			
			return result;
			
			
		}
	}
	

}

```
