# Hash(해시)

해시 함수(hash function) 혹은 해시 알고리즘(hash algorithm)은 **임의의 길이의 데이터** 를 **고정된 길이의 데이터** 로 매핑하는 함수이며, 이를 해싱(hashing)한다고 한다.  
해시 함수에 의해 얻어지는 값을 `해시 값`, `해시 코드`, `해시 체크섬` 또는 간단하게 `해시`라고 한다.

<img src="https://user-images.githubusercontent.com/66757141/209589990-cfc7e5dd-4276-464d-a36f-2a5137eab444.png" alt="hash" width="500px"/>

<br/>

## Hash Table(해시 테이블)

해시 테이블(혹은 해시 맵)은 연관 배열이나 딕셔너리를 구현하는 자료구조이며, `키`를 `값`에 매핑 `key-value` 형태의 추상자료형(Abstract Data Type, ADT)이다.

해시테이블은 해시함수 통해 키를 매핑하여 얻은 해시 값을 인덱스로 사용한다. 그리고 데이터가 저장되는 곳을 `버킷`, `슬롯` 이라고 한다.

<img src="https://user-images.githubusercontent.com/66757141/209565531-841fcd27-814f-4982-8d30-0dc94619a5e8.png" alt="Hash_table_3_1_1_0_1_0_0_SP svg" width="500px"/>

<br/>

## Hash Collision(해시 충돌)

해시 충돌은 서로 다른 키에 대하여 동일한 버킷이 할당되었을 경우, 즉 해시 함수에 의해 동일한 해시 값이 매핑되는 경우를 의미한다. 이는 해시 테이블의 특성에 위배되며 버킷 오버플로우\*를 발생시킬 수 있다.

_\* 버킷 오버플로우 - 버킷의 크기를 넘어서 저장_

<img src="https://user-images.githubusercontent.com/66757141/209569409-554034de-543d-4816-a3af-18b278f6fed4.png" alt="Hash_table_4_1_1_0_0_1_0_LL svg" width="500px"/>

이러한 해시 충돌에 대한 해결 방법은 아래와 같다.

#### Separate chaining(Open Hashing)

해시 충돌이 발생하면 새로운 공간을 할당해서 연결리스트 형태로 연결하여 저장한다. 이러한 개방적 특성으로 개방 해싱(Open Hashing)이라고도 한다.

<img src="https://user-images.githubusercontent.com/66757141/209569742-f6642f8e-4383-4102-9c5e-7fbff62be191.png" alt="1280px-Hash_table_5_0_1_1_1_1_1_LL svg" width="500px"/>

#### Open addressing(Closed Hashing)

해시 충돌이 발생하면 해시 테이블 내에서 주어진 조건에 따라 probing(탐색)하여 다음 버킷을 찾아 저장한다. 주어진 해시 테이블 내에서 저장되는 특징으로 폐쇄 해싱(Closed Hashing) 이라고도 한다.

<br/>

## Hash Table 시간복잡도

해시테이블은 key와 value가 1:1 쌍을 이루므로 삽입, 삭제, 검색 등의 과정에서 모두 평균적으로 **O(1)\***의 시간복잡도를 갖는다.

엄밀하게는 아래의 worst case에서는 **O(n)** 의 시간복잡도를 갖을 수 있다.

- 너무 많은 요소들이 동일한 해시값으로 매핑될 경우, 동일한 인덱스에 대한 탐색을 하는데에 O(n)이 소요될 수 있다.
- 해시테이블이 로드밸런서를 이미 거쳤을 경우, it has to rehash [create a new bigger table, and re-insert each element to the table].

그럼에도 평균적으로 **O(1)** 이라고 하는 이유는 아래와 같다.

- 좋은 해시 함수를 선택했고, 큰 로드밸런스를 필요로 하지 않는다면 많은 요소가 동일한 값으로 해싱되는 경우는 드물다.
- The rehash operation, which is O(n), can at most happen after n/2 ops, which are all assumed O(1): Thus when you sum the average time per op, you get : (n\*O(1) + O(n)) / n) = O(1)

<br/>

---

## Reference

📄https://ko.wikipedia.org/wiki/해시_함수  
📄https://en.wikipedia.org/wiki/Hash_table  
📄https://en.wikipedia.org/wiki/https://en.wikipedia.org/wiki/Hash_collision  
📄https://en.wikipedia.org/wiki/Open_addressing  
📄https://go-coding.tistory.com/30  
📄https://galid1.tistory.com/170  
📄https://modeling-languages.com/robust-hashing-models/
