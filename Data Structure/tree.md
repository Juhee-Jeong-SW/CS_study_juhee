# Tree

## 📌 Tree

### 의미

- 선형 자료 구조 예로, 배열에서 삽입 삭제 시 O(n) 걸림.
  - BUT, 편향 트리가 아닌 이상, 일반적 트리에선 **O(logN)** 가능

### 특징

- 비선형 자료구조

- `계층적 관계`를 표현하는 자료구조

- 표현에 집중

  → 무엇인가를 저장하고 꺼내야 한다는 사고에서 벗어나자!

- 루트 노드를 제외한 모든 노드는 단 하나의 부모 노드만을 가짐.

### 구성 요소
![tree그림](https://user-images.githubusercontent.com/70262329/103750211-cef61300-5049-11eb-988c-28833e908737.png)

- 노드(Node) : 트리를 구성하고 있는 각각의 요소
- 간선(Edge) : 트리를 구성하기 위해 노드와 노드를 연결하는 선
- 루트 노드(Root Node) : 트리 구조에서 최상위에 있는 노드
- 단말 노드(Terminal Node=Leaf Node) : 하위에 다른 노드가 연결되어 있지 않은 노드
- 내부 노드(비단말 노드, Internal Node) : 단말 노드를 제외한 모든 노드, 루트노드도 포함

## 📌 이진 트리 (Binary Tree)

- 루트 노드를 중심으로 두 개의 서브트리로 나뉘어 짐. (노드가 없을 수도..) 나누어진 두 서브트리 모두 이진 트리여야 함.

- 트리의 레벨 : 각 층별로 숫자를 매긴 것

  - 레벨은 1부터 시작, 로트 노드 레벨 : 1

- 트리의 높이 : 최고 레벨을 가리키는 것.

- 종류

  - 포화 이진 트리 (Full Binary Tree) : 모든 레벨이 꽉 찬 이진트리

    - 레벨 별로 노드의 개수가 1, 2, 4, 8, 16.. 으로 늘어남. 따라서 일반적인 이진트리에서 각 레벨 별 최대 노드의 개수는 2^(k-1)

    - 레벨 별 노드는 공비가 2인 등비수열.

      → 높이가 h인 이진트리가 가질 수 있는 최대 노드 수는 2^h-1  (등비수열의 합)

  - 완전 이진 트리 ( Complete Binary Tree) : 왼쪽에서 오른쪽으로 순서대로 차곡 차곡 채워진 이진 트리

    - 노드를 삽입할 때, 왼쪽부터 차례대로 삽입하는 트리.
    - 왼쪽이 비어있고, 오른쪽이 들어가있으면 완전 이진 트리 X

  - 편향 이진 트리(Skewed Binary Tree) : 모든 노드가 부모의 왼쪽 자식이기 때문에 왼쪽으로 편향되어 이거나 모든 노드가 부모의 오른쪽 자식이기 때문에 오른쪽으로 편향되어 있는 이진트리
![이진트리종류](https://user-images.githubusercontent.com/70262329/103750214-d0274000-5049-11eb-8be9-e61f7d45dae6.png)


사진 출처 : https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Data Structure/[Data Structure] Tree.md

## 📌 BST (Binary Search Tree)

이진 트리의 일종.

효율적인 탐색을 위한 저장방법을 고민해본 것.

### 데이터 저장 규칙

1. 이진 탐색 트리의 노드에 저장된 키는 유일함.
2. 부모의 키가 왼쪽 자식 노드의 키보다 큼.
3. 부모의 키가 오른쪽 자식 노드의 키보다 작음.
4. 왼쪽과 오른쪽 서브트리도 이진 탐색 트리.

### 시간 복잡도

- **O(log n) := O(h)**

  - 트리의 높이를 하나씩 더해갈수록 추가할 수 있는 노드의 수가 두 배씩 증가함.

- 최악

  - 저장 순서에 따라 계속 한 쪽으로만 노드가 추가되는 경우

    → 편향 트리가 될 경우.

  - **O(n)**

- `Rebalancing 기법`

  - 배열보다 많은 메모리를 사용해 데이터를 저장했지만 탐색에 필요한 시간 복잡도가 같게 되는 비효율적인 현상이 발생할 수 있음. → 해결법!
  - 균형을 잡기 위한 트리 구조의 재조정을 하는 것

## 📌 Binary Heap

저료구조의 일종.

Tree 형식을 하고 있음. Tree 중에서도 배열에 기반한 Complete Binary Tree 임 .

### 특징

- 배열에 트리의 값을 넣어줄 때, 0번째는 건너뛰고 1번 index부터 루트노드가 시작됨.

  → 노드의 고유번호 값과 배열의 index를 일치시켜 혼동을 줄이기 위함.

### 종류

- Max Heap
  - Root node에 있는 값이 제일 크므로 최대값을 찾는 데 소요되는 연산의 시간복잡도 : **O(1)**
  - complete binary search 이므로 배열을 사용하여 효율적 관리 가능 → Random Access 가능
- Min Heap
  - 최소값을 찾는 데 소요되는 연산의 시간복잡도 : **O(1)**
  - heap구조를 유지하기 위해 제거된 루트 노드를 대체할 다른 노드 필요
  - heap은 맨 마지막 노드를 루트 노드로 대체시킨 후, 다시 heapify 과정을 거쳐 heap 구조를 유지함.
  - 이 경우 **O(log n)**의 시간 복잡도로 최대/최소값에 접근할 수 있게 됨.

## 📌 Red Black Tree

BST를 기반으로 하는 트리 형식의 자료구조.

동일한 노드의 개수일 때, depth를 최소화하여 시간 복잡도를 줄이는 것이 핵심!

→ 이 경우 tree가 complete binary tree임.

### 정의

다음의 성질을 만족하는 BST임

1. 각 노드는 red of black 이라는 색깔을 가짐.

2. Root node 의 색깔은 Black 임.

3. 각 leaf node 는 black이다.

4. 어떤 노드의 색깔이 red 라면 두 개의 children 의 색깔은 모두 black 임.

5. 각 노드에 대해 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은 수의 black nodes 들을 포함하고 있음. 이를 해당 노드의 black-height 라고 함.

   cf) Black-Height: 노드 x 로부터 노드 x 를 포함하지 않은 leaf node 까지의 simple path 상에 있는 black nodes 들의 개수

### 특징

- BST 특징 모두 가짐.
- Root node로 부터 leaf node까지의 모든 경로 중 최소 경로와 최대 경로의 크기 비율은 2보다 크지 않다. → Balanced 상태
- 노드의 child 가 없을 경우 child 를 가리키는 포인터는 NIL 값을 저장함. 이러한 NIL 들을 leaf node로 간주함.

### 시간복잡도

- Search, Insert, Delete : **O(log n)**

### **삽입**

우선 BST 의 특성을 유지하면서 노드를 삽입을 한다. 그리고 삽입된 노드의 색깔을 **RED 로** 지정한다. Red 로 지정하는 이유는 Black-Height 변경을 최소화하기 위함이다. 삽입 결과 RBT 의 특성 위배(violation)시 노드의 색깔을 조정하고, Black-Height 가 위배되었다면 rotation 을 통해 height 를 조정한다. 이러한 과정을 통해 RBT 의 동일한 height 에 존재하는 internal node 들의 Black-height 가 같아지게 되고 최소 경로와 최대 경로의 크기 비율이 2 미만으로 유지된다.

### **삭제**

삭제도 삽입과 마찬가지로 BST 의 특성을 유지하면서 해당 노드를 삭제한다. 삭제될 노드의 child 의 개수에 따라 rotation 방법이 달라지게 된다. 그리고 만약 지워진 노드의 색깔이 Black 이라면 Black-Height 가 1 감소한 경로에 black node 가 1 개 추가되도록 rotation 하고 노드의 색깔을 조정한다. 지워진 노드의 색깔이 red 라면 Violation 이 발생하지 않으므로 RBT 가 그대로 유지된다.

Java Collection 에서 ArrayList 도 내부적으로 RBT 로 이루어져 있고, HashMap 에서의 `Separate Chaining`에서도 사용된다. 그만큼 효율이 좋고 중요한 자료구조이다.
