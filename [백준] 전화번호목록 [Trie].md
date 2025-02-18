# 0️⃣ [백준] 전화번호목록 </span> 

---
### 📃 문제 설명
전화번호 목록이 주어진다. 이때, 이 목록이 일관성이 있는지 없는지를 구하는 프로그램을 작성하시오.

전화번호 목록이 일관성을 유지하려면, 한 번호가 다른 번호의 접두어인 경우가 없어야 한다.

예를 들어, 전화번호 목록이 아래와 같은 경우를 생각해보자

긴급전화: 911
상근: 97 625 999
선영: 91 12 54 26
이 경우에 선영이에게 전화를 걸 수 있는 방법이 없다. 
전화기를 들고 선영이 번호의 처음 세 자리를 누르는 순간 바로 긴급전화가 걸리기 때문이다. 따라서, 이 목록은 일관성이 없는 목록이다.

---
### 🔑 출력 형식
![image](https://github.com/user-attachments/assets/c66f58eb-1043-4569-90c7-ea83d7b67027)


---
### ❗️ 풀이 
1.먼저 map을 이용해 트라이 형식으로 만들어준다.
2. containskey를 통해서 있으면서 접두사면 break를 걸었다.
3. 포함되어있지 않으면 map에 자식 노드에 추가하게 만들었다.


---

### 👩‍💻 배운 점
트라이를 공부중이에요.

---
### 💰 코드
```
package Test;
import java.util.*;

public class 백준_전화번호목록 {
	
	static class Node{
		HashMap<Character, Node> child;
		
		boolean endnumber;
		
		Node(){
			this.child = new HashMap<>();
			this.endnumber = false;
		}
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		
		int tc = sc.nextInt();
		
		for(int t=0; t<tc;t++) {
			
			boolean check = true;
			
			int n = sc.nextInt();
			
			String words[] = new String [n];
			
			for(int i=0;i<n;i++) {
				words[i] = sc.next();
			}
			
			Arrays.sort(words);
			
			Trie trie = new Trie();
			
			for(int i=0;i<words.length;i++) {
				if(!trie.insert(words[i])) {
					
					check = false;
					//System.out.println("zzzzzz");
					break;
				}
				//System.out.println("two : " + words[i]);
				//System.out.println("check : " + trie.insert(words[i]));
				
			}
			
			if(check) {
				System.out.println("YES");
			}
			else {
				System.out.println("NO");
			}
			
			
			
		}

	}
	
	public static class Trie{
		
		Node root = new Node();
		
		Trie(){
			
		}
		
		public boolean insert(String num) {
			Node node = this.root;
			
			String number = num;
			
			for(int i=0;i<number.length();i++) {
				//System.out.println("number: " + number.charAt(i));
				//&& node.child.get(number.charAt(i)).endnumber
				//node.child.containsKey(number.charAt(i)
				if(node.child.containsKey(number.charAt(i))) {
					if(node.child.get(number.charAt(i)).endnumber) {
						//System.out.println("ggggg");
						//System.out.println("gggg : " + node.endnumber);
						return false;
					}
					else {
						node = node.child.get(number.charAt(i));
					}
				}
				else{
					node.child.put(number.charAt(i), new Node());
					//System.out.println("ㄹㅇㄹㅇ : " +);
					
					node = node.child.get(number.charAt(i));
					if(i==number.length()-1) {
						//System.out.println("test : " + number.charAt(i));
						node.endnumber = true;
						//System.out.println("boolean? : " + node.endnumber);
						}
				}
				
			}
			return true;
			
		}
		
		
	}

}

```
