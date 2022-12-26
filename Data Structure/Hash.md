# Hash(해시)

해시 함수(hash function) 혹은 해시 알고리즘(hash algorithm)은 **임의의 길이의 데이터** 를 **고정된 길이의 데이터** 로 매핑하는 함수이며, 이를 해싱(hashing)한다고 한다.  
해시 함수에 의해 얻어지는 값을 `해시 값`, `해시 코드`, `해시 체크섬` 또는 간단하게 `해시`라고 한다.

<img src="https://user-images.githubusercontent.com/66757141/209565523-a7740995-1133-48db-90d4-110798930f96.png" alt="Hash_table_4_1_1_0_0_1_0_LL svg" width="500px"/>

<br/>

## Hash Table(해시 테이블)

해시 테이블(혹은 해시 맵)은 연관 배열이나 딕셔너리를 구현하는 자료구조이며, `키`를 `값`에 매핑 `key-value` 형태의 추상자료형(Abstract Data Type, ADT)이다.

해시테이블은 해시함수 통해 키를 매핑하여 얻은 해시 값을 인덱스로 사용한다. 그리고 데이터가 저장되는 곳을 `버킷`, `슬롯` 이라고 한다.

<br/>

## Hash Collision(해시 충돌)

해시 충돌은 서로 다른 키에 대하여 동일한 버킷이 할당되었을 경우, 즉 해시 함수에 의해 동일한 해시 값이 매핑되는 경우를 의미한다. 이는 해시 테이블의 특성에 위배되며 버킷 오버플로우\*를 발생시킬 수 있다.

_\* 버킷 오버플로우 - 버킷의 크기를 넘어서 저장_

이러한 해시 충돌에 대한 해결 방법은 아래와 같다.

#### Separate chaining

<br/>

## Hash Table 시간복잡도

해시테이블은 key와 value가 1:1 쌍을 이루므로 삽입, 삭제, 검색 등의 과정에서 모두 평균적으로 **O(1)\***의 시간복잡도를 갖는다.

엄밀하게는 아래의 worst case에서는 **O(n)** 의 시간복잡도를 갖을 수 있다.

- 너무 많은 요소들이 동일한 해시값으로 매핑될 경우, 추가적으로 살피는데 O(n)이 소요될 수 있다.
- 해시테이블이 로드밸런서를 이미 거쳤을 경우, it has to rehash [create a new bigger table, and re-insert each element to the table].

그럼에도 평균적으로 **O(1)** 이라고 하는 이유는 아래와 같다.

- 좋은 해시 함수를 선택했고, 큰 로드밸런스를 필요로 하지 않는다면 많은 요소가 동일한 값으로 해싱되는 경우는 드물다.
- The rehash operation, which is O(n), can at most happen after n/2 ops, which are all assumed O(1): Thus when you sum the average time per op, you get : (n\*O(1) + O(n)) / n) = O(1)

<img src="https://user-images.githubusercontent.com/66757141/209565531-841fcd27-814f-4982-8d30-0dc94619a5e8.png" alt="Hash_table_3_1_1_0_1_0_0_SP svg" width="500px"/>

<br/>

---

## Reference

📄https://ko.wikipedia.org/wiki/해시_함수  
📄https://en.wikipedia.org/wiki/Hash_table  
📄https://go-coding.tistory.com/30
