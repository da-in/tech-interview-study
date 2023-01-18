# B-Tree & B+tree

## 배경

단순 트리구조는 한 노드의 하나의 데이터 값만 존재 </br>
하드디스크 같은 외부 기억장치들은 블럭 단위로 파일을 입출력 </br>
입출력시 발생하는 비용은 파일 크기와 상관없이 동일 (한 블럭에 조금 차있던, 꽉 차있던 비용 동일) </br>
한 블럭에 **여러 데이터를 동시 저장하는 것**이 효율적 </br>

# B-Tree

이진트리부터 개선된 트리의 형태이고, 스스로 트리의 균형을 유지한다.
B-Tree는 하나의 노드에 2개 이상의 값을 가지고 있기 때문에 **차수(M)** 개념 등장 </br>

## M차 B-Tree 조건
- leaf node를 제외한 내부 node는 [M/2] ~ M개의 자식노드를 가진다. 
- 각 node는 [M/2-1] ~ M-1개의 데이터를 가진다.
- 데이터의 수가 K개라면 자식의 수는 K+1이다. 
- 한 데이터는 Tree에 한번만 등장한다. (중복x)
- 데이터는 모두 정렬되어 있다.
- 모든 leaf node는 같은 레벨에 존재 </br>


## 탐색 - 하향식 
1. root node부터 탐색
2. K를 찾으면 탐색 종료
3. K와 데이터 값 비교하며 leaf node까지 반복 </br>

![탐색](https://user-images.githubusercontent.com/102718303/209688623-e626f589-06e9-4517-b627-4d14014aff87.png)


## 삽입 - 상향식
1. 트리가 비어있다면 root node 할당 후 삽입
2. 비어 있지 않다면, 데이터를 삽입 할 leaf node 탐색
3. 삽입 후 M차 조건을 만족하면 종료, 아니라면 분리</br>
  - 분리가 일어나지 않는 경우
  - 분리가 일어나는 경우 </br>
    1. 분리할 노드의 왼쪽 값은 왼쪽 자식, 오른쪽 값은 오른쪽 자식으로 분리 (가운데가 부모로)
    2. 부모 노드가 조건을 만족하지 않는다면 위의 과정 반복 </br>
    ![삽입](https://user-images.githubusercontent.com/102718303/209688593-0c2bfce1-1c38-4933-ab67-85f045a2c0f5.png)


## 삭제

삭제는 삽입보다 복잡하고 케이스가 많고, 기본 베이스는 **재분배**와 **합침**이다.</br>

**1. 리프노드 삭제**
  - 삭제해도 조건 만족 : 그냥 삭제 </br>
  ![삭제1](https://user-images.githubusercontent.com/102718303/209688569-69f66186-cdd5-41c4-ae71-7b884a2728b2.png)

  
  - 조건은 만족하지 않지만, 옆 노드에서 빌려올 수 있는 경우
   1. 리프노드의 형제 노드에서 빌려야 할 값 찾기 -> 왼쪽 형제 노드면 최대값, 오른쪽 형제 노드라면 최소값.
   2. 리프 노드와 형제 노드를 동시에 가리키는 부모 노드 값 찾기
   3. 삭제 노드를 삭제 후, 2번의 값을 내리고, 1번의 값을 부모로 올린다. </br>
   ![image](https://user-images.githubusercontent.com/102718303/209688200-256e17c6-e8ef-4bc7-bc3f-4d966c1ef5cd.png)

   

  - 조건도 만족하지 않고, 빌려올 수도 없는 경우
   1. 삭제할 노드와 형제 노드를 병합
   2. 병합 노드의 조건 만족을 위해 부모 노드의 값을 내려준다.
   3. 부모 노드가 조건을 만족하지 않는 다면 1-2번 과정을 수행한다. </br>
   ![삭제3](https://user-images.githubusercontent.com/102718303/209688537-5c04da9e-230d-4403-9b75-109a1aa7fe6c.png)

  
  
**2. 내부노드 삭제** </br>
- 자식 노드에서 값을 빌려오는 경우 
- 자식 노드의 값을 빌려올 수 없지만, 부모 노드가 여유있는 경우 </br>
![삭제5](https://user-images.githubusercontent.com/102718303/209688475-aeea4599-692d-488c-afd7-60e42f863aad.png)

- 자식 노드, 부모 노드 둘 다 여유가 없는 경우 </br>
![삭제6](https://user-images.githubusercontent.com/102718303/209688490-8581e5c0-022a-4393-a110-db23331ac35a.png)


> B-Tree 시물레이션
> https://www.cs.usfca.edu/~galles/visualization/BTree.html </br>




# B+-Tree

## B-Tree와 다른점 </br>
- 리프 노드에 모든 키와 데이터가 존재 / 정렬 / 연결리스트로 연결 `O(logN)`
- non-leaf node에는 키 값과 포인터만 존재
- 키 값의 중복 등장 가능 </br>

![image](https://user-images.githubusercontent.com/102718303/208671369-f38f2d03-ed94-4915-8488-48cd570ae87d.png)

## M차 B+-Tree의 조건
- 리프 노드를 제외한 내부 노드는 M/2 ~ M개의 자식노드를 가진다. 
- 각 노드는 [M/2 - 1] ~ M-1개의 키를 가진다.
- 키의 수가 K개라면 자식의 수는 K+1이다.
- 리프 노드의 키는 모두 정렬되어 있다. 
- 모든 리프 노드는 같은 레벨에 존재 </br>

## 삽입
**1. 분할이 일어나지 않고, 삽입 위치가 리프 노드의 가장 앞자리가 아닌 경우** : B-Tree와 동일한 방식 </br>

  
**2. 분할이 일어나지 않고, 삽입 위치가 리프 노드의 가장 앞자리인 경우** 삽입 후 부모 키를 삽입된 키로 갱신 </br>

  ![image](https://user-images.githubusercontent.com/102718303/208671720-4f3c0a20-3a73-456f-880a-0c69031fc9c4.png)

**3. 분할이 일어나는 경우** </br>
   - B-Tree와 동일한 방식으로 분할

  ![image](https://user-images.githubusercontent.com/102718303/208672313-2164acd1-3811-42bc-a2f2-187a93f7b14e.png)
  ![image](https://user-images.githubusercontent.com/102718303/208672394-5a51e195-a0bb-4182-8420-a78b93270b60.png)
  ![image](https://user-images.githubusercontent.com/102718303/208672448-9c9187fa-f87c-4771-b06f-2055dc9e141e.png)


## 삭제
기본적 틀은 B-Tree와 비슷하지만, 삭제된 키가 내부노드에 존재할 수 있다는 점이 특징이다. </br>

**1. 삭제할 키가 내부노드에 없고, 리프 노드의 처음이 아닌경우 : 그냥 삭제** </br>

**2. 삭제할 키가 리프 노드의 처음인 경우** </br>
  ![image](https://user-images.githubusercontent.com/102718303/208674252-ec416e65-0b54-49f8-9429-c6a81b216eb2.png)
  ![image](https://user-images.githubusercontent.com/102718303/209690813-142c8f80-27a8-4bcb-8ee1-90f8c0694f6d.png)
  ![image](https://user-images.githubusercontent.com/102718303/208674299-1ec8645a-0b66-4202-aa3a-00d16fade6ed.png)
    
>B+-Tree 시물레이션
>https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html


## 장점 (DB에서 B-Tree, B+-Tree를 사용하는 이유)
- 항상 정렬된 상태로 특정 값보다 크고 작은 부등호 연산에 문제가 없다.
- 포인터가 적기 때문에 많은 데이터가 존재해도 빠르게 접근 가능
- 데이터 탐색, 저장, 수정, 삭제에도 항상 O(logN) </br></br>



## Reference
- https://ssocoit.tistory.com/217
- https://code-lab1.tistory.com/217
- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ya3344&logNo=221395287263
- https://siahn95.tistory.com/entry/DB-%EC%9D%B8%EB%8D%B1%EC%8A%A4%EB%9E%80-2-%EA%B5%AC%EC%A1%B0-B-Tree-%EA%B3%84%EC%97%B4%EC%9D%84-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0
- https://mommoo.tistory.com/108
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree
