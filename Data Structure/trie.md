# 트라이(Trie)

## 📌 Trie

- 일반 트리 자료구조 중 하나, Digital Tree, Radix Tree, Prefix Tree라 불림
- 텍스트 자동 완성 기능과 같이 `문자열을 저장하고 탐색`하는데 유용한 자료구조

### 형태

- 각 노드는 <Key, Value> 맵을 가지고 있음.
- Key는 하나의 **알파벳**, Value는 그 **Key에 해당하는 자식 노드**가 됨.

https://camo.githubusercontent.com/eb7454207b7ca1595c87a07834870e8e0fcbc63fa1004d31295bbac4e97594da/68747470733a2f2f776f6f766963746f72792e6769746875622e696f2f696d672f747269655f73616d706c652e706e67

DEV, DEAR, PIE, POP, POW라는 단어가 들어있는 Trie 자료 구조의 도식화

→ 휴대폰 전화번호부에서 검색을 하거나 사전에서 단어를 찾는 것과 같음.

- 예로, DEV라는 문자열을 찾기 이해 루트 노드에서부터 순차적으로 D → E → V 탐색
- 그림에서 볼 수 있듯이 `루트 노드는 특정 문자를 의미하지 않고, 자식 노드만 가지고 있다.`
- 유의할 점은 **'부모 노드'나 '자신이 어떤 알파벳(Key)에 해당하는 노드(Value)'인지를 가지고 있는게 아니라는 점입니다.**
- 즉, 루트 노드는 [D], [P]라고 하는 알파벳을 Key로 하는 자식 노드들을 가지고 있고, [D]는 [E]를 Key로 하는 자식 노드, [P]는 [I]와 [O]를 Key로 하는 자식 노드들을 가지고 있는 것이다.
- 또 루트 노드를 제외한 `노드의 자손들은 해당 노드와 공통 접두어를 가진다는 특징이 있다.` 즉, 'DE' 노드의 자손인 'DEAR'와 'DEV'는 'DE-'를 공통 접두어로 가지며, 'P'의 자손인 'POW'와 'PIE'는 'P-'를 공통 접두어로 가진다.

https://camo.githubusercontent.com/bd66f6e43655b32ebe9a2180a4c17ac75bb93817fb3248106a4cb14098676c79/68747470733a2f2f776f6f766963746f72792e6769746875622e696f2f696d672f747269655f73616d706c65322e706e67

### **Trie 자료구조의 특징**

- 정렬된 트리 구조이다.(데이터에 따라 이진트리일 때도 있다.)
- Trie는 자식 노드를 Map<Key, Value> 형태로 가지고 있다.
- 루트 노드를 제외한 노드의 자손들은 해당 노드와 공통 접두어를 가진다.
- 루트 노드는 빈 문자와 연관있다.(특정 문자가 할당되어 있지 않다.)