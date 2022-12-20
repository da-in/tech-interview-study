# B-Tree & B+tree

## 배경

단순 트리구조는 한 노드의 하나의 데이터 값만 존재 </br>
하드디스크 같은 외부 기억장치들은 블럭 단위로 파일을 입출력 </br>
입출력시 발생하는 비용은 파일 크기와 상관없이 동일 (한 블럭에 조금 차있던, 꽉 차있던 비용 동일) </br>
한 블럭에 **여러 데이터를 동시 저장하는 것**이 효율적 </br>

# B-Tree

B-Tree는 하나의 노드에 2개 이상의 값을 가지고 있기 때문에 **차수(M)** 개념 등장 </br>

## M차 B-Tree 조건
- leaf node를 제외한 내부 node는 M/2 ~ M개의 자식노드를 가진다. 
- 각 node는 floor(M/2-1) ~ M-1개의 데이터를 가진다.
- 데이터의 수가 K개라면 자식의 수는 K+1이다. 
- 한 데이터는 Tree에 한번만 등장한다. (중복x)
- 데이터는 모두 정렬되어 있다.
- 모든 leaf node는 같은 레벨에 존재 </br>


## 탐색 - 하향식 
1. root node부터 탐색
2. K를 찾으면 탐색 종료
3. K와 데이터 값 비교하며 leaf node까지 반복


## 삽입 - 상향식
1. 트리가 비어있다면 root node 할당 후 삽입
2. 비어 있지 않다면, 데이터를 삽입 할 leaf node 탐색
3. 삽입 후 M차 조건을 만족하면 종료, 아니라면 분리</br>

  **- 분리가 일어나지 않는 경우**
  ![image](https://user-images.githubusercontent.com/102718303/208637269-412a07e7-1aa2-47c4-a8c7-1209d9d85484.png)

  **- 분리가 일어나는 경우**
    1. 분리할 노드의 왼쪽 값은 왼쪽 자식, 오른쪽 값은 오른쪽 자식으로 분리 (가운데가 부모로)
    2. 부모 노드가 조건을 만족하지 않는다면 위의 과정 반복 </br>
    ![image](https://user-images.githubusercontent.com/102718303/208637585-aecf3f70-4d3c-4925-9f00-8ba3d3b6c1e7.png)
    ![image](https://user-images.githubusercontent.com/102718303/208637729-1c7690f8-eb9a-409a-986e-70a6bf5d6872.png)



## 삭제

삭제는 삽입보다 복잡하고 케이스가 많다. </br>
기본 베이스는 **재분배**와 **합침**이다. </br>

**1. 리프노드 삭제**
  - 삭제해도 조건 만족 : 그냥 삭제
  ![image](https://user-images.githubusercontent.com/102718303/208639456-2b020bc6-dd94-4e0b-bebc-8893d06edbb4.png) </br>
  
  - 조건은 만족하지 않지만, 옆 노드에서 빌려올 수 있는 경우 : 삭제 값과 부모 값을 바꿔준다.
  ![image](https://user-images.githubusercontent.com/102718303/208639778-f4fa27f3-96f8-4d64-8213-65a4560b0bb6.png)
  ![image](https://user-images.githubusercontent.com/102718303/208639955-b65f2945-ccfa-4e47-b5c8-1875321d6d2d.png) </br>
  
  - 조건도 만족하지 않고, 빌려올 수도 없는 경우 : 부모를 분할
  ![image](https://user-images.githubusercontent.com/102718303/208640159-21397682-ffe4-4fa1-a942-33001dde39c0.png)
  ![image](https://user-images.githubusercontent.com/102718303/208640265-cb6a368d-bc18-43fa-af9f-e59963d849b7.png)
  
  
**2. 내부노드 삭제** </br>
![image](https://user-images.githubusercontent.com/102718303/208641369-1b5c792c-24a2-477a-9aa0-973ec4940cdf.png)
![image](https://user-images.githubusercontent.com/102718303/208641420-bfdaf113-cce1-4535-8b53-a28395d915e6.png)


> B-Tree 시물레이션
> https://www.cs.usfca.edu/~galles/visualization/BTree.html </br>




# B+-Tree

## B-Tree와 다른점 </br>
- leaf node에 모든 키와 데이터가 존재 / 정렬 / 연결리스트로 연결 `O(logN)`
- non-leaf node에는 키 값과 포인터만 존재
- 키 값의 중복 등장 가능 </br>

![image](https://user-images.githubusercontent.com/102718303/208671369-f38f2d03-ed94-4915-8488-48cd570ae87d.png)

## M차 B+-Tree의 조건
- leaf node를 제외한 내부 node는 M/2 ~ M개의 자식노드를 가진다. 
- 각 node는 floor(M/2 - 1) ~ M-1개의 키를 가진다.
- 키의 수가 K개라면 자식의 수는 K+1이다.
- leaf node의 키는 모두 정렬되어 있다. 
- 모든 leaf node는 같은 레벨에 존재 </br>

## 삽입
**1. 분할이 일어나지 않고, 삽입 위치가 leaf node의 가장 앞자리가 아닌 경우** : B-Tree와 동일한 방식 </br>

  
**2. 분할이 일어나지 않고, 삽입 위치가 leaf node의 가장 앞자리인 경우** 삽입 후 부모 키를 삽입된 키로 갱신 </br>

  ![image](https://user-images.githubusercontent.com/102718303/208671720-4f3c0a20-3a73-456f-880a-0c69031fc9c4.png)

**3. 분할이 일어나는 경우** </br>

  ![image](https://user-images.githubusercontent.com/102718303/208672313-2164acd1-3811-42bc-a2f2-187a93f7b14e.png)
  ![image](https://user-images.githubusercontent.com/102718303/208672394-5a51e195-a0bb-4182-8420-a78b93270b60.png)
  ![image](https://user-images.githubusercontent.com/102718303/208672448-9c9187fa-f87c-4771-b06f-2055dc9e141e.png)


## 삭제
기본적 틀은 B-Tree와 비슷하지만, 삭제된 키가 내부노드에 존재할 수 있다는 점이 특징이다. </br>

**1. 삭제할 키가 내부노드에 없고, leaf node의 처음이 아닌경우 : 그냥 삭제** </br>

**2. 삭제할 키가 leaf node의 처음인 경우** </br>
  ![image](https://user-images.githubusercontent.com/102718303/208674252-ec416e65-0b54-49f8-9429-c6a81b216eb2.png)
  ![image](https://user-images.githubusercontent.com/102718303/208674299-1ec8645a-0b66-4202-aa3a-00d16fade6ed.png)
    
>B+-Tree 시물레이션
>https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html



## 장점 (DB에서 B-Tree, B+-Tree를 사용하는 이유)
- 항상 정렬된 상태로 특정 값보다 크고 작은 부등호 연산에 문제가 없다.
- 포인터가 적기 때문에 많은 데이터가 존재해도 빠르게 접근 가능
- 데이터 탐색, 저장, 수정, 삭제에도 항상 O(logN) </br></br>

>상세한 설명과 그림 참조
>- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree
>- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree
</br>


## Reference
- https://ssocoit.tistory.com/217
- https://code-lab1.tistory.com/217
- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ya3344&logNo=221395287263
- https://siahn95.tistory.com/entry/DB-%EC%9D%B8%EB%8D%B1%EC%8A%A4%EB%9E%80-2-%EA%B5%AC%EC%A1%B0-B-Tree-%EA%B3%84%EC%97%B4%EC%9D%84-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0
