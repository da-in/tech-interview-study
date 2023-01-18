# Heap

Heap은 비선형 자료구조이다.

## 우선순위 큐(Priority Queue)

우선순위 큐는 FIFO(First In First Out)인 일반 큐와 달리 우선 순위가 높은 요소가 먼저 나가는 추상자료형\*이다. 일반적으로 배열, 연결리스트, 힙 등으로 구현한다.

\* 추상자료형(Abstract Data Type, ADT)은 구현 방법을 명시하지 않고 자료구조의 특성과 연산을 명시한 것이다. Stack과 Queue 등이 해당한다.

<img src="https://user-images.githubusercontent.com/66757141/208309563-42d5a615-a55e-4f42-be58-97ac82c2e7c9.png" alt="ds-priority-queue2" width="400px">

_[javatpoint - priority queue](https://www.javatpoint.com/ds-priority-queue)_

우선순위 큐는 일반적으로 아래의 연산을 지원한다.  
`enqueue()` : 새 요소 삽입  
`dequeue()` : 루트의 요소를 삭제하여 그 값을 반환  
`peek()` : 루트 요소를 반환

구현 방식에 따른 시간복잡도는 아래와 같다.

| 자료 구조                               | enqueue() | dequeue() |
| --------------------------------------- | --------- | --------- |
| 배열 (unsorted array)                   | O(1)      | O(N)      |
| 연결 리스트 (unsorted linked list)      | O(1)      | O(N)      |
| 정렬된 배열 (sorted array)              | O(N)      | O(1)      |
| 정렬된 연결 리스트 (sorted linked list) | O(N)      | O(1)      |
| 힙 (heap)                               | O(log N)  | O(log N)  |

<br/>

## 힙(Heap)

힙은 **이진 트리** 형태를 가지며 우선순위가 높은 요소를 루트로 배치하고 항상 루트가 먼저 나간다.  
우선순위가 높은 요소가 먼저 나가기 위해 요소가 삽입 및 삭제 되는 시점에 바로 **정렬**된다.  
루트가 가장 큰 값이 되는 **최대 힙(Max Heap)** 과 루트가 가장 작은 값이 되는 **최소 힙(Min Heap)** 이 있다.

<img src="https://user-images.githubusercontent.com/66757141/208309574-1446e492-3e63-4bc6-a6c2-2c197bb07d21.png" alt="Min-Max-Heap" width="600px">

<br/>

## 힙 요소 추가 push()

1. 추가할 요소를 트리의 가장 마지막 정점에 입력한다.
2. 추가한 요소가 부모 요소보다 우선순위가 높다면 부모와 순서를 바꾼다.
3. 이를 반복하면 가장 우선순위가 높은 요소가 루트가 된다.

\* 요소가 항상 마지막 정점에 추가되기 때문에 힙은 항상 완전 이진트리이며, 완전 이진트리의 높이는 `log N`이므로 힙의 요소 추가 알고리즘은 `O(log N)` 시간복잡도를 갖는다.

<img src="https://user-images.githubusercontent.com/66757141/208309577-4340bc21-1247-4597-8b88-c53aa0a6771a.png" alt="Push-min-heap" width="800px">

<br/>

## 힙 요소 제거 pop()

1. 루트 정점의 요소를 제거한다.
2. 가장 마지막 정점의 요소를 루트로 올린다.
3. 루트 요소의 두 자식 중 우선순위가 더 높은 정점과 바꾼다.
4. 두 자식 요소의 우선순위가 더 낮을 때 까지 반복한다.

\* 힙의 요소 제거 알고리즘은 추가와 동일하게 O(log N) 시간복잡도를 가진다.

<img src="https://user-images.githubusercontent.com/66757141/208309579-5dbb6fb6-509d-4081-a61a-c43b438d664b.png" alt="Pop-min-heap" width="800px">

<br/>

## Heap의 응용

힙은 최대 최소 값을 반복적으로 구하는 경우, `Dijkstra`의 **최단 경로 알고리즘**, 최소 신장 트리의 **Prim 알고리즘** 등의 그래프 알고리즘에서 유용하다. 또한 Heapsort 정렬 알고리즘과 Huffman 코딩(데이터 압축 기술)에도 사용된다.

<br/>

## Heap 구현

<img src="https://user-images.githubusercontent.com/66757141/208309585-fa8fc066-558d-4987-baa3-3ecda5d4a260.png" alt="Min-Heap" width="500px">

이진 트리 형태로 구현해도 되고, 배열로 저장해도 된다.

`파이썬`에서는 `heapq` 모듈을 통해 heap 자료구조를 쉽게 사용할 수 있다.  
`heapq` 모듈은 최소힙으로 구현되어있기 때문에 최대힙을 사용하려면 변환이 필요하다. (y=-x 변환)

```python
import heapq
heap = []
heapq.heappush(heap, 50)
heapq.heappush(heap, 10)
heapq.heappush(heap, 20)
result = heapq.heappop(heap)
```

`자바스크립트`에서는 직접 구현하여 사용해야한다.🥲

```javascript
class MaxHeap {
  constructor() {
    this.heap = [null];
  }

  swap(a, b) {
    [this.heap[a], this.heap[b]] = [this.heap[b], this.heap[a]];
  }

  push(value) {
    this.heap.push(value);
    let currentIndex = this.heap.length - 1;
    let parentIndex = Math.floor(currentIndex / 2);

    while (parentIndex !== 0 && this.heap[parentIndex] < value) {
      swap(currentIndex, parentIndex);
      currentIndex = parentIndex;
      parentIndex = Math.floor(currentIndex / 2);
    }
  }

  pop() {
    const returnVlaue = this.heap[1];
    this.heap[1] = this.heap.pop();
    let currentIndex = 1;
    let leftIndex = 2;
    let rightIndex = 3;
    while (
      this.heap[currentIndex] < this.heap[leftIndex] ||
      this.heap[currentIndex] < this.heap[rightIndex]
    ) {
      if (this.heap[leftIndex] < this.heap[rightIndex]) {
        swap(currentIndex, rightIndex);
        currentIndex = rightIndex;
      } else {
        swap(currentIndex, leftIndex);
        currentIndex = leftIndex;
      }
      leftIndex = currentIndex * 2;
      rightIndex = currentIndex * 2 + 1;
    }
  }
}
```

<br/>

---

## Reference

🎨https://www.techiedelight.com/introduction-priority-queues-using-binary-heaps/  
📄https://yoongrammer.tistory.com/81  
📄https://www.javatpoint.com/ds-priority-queue
