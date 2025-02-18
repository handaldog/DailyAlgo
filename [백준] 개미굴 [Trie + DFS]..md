# 0️⃣ [백준] 개미 </span> 

---
### 📃 문제 설명
개미는(뚠뚠) 오늘도(뚠뚠) 열심히(뚠뚠) 일을 하네.

개미는 아무말도 하지 않지만 땀을 뻘뻘 흘리면서 매일 매일을 살길 위해서 열심히 일을 하네.

한 치 앞도(뚠뚠) 모르는(뚠뚠) 험한 이 세상(뚠뚠) 그렇지만(뚠뚠) 오늘도 행복한 개미들!

우리의 천재 공학자 윤수는 이 개미들이 왜 행복한지 궁금해졌다.

행복의 비결이 개미가 사는 개미굴에 있다고 생각한 윤수는 개미굴의 구조를 알아보기 위해 로봇 개미를 만들었다.

로봇 개미는 센서가 있어 개미굴의 각 층에 먹이가 있는 방을 따라 내려가다 더 이상 내려갈 수 없으면 그 자리에서 움직이지 않고 신호를 보낸다.

이 신호로 로봇 개미는 개미굴 각 층을 따라 내려오면서 알게 된 각 방에 저장된 먹이 정보를 윤수한테 알려줄 수 있다.

로봇 개미 개발을 완료한 윤수는 개미굴 탐사를 앞두고 로봇 개미를 테스트 해보기 위해 위 그림의 개미굴에 로봇 개미를 투입했다. 로봇 개미의 수는 각 개미굴의 저장소를 모두 확인할 수 있을 만큼 넣는다.

다음은 로봇 개미들이 윤수에게 보내준 정보다.

KIWI BANANA
KIWI APPLE
APPLE APPLE
APPLE BANANA KIWI
공백을 기준으로 왼쪽부터 순서대로 로봇 개미가 각 층마다 지나온 방에 있는 먹이 이름을 뜻한다.

윤수는 로봇 개미들이 보내준 정보를 바탕으로 다음과 같이 개미굴의 구조를 손으로 그려봤다.

APPLE
--APPLE
--BANANA
----KIWI
KIWI
--APPLE
--BANANA

개미굴의 각 층은 "--" 로 구분을 하였다. 또 같은 층에 여러 개의 방이 있을 때에는 사전 순서가 앞서는 먹이 정보가 먼저 나온다.

우리의 천재 공학자 윤수는 복잡한 개미굴들을 일일이 손으로 그리기 힘들어 우리에게 그려달라고 부탁했다.

한치 앞도 모르는 험한 이세상 그렇지만 오늘도 행복한 개미들!

행복의 비결을 알기 위해 윤수를 도와 개미굴이 어떤 구조인지 확인해보자.

---
### 🔑 출력 형식
![image](https://github.com/user-attachments/assets/155d4d7b-ad78-4c59-a0d2-68f26616fc24)


---
### ❗️ 풀이 
1. trie형식으로 만들어 준다음에 DFS로 들어간다.


---

### 👩‍💻 배운 점
트리 형식 문제를 푸는 연습을 하고 있어요.

---
### 💰 코드
```
package Test;

import java.util.*;

public class 백준_개미굴 {
	
	
	static class Node{
		HashMap<String , Node> child;
		
		Node(){
			this.child = new HashMap<>();
		}
	}
	
	static ArrayList<String> print = new ArrayList<>();

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		
		Trie trie = new Trie();
		
		for(int i=0;i<n;i++) {
			
			int cnt = Integer.parseInt(sc.next());
			
			String strs[] = new String[cnt];
			
			for(int j=0;j<cnt;j++) {
				strs[j] = sc.next();
			}
			
			
			trie.insert(strs);
			
		}
		
		trie.setting(trie.root, 0);
		
		for(int i=0;i<print.size();i++) {
			System.out.print(print.get(i));
		}
		
	}
	
	public static class Trie{
		
		Node root = new Node();
		
		
		public void insert(String[] strs) {
			
			Node node = this.root;
			
			
			for(int i=0;i<strs.length;i++) {
				
				node.child.putIfAbsent(strs[i], new Node());
					
				node = node.child.get(strs[i]);
			}
			
			
		}
		public void setting(Node root, int idx) {
			
			//System.out.println("?");
			
			
			ArrayList<String> list = new ArrayList<>(root.child.keySet());
			
			Collections.sort(list);
			
			for(int i=0;i<list.size();i++) {
				for(int j=0;j<idx;j++) {
					print.add("--");
				}
				print.add(list.get(i));
				print.add("\n");
				setting(root.child.get(list.get(i)), idx+1);
			}
		}
		
	}

}

```
