# Hash(해시)

- 해시 함수(hash function)는 **임의의 길이의 데이터** 를 **고정된 길이의 데이터** 로 매핑하는 함수이며, 이 과정을 **해싱(hashing)** 한다고 한다.  
- 즉, **Hash(해시)** 는 입력 데이터를 해쉬 함수에 의해 고정된 길이의 데이터로 변환된 값이다.

>`해시 값`, `해시 코드`, `해시 체크섬`이라고도 한다.

</br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcluEM%2FbtryF769jdT%2FtldrkmqK9arIia8rGKH5e0%2Fimg.png" alt="hash" width="500px"/>

<br/>

## Hash Table(해시 테이블)

- 해시 테이블(혹은 해시 맵)은 `키`를 `값`에 매핑하는 `key-value` 형태의 자료구조이다.
- 해시 테이블은 해시 함수를 통해 키를 매핑하여 얻은 해시 값을 인덱스로 사용한다.
- 그리고 데이터가 저장되는 곳을 `버킷`, `슬롯` 이라고 한다.

> 버킷(bucket) : 하나의 주소를 갖는 파일의 한 구역으로 버킷의 크기는 같은 주소에 포함될 수 있는 레코드 수를 의미한다.   
> 슬롯(slot) : 한 개의 레코드를 저장할 수 있는 공간으로 한 버킷 안에 여러 개의 슬롯이 있다.

</br>

<img src="https://user-images.githubusercontent.com/66757141/209565531-841fcd27-814f-4982-8d30-0dc94619a5e8.png" alt="Hash_table_3_1_1_0_1_0_0_SP svg" width="450px"/>

<br/>

## Hash Collision(해시 충돌)

- 해시 충돌은 서로 다른 키에 대하여 동일한 버킷에 할당 되었을 경우, 즉 해시 함수에 의해 동일한 해시 값이 매핑되는 경우를 의미한다.
- 이는 해시 테이블의 특성에 위배되며, 버킷 오버플로우\*를 발생시킬 수 있다.
- 해시 충돌이 발생하는 이유는 크게 두가지이다.
  - 해시 함수의 성는이 좋지 못한 경우
  - 저장되는 데이터의 양이 해시 테이블의 크기보다 큰 경우

</br>

  > 버킷 오버플로우 :  버킷의 크기를 넘어서 저장하는 것이다.

<img src="https://user-images.githubusercontent.com/66757141/209569409-554034de-543d-4816-a3af-18b278f6fed4.png" alt="Hash_table_4_1_1_0_0_1_0_LL svg" width="450px"/>

</br>

## Hash Collision(해시 충돌) 해결 방법

### Separate chaining (Open Hashing)

- 해시 충돌이 발생하면 새로운 공간을 할당해서 연결리스트 형태로 연결하여 저장한다.  
- 이러한 개방적 특성으로 개방 해싱(Open Hashing)이라고도 한다.
- 하지만 이는 매핑된 값이 한 곳에 몰리는 경우, 탐색을 위해 최대 `O(N)`의 시간복잡도를 가질 수 있다. 해결 방법은 두가지가 있다. 
  - 일정 적재율을 넘어서면 버킷의 크기를 동적으로 늘린다.
  - 연결리스트가 아닌 비선형적 자료구조를 사용하여 저장한다. 이때 `O(logn)`의 `Red-Black Tree` 자료구조를 사용할 수 있다.

<img src="https://user-images.githubusercontent.com/66757141/209569742-f6642f8e-4383-4102-9c5e-7fbff62be191.png" alt="1280px-Hash_table_5_0_1_1_1_1_1_LL svg" width="450px"/>

</br>

### Open addressing( Closed Hashing)

- 해시 충돌이 발생하면 해시 테이블 내에서 주어진 조건에 따라 **probing(탐사)** 하여 다음 버킷을 찾아 저장한다.  
- 공간을 늘리지 않고, 주어진 해시 테이블 내에서 저장되므로 **폐쇄 해싱(Closed Hashing)** 이라고도 한다.
- 크게 3가지 방법이 존재한다.

<img src="https://user-images.githubusercontent.com/66757141/209595178-a7ea3c2a-00e4-4fb2-bc2f-084bf1f8a341.png" alt="linear-and-quadratic-probing" width="480px"/>

</br>

**1. Linear Probing(선형 탐사)**  
  - 기존 해시 값에 `1`을 더하는 형태로 바로 다음 버킷을 탐색한다.
  - 즉, 해시 주소(index)의 다음 주소(index)부터 차례대로 맨 처음까지 순회하며 빈 공간을 찾는 방식
  - 선형 탐사법은 군집화의 문제를 가지고 있다.

  > 군집화란 충돌시 바로 다음 인덱스에 접근하기 때문에 충돌한 부분이 계속해서 길게 증가하는 것을 말한다.
  > 해당 구간에서 선형탐색이 빈번하게 일어나게 된다.

</br>

**2. Quadratic Probing(이차 탐사)**  
  - 선형 탐사의 문제를 해결하기 위해 고안되었다.
  - `1`이 아닌 상수를 제곱한 값을 더하는 방식으로 군집화 문제를 해결한다.
  - 하지만 약한 군집화가 존재하고, 버켓의 비어있는 공간이 있어도 찾지 못할 수 있는 단점이 존재한다.

</br>

**3. Double Hashing(이중 해싱)**  
  - 앞의 두 방법은 해시 충돌의 발생 시 일정한 규칙에 따라 인덱스를 증가시키기 때문에, 규칙에 따른 군집화 문제를 해결하지 못한다.
  - **이중 해싱**은 충돌시 **추가적인 해시 함수**를 사용하여 해당 버킷에 저장하는 방식이다.
  - 충돌시 `h(key) + i*J(key)`의 형태로 탐색 순서를 추가적으로 곱해 충돌 확률을 매우 낮출 수 있다.
  - 그러나 추가적인 해시 함수를 사용하므로 함수의 성능이 해시 테이블 전체에 큰 영향을 준다.

<br/>

## Hash Table 시간복잡도

- 해시 테이블은 `key-value`가 `1:1` 쌍을 이루므로 삽입, 삭제, 검색 등의 과정에서 모두 평균적으로 `O(1)`의 시간복잡도를 갖는다.
- 하지만 너무 많은 키들이 동일한 해시 값으로 매핑될 경우, 동일한 인덱스에 대한 탐색 과정에서 최대 `O(N)`이 소요될 수 있다.
- 해시 테이블이 로드밸런서를 이미 거쳤을 경우 rehash\* 연산이 일어난다.
- 그럼에도 평균적으로 **O(1)** 이라고 하는 이유는 아래와 같다.
  - 좋은 해시 함수를 선택하고, 큰 로드밸런스를 필요로 하지 않는다면 많은 키가 동일한 값으로 해싱되는 경우는 드물다.
  - `O(N)`의 시간복잡도를 갖는 rehash 연산은, `N/2`회 이상의 `O(1)` 연산이 수행된 후에나 발생한다.
  - 따라서 평균 시간복잡도는 `(k * O(1) + (n-k) * O(N)) / N = O(1)` 같은 형태가 된다.

</br>

> **rehash** : 기존 해시 테이블의 크기를 늘리고 새롭게 데이터를 복사하는 과정이다.

<br/>

---

## Reference

📄https://you88.tistory.com/36  
📄https://en.wikipedia.org/  
📄https://go-coding.tistory.com/30  
📄https://galid1.tistory.com/170  
📄https://modeling-languages.com/robust-hashing-models/  
📄https://stackoverflow.com/questions/9214353/hash-table-runtime-complexity-insert-search-and-delete  
📄https://kang-james.tistory.com/136
