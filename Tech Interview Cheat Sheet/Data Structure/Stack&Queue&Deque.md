# Stack & Queue & Deque

먼저 Stack과 Queue는 자료구조에서 가장 기본이 되는 중요한 추상자료형\*(Abstract Data Type, ADT)이다.

\* 추상자료형(Abstract Data Type, ADT)은 구현 방법을 명시하지 않고 자료구조의 특성과 연산을 명시한 것이다.

<br/>

## 스택(Stack)

**Stack** 이라는 이름은 쌓아올린다는 의미를 가지고 있다. 그래서 Stack은 쌓아올린 형태의 자료구조를 의미한다.  
스택은 한 쪽 방향에만 자료를 추가 및 삭제 할 수 있으며 가장 마지막에 삽입된 자료의 위치를 `top`이라 한다.  
스택은 `top`에만 접근이 가능하기 때문에 그 외의 위치에 대한 데이터 추가 및 삭제가 불가능하다.
**후입선출(Last-In-First-Out, LIFO)** 방식으로 동작한다.

<img width="330px" src="https://user-images.githubusercontent.com/66757141/208432228-d060964a-44ff-4c77-860e-dda2b7b8a873.png" alt="difference-between-stack-and-queue1" />

#### ADT Stack의 연산

1. `push(item)` : stack에 item을 삽입한다(만약 size를 초과한다면 false를 반환할 수 있다). `O(1)`
2. `pop()` : stack의 top에 위치한 item을 반환하면서 동시에 제거한다(반환하지 않을 수 있다). `O(1)`
3. `peek()` : stack의 top에 위치한 item을 삭제 없이 반환한다. `O(1)`
4. `ifFull()` : stack이 가득 차있다면 true, 아니라면 false를 반환한다. `O(1)`
5. `isEmpty()` : stack에 item이 없다면 true, 아니라면 false를 반환한다. `O(1)`

#### Stack의 장단점

1. `top` 위치의 데이터에 바로 접근하므로 데이터 삽입, 삭제의 시간 복잡도가 `O(1)`로 빠르다.
2. `top` 이외의 데이터에 접근할 수 없으므로 탐색이 불가능하다. 탐색하려면 모든 데이터를 `pop()`해야 한다.

#### Stack의 활용

- 재귀 알고리즘
- DFS 알고리즘
- 작업 실행 취소와 같은 역추적 작업이 필요할 때
- 괄호 검사, 후위 연산법, 문자열 역순 출력 등

<br/>

## 큐(Queue)

**Queue** 라는 이름은 대기열을 의미한다. 줄을 서서 기다리는 사람들과 유사하다.  
Queue는 한 쪽에서 삽입, 반대 쪽에서 삭제가 이루어진다. 삽입이 이루어지는 쪽을 `rear`, 데이터가 삭제되는 쪽은 `front`라고 한다.
**선입선출(First-In-First-Out, FIFO)** 방식이다.

<img width="400px" src="https://user-images.githubusercontent.com/66757141/208432243-3b54920f-2305-463a-9f4e-248b127b2252.png" alt="difference-between-stack-and-queue2" />

#### ADT Queue의 연산

1. `enqueue(item)` : queue에 item을 삽입한다. `O(1)`
2. `dequeue()` : queue의 front에 위치한 item을 반환하고 삭제한다. `O(1), O(N)`
3. `peek()` : queue의 front에 위치한 item을 삭제 없이 반환한다. `O(1)`
4. `ifFull()` : queue이 가득 차있다면 true, 아니라면 false를 반환한다. `O(1)`
5. `isEmpty()` : queue에 item이 없다면 true, 아니라면 false를 반환한다. `O(1)`

#### Queue의 장단점

1. `front` 위치의 데이터에 바로 접근하므로 데이터 삽입, 삭제의 시간 복잡도가 `O(1)`로 빠르다.
2. 큐 역시 `front`가 아닌 중간에 위치한 데이터 접근이 불가능하다.
3. Queue 를 Linked List가 아니라 일반 `Array`로 구현하면 dequeue의 시간복잡도가 `O(n)`이 됨에 유의한다. (front의 item을 삭제하면 모두 앞으로 한칸식 이동하게 된다.)

#### Queue의 활용

- 데이터를 입력된 순서대로 처리해야 할 때
- BFS 알고리즘
- 프로세스 관리
- 대기 순서 관리

<br/>

## 덱(Deque)

**덱(Deque)** 은 **Double-Ended Queue**의 약어이다.  
큐의 앞(front)과 뒤(rear, back) 모두에서 삽입과 삭제가 가능한 큐를 말하며, 때문에 Stack 처럼도 Queue처럼도 사용이 가능하다.

![anod](https://user-images.githubusercontent.com/66757141/208432148-60954075-b7cd-46d6-9b05-efd5e197320d.png)

#### ADT Deque의 연산

1. `push_front(item)` : queue의 front에 item을 추가한다. `O(1)`
2. `pop_front()` : front의 item을 삭제 및 반환한다. `O(1)`
3. `push_rear(item)` : queue의 rear에 item을 추가한다. `O(1)`
4. `pop_rear()` : rear의 item을 삭제 및 반환한다. `O(1)`

#### Deque의 장단점

1. 데이터의 앞, 뒤 모두에서 삽입 삭제가 모두 가능하며 O(1)의 빠른 시간복잡도를 갖는다.
2. 스택, 큐에 비해 구현이 어렵다.

\+

3. 크기가 가변적이다.
4. index 를 통해 임의의 원소에 O(1)시간복잡도로 바로 접근이 가능하다.
5. 새로운 원소 삽입 시, 메모리를 재할당하고 복사하지 않고 새로운 단위의 메모리 블록(chunk)을 할당하여 삽입한다.  
   _(3은 연결리스트로 구현했을 경우를 생각하면 쉽게 이해되는 부분이나 4~5에서는 C++의 std::Deque에 관한 설명과 혼용 된 것 같다.)_

#### Deque의 활용

- 데이터를 앞, 뒤 모두에서 삽입 삭제하는 과정이 필요한 경우
- 데이터의 크기가 가변적일 경우

<br/>

## Underflow & Overflow

자료구조가 비어있을 때 pop()과 같은 출력을 시도하면 `underflow`, 자료구조의 공간이 가득 찼을 때 push()와 같은 삽입을 시도하면 `overflow` 되며 오류를 야기한다.

<br/>

---

## Reference

📄https://www.tutorialandexample.com/difference-between-stack-and-queue  
📄https://devuna.tistory.com/22  
📄https://2jinishappy.tistory.com/134  
📄https://velog.io/@nnnyeong/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-Stack-%ED%81%90-Queue-%EB%8D%B1-Deque  
📄https://www.tutorialspoint.com/data_structures_algorithms/stack_algorithm.htm?key=queue  
📄https://www.tutorialspoint.com/data_structures_algorithms/dsa_queue.htm  
📄https://www.geeksforgeeks.org/deque-in-python/  
📄https://en.cppreference.com/w/cpp/container/deque
