# Linked List

연결리스트(Linked List)는 한 줄로 연결되어있는 형태의 선형 자료 구조이다. 연속적인 메모리 공간을 사용하지 않는 대신 노드에 데이터와 포인터를 가져 다음 노드를 가리키는 방식으로 연결된다.

<img src="https://user-images.githubusercontent.com/66757141/208934650-d3ecb919-290a-4c58-b0a0-06ea8dfa13aa.png" alt="Singly-linked-list" width="300px" />

<br/>

## Linked List의 특성

1. 요소의 삭제, 추가의 시간복잡도가 `O(1)`로 빠르다. 배열은 요소가 삽입 및 삭제될 경우 모든 데이터들이 재배치되어 시간 복잡도가 `O(N)`이지만 연결 리스트는 해당 노드간의 연결만 수정하는 방식으로 빠르다.
2. 인덱스를 통해 중간 위치에 접근할 때 배열보다 느리다. 링크드리스트는 노드를 순회하며 접근하여 O(N)이 소요된다.

<br/>

## Linked List의 종류

**단일 연결 리스트(Singly linked list)**  
단일 연결 리스트는 각 노드에 자료 공간과 한 개의 포인터 공간이 있고, 각 노드의 포인터는 다음 노드를 가리킨다.

<img src="https://user-images.githubusercontent.com/66757141/208934650-d3ecb919-290a-4c58-b0a0-06ea8dfa13aa.png" alt="Singly-linked-list" width="300px" />

**이중 연결 리스트(Doubly linked list)**  
이중 연결 리스트의 구조는 단일 연결 리스트와 비슷하지만, 포인터 공간이 두 개가 있고 각각의 포인터는 앞의 노드(forward, next)와 뒤의 노드(backwards, prev)를 가리킨다.

<img src="https://user-images.githubusercontent.com/66757141/208934722-7824ebde-cf13-4e58-8e25-10f1df7a9ae2.png" alt="Doubly-linked-list" width="450px" />

**다중 연결 리스트(Multiply linked list)**  
다중 연결 리스트는 두개 이상의 포인터를 가지는 연결 리스트를 의미하며, 이중 연결 리스트를 포함한다.

**원형 연결 리스트(Circular linked list)**  
원형 연결 리스트는 일반적인 연결 리스트에 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조이다.

<img src="https://user-images.githubusercontent.com/66757141/208934749-280d70f4-1ba4-48fc-9543-403d82dd0ddb.png" alt="Circularly-linked-list" width="260x" />

<br/>

## Linked List 연산

단일 연결 리스트에서 노드의 삽입과 삭제 과정을 살펴본다. 이중 연결 리스트의 경우 prev와 next를 모두 수정해주면 된다.

**노드 삽입**  
Node A와 C 사이에 B를 삽입하고자 할 때, B가 C를 가리키도록 한 후, A가 B를 가리키게 한다.

![474px-CPT-LinkedLists-addingnode svg](https://user-images.githubusercontent.com/66757141/208935569-6ede4e92-a6c8-4afd-a815-4364d669917c.png)

```java
function insertAfter(Node node, Node newNode) // insert newNode after node
    newNode.next := node.next
    node.next    := newNode
```

**노드 삭제**

Node A, B, C가 차례로 연결되어있을 때 B를 삭제하고자 한다면, A가 C를 가리키도록 한 후 Node B를 삭제한다.

![380px-CPT-LinkedLists-deletingnode svg](https://user-images.githubusercontent.com/66757141/208935589-6820192b-90b0-4a3b-9790-6023abc38449.png)

```java
function insertAfter(Node node, Node newNode) // insert newNode after node
    newNode.next := node.next
    node.next    := newNode
```

<br/>

---

## Reference

📄https://ko.wikipedia.org/wiki/연결_리스트  
📄https://en.wikipedia.org/wiki/Linked_list
