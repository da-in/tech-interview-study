# 이진탐색트리 (Binary Search Tree)

각 노도의 자식노드가 최대 2개인 이진트리에 여러 조건이 붙은 트리

## 특징
- 각 노드에 중복되지 않는 키(key)가 있다.
- 루트 노드의 왼쪽 서브 트리는 루트 노드 키보다 작은 키를 갖는 노드들로 구성
- 루트 노드의 오른쪽 서브 트리는 루트 노드 키보다 큰 키를 갖는 노드들로 구성
- 좌우 서브 트리도 모두 이진 탐색 트리여야 한다. </br>

![1](https://user-images.githubusercontent.com/102718303/209345564-989928b2-01e6-47b6-a7c5-2fc9fca28dbb.png)


## 탐색
- 루트 노드의 키와 찾고자 하는 값 비교 (루트 노드가 그 값이라면 탐색 종료)
- 찾고자 하는 값이 루트 노드보다 작다면 왼쪽 서브 트리로 탐색 진행
- 찾고자 하는 값이 루트 노드보다 크다면 오른쪽 서브 트리로 탐색 진행
- 위 과정 반복 </br>

![탐색](https://user-images.githubusercontent.com/102718303/209469225-bec5a41a-cb0f-4e56-97b1-c9215998da4c.png)


## 삽입
- 트리에 삽입할 값이 있다면 오류 발생 (중복 x)
- 루트 노드 부터 값을 비교하면서 추가 </br>

![삽입](https://user-images.githubusercontent.com/102718303/209469233-0d23a206-290e-489b-8be0-5925481dd1ab.png)


## 삭제
- 삭제하려는 노드가 **리프 노드**일 경우 : 그냥 삭제
- 삭제하려는 노드의 **서브 트리가 하나**인 경우 : 해당 노드를 삭제하고 부모 노드가 삭제한 노드의 자식 노드를 가리키면 된다. </br>
  ![2](https://user-images.githubusercontent.com/102718303/209345876-8cfb6a14-8995-4a6a-8e00-f85e57576d81.png)


- 삭제하려는 노드의 **서브 트리가 두 개**인 경우 : 두가지 방법</br>
  
  - 오른쪽 서브 트리에서 가장 작은 값을 삭제 노드 자리로 옮긴다. </br>
  ![삭제](https://user-images.githubusercontent.com/102718303/209469252-28797efa-a54b-4584-9ff9-436975b1f330.png)
  
  - 왼쪽 서브 트리에서 가장 큰 값을 삭제 노드 자리로 옮긴다 </br>


## 장점
- 배열을 사용하여 탐색 할 때보다 시간복잡도 감소 : `O(logN)`

## 단점
- 트리 모양이 한쪽으로 치우치게 되면 시간복잡도가 `O(N)` 근접 

----

## Reference
- https://code-lab1.tistory.com/10
- https://yoongrammer.tistory.com/71
- https://ansohxxn.github.io/algorithm/bst/
