# 트리(Tree)

**트리(Tree)** 는 그래프(Graph)의 한 형태로, 계층적인 관계를 표현하는 비선형 자료구조이다.  


## 트리의 요소

기본적으로 트리는 그래프이므로 **노드(Node)** 와 **간선(Edge)** 으로 구성된다.

- **노드(Node)**: 트리를 구성하는 기본 요소로, 데이터와 다른 노드와의 연결 정보를 가지고 있다. 정점(vertex)라고도 한다.
- **간선(Edge)**: 노드와 노드를 연결하는 선이다. 부모 노드와 자식 노드를 연결한다.

트리는 그래프의 한 케이스로, 루트 노드로부터 하위에 자식 노드를 두어 계층적인 구조를 가지고 있다.

- **루트(Root) 노드**: 최상위 노드로 유일하다.
- **리프(Leaf) 노드**: 자식 노드가 없는 노드를 말한다.
- **깊이(depth)** : 루트에서 어떤 노드까지의 간선 수로, 레벨(Level)이라고도 한다.
- **높이(height)** : 트리의 최대 깊이

<img src="https://user-images.githubusercontent.com/102718303/209174654-391cc4d2-6d44-4fcd-b1af-efd0753305f5.png" width="500px">

## 트리의 특징
- 부모 자식 관계를 가지는 **계층형 자료구조** 로, 방향성이 있으며, 모든 자식 노드는 하나의 부모 노드만 갖는다.
- 두 개의 노드 사이에는 한 개의 간선을 가지며 사이클(Cycle)이 존재하지 않아 **최소 연결 트리** 라고 부르기도 한다.
- 트리 내에 하위 트리(Sub Tree)가 있는 **재귀적 자료구조** 이다.
- 노드가 `n`개인 트리는 항상 `n-1`개의 간선을 가진다.

## 트리의 종류

#### 편향트리(Skew Tree)
모든 노드들이 자식을 하나만 갖는 트리이다.  
> 왼쪽 방향으로만 자식을 가지면 Left Skew Tree, 오른쪽 방향으로만 자식을 가지면 Right Skew Tree라고 한다.

<img src="https://user-images.githubusercontent.com/102718303/209174882-074b3284-eac8-435d-bcea-2e99740e9cb5.png" />


#### 이진트리(Binary Tree)
모든 부모 노드가 2개 이하의 자식 노드를 갖는 트리이다.

<img src="https://user-images.githubusercontent.com/102718303/209175599-8cea12fa-9b1f-4785-8495-1e21acebe15f.png" width="250px" />

#### 이진 탐색 트리(Binary Search Tree)
정렬된 이진 트리이다.  
노드의 왼쪽 자식은 부모 노드보다 작은 값, 오른쪽 자식은 부모 노드보다 큰 값을 갖는다.

<img src="https://user-images.githubusercontent.com/102718303/209175862-f3d2b5ec-2da8-4955-9b49-dd36b61df122.png" width="360px" />

#### 다원 탐색 트리(Multiway Search Tree)
한 노드 내에 최대 `m-1`개의 요소와 `m`개의 자식을 가질 수 있는 트리이다.  
이진 탐색 트리의 확장된 형태로 높이(height)를 줄이기 위해 사용한다.

<img src="https://user-images.githubusercontent.com/102718303/209177672-9b2f2f0a-bd9b-4ec1-adaf-8ab9fae1afce.png" width="600px" />

#### 균형 트리(Balanced Tree, B-Tree)
다원 탐색 트리에서 높이 균형을 유지하는 트리이다.  
자세한 내용은 [B-Tree](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Data%20Structure/B-Tree%20%26%20B%2Btree.md) 에서 다룬다.


## 트리 순회 방식 [중요]

- **Preorder (전위 순회)** : 부모 노드 > 왼쪽 서브 트리 > 오른쪽 서브 트리  
<img alt="Preorder-traversal" src="https://user-images.githubusercontent.com/102718303/209254137-f1ef93ab-63bc-4d36-95a0-93384b30e37b.gif" width="300px" />

- **Inorder (중위 순회)** : 왼쪽 서브 트리 > 부모 노드 > 오른쪽 서브 트리  
<img alt="Inorder-traversal" src="https://user-images.githubusercontent.com/102718303/209254209-d21324df-c98d-4387-b894-d7045169146e.gif" width="300px" />

- **Postorder (후위 순회)** : 왼쪽 서브 트리 > 오른쪽 서브 트리 > 부모 노드
<img alt="Postorder-traversal" src="https://user-images.githubusercontent.com/102718303/209254265-04bfe1b3-0087-4c7a-9b49-790cc66c47a8.gif" width="300px" />


## 트리의 활용

- 계층적 데이터 저장
- 효율적인 검색 속도
- 힙(Heap)
- 데이터 베이스의 인덱싱(B-Tree, B+Tree)
- [Trie(트라이)](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Data%20Structure/Trie.md) 자료구조

---

## Reference
- https://yoongrammer.tistory.com/68
- https://code-lab1.tistory.com/8
- https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%A6%AC-Tree
