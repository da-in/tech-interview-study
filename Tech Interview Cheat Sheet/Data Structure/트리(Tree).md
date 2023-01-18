# 트리 (Tree)

**트리(Tree)** 란 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조이다. </br></br>
![image](https://user-images.githubusercontent.com/102718303/209174654-391cc4d2-6d44-4fcd-b1af-efd0753305f5.png)


## 기본 용어
- **노드 (node)** : 트리를 구성하는 기본 요소
- **간선 (edge)** : 노드와 노드 간의 연결선
- **루트 노드, 부모 노드, 자식 노드**
- **리프 노드** : 자식 노드가 없는 노드
- **내부 노드** : 자식 노드를 하나 이상 가진 노드
- **깊이 (depth)** : 루트에서 어떤 노드까지의 간선 수
- **높이 (height)** : 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선 수
- **Degree** : 노드의 자식 수
- **Breadth** : 리프 노드의 수
- **Order** : 부모 노드가 가질 수 있는 최대 자식 수


## 특징
- 하나의 루트 노드만 가지고, 0개 이상의 하위 트리로 구성
- 데이터를 순차적으로 저장하지 않으므로 **비선형 자료구조**
- 트리내에 또 다른 트리 (subtree)가 있는 재귀적 자료구조
- **loop**를 갖지 않고, 연결된 **무방향 그래프** 구조
- 노드 간의 부모 자식 관계를 가지는 계층형 자료구조이고, 모든 자식 노드는 하나의 부모 노드만 갖는다.
- 노드가 n개인 트리는 항상 n-1개의 간선을 가진다. </br>

![image](https://user-images.githubusercontent.com/102718303/209174766-a606cd00-4ff6-4f81-a59a-fbc9f052e2aa.png)


## 트리 종류

#### 편향트리 (Skew Tree)
- 모든 노드들이 자식을 하나만 가진 트리 </br>
>왼쪽 방향으로만 가질 때 left skew tree, 오른쪽 방향으로만 가질 때 right skew tree </br></br>

![image](https://user-images.githubusercontent.com/102718303/209174882-074b3284-eac8-435d-bcea-2e99740e9cb5.png)


#### 이진트리 (Binary Tree)
- 각 노드의 자식 노드가 2개 이하인 트리 </br>

![image](https://user-images.githubusercontent.com/102718303/209175599-8cea12fa-9b1f-4785-8495-1e21acebe15f.png)

#### 이진탐색트리 (Binary Search Tree)
- 순서화된 이진 트리
- 노드의 왼쪽 자식은 부모 노드보다 작은 값, 오른쪽 자식은 부모 노드보다 큰 값을 가진다. </br>

![image](https://user-images.githubusercontent.com/102718303/209175862-f3d2b5ec-2da8-4955-9b49-dd36b61df122.png)

#### m원 탐색 트리 (m-way Search Tree)
- 최대 m개의 서브 트리를 갖는 탐색 트리
- 이진 탐색 트리의 확장된 형태로 높이 (height)를 줄이기 위해 사용 </br>

![image](https://user-images.githubusercontent.com/102718303/209177672-9b2f2f0a-bd9b-4ec1-adaf-8ab9fae1afce.png)

#### 균형 트리 (Balanced Tree, B-Tree)
- m원 탐색 트리에서 높이 균형을 유지하는 트리</br>


## 트리 순회 방식 (중요!)

- **Preorder (전위 순회)** : 루트 노드 -> 왼쪽 서브 트리 -> 오른쪽 서브 트리</br>
![Preorder-traversal](https://user-images.githubusercontent.com/102718303/209254137-f1ef93ab-63bc-4d36-95a0-93384b30e37b.gif)

- **Inorder (중위 순회)** : 왼쪽 서브 트리 -> 노드 -> 오른쪽 서브 트리 </br>
![Inorder-traversal](https://user-images.githubusercontent.com/102718303/209254209-d21324df-c98d-4387-b894-d7045169146e.gif)

- **Postorder (후위 순회)** : 왼쪽 서브 트리 -> 오른쪽 서브 트리 -> 노드 </br>
![Postorder-traversal](https://user-images.githubusercontent.com/102718303/209254265-04bfe1b3-0087-4c7a-9b49-790cc66c47a8.gif)


## 어디에 쓰이는가?

- 계층적 데이터 저장
- 효율적인 검색 속도
- 힙 (Heap)
- 데이터 베이스의 인덱싱 (B-Tree, B+Tree)
- Trie (트라이) 자료구조 </br>
---

## Reference
- https://yoongrammer.tistory.com/68
- https://code-lab1.tistory.com/8
- https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%A6%AC-Tree
