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

### Separate chaining(Open Hashing)

해시 충돌이 발생하면 새로운 공간을 할당해서 연결리스트 형태로 연결하여 저장한다.  
이러한 개방적 특성으로 개방 해싱(Open Hashing)이라고도 한다.

하지만 이는 키가 몰리는 경우, 키 내에서의 탐색을 위해 worst case로 O(n)의 시간복잡도를 가질 수 있다. 이를 해결하는 방법은 다음과 같다.

- 일정 적재율을 넘어서면 버킷의 크기를 동적으로 늘린다.
- 연결리스트가 아닌 비선형적 자료구조를 사용하여 저장한다. 이때 $O(logn)$의 Red-Black Tree 형태를 사용할 수 있다.

<img src="https://user-images.githubusercontent.com/66757141/209569742-f6642f8e-4383-4102-9c5e-7fbff62be191.png" alt="1280px-Hash_table_5_0_1_1_1_1_1_LL svg" width="500px"/>

### Open addressing(Closed Hashing)

해시 충돌이 발생하면 해시 테이블 내에서 주어진 조건에 따라 probing(탐사)하여 다음 버킷을 찾아 저장한다.  
주어진 해시 테이블 내에서 저장되는 특징으로 폐쇄 해싱(Closed Hashing) 이라고도 한다.

<img src="https://user-images.githubusercontent.com/66757141/209595178-a7ea3c2a-00e4-4fb2-bc2f-084bf1f8a341.png" alt="linear-and-quadratic-probing" width="500px"/>

- **Linear Probing(선형 탐사)**  
  기존 해시값에 1을 더하는 형태로 바로 다음 버킷을 탐색한다.  
   h(6) mod 5 = 7 mod 5 = 2 _충돌 가정_  
   h(6)+1 mod 5 = 8 mod 5 = 3 _저장, 또 충돌시 다음 탐색_

  선형 탐사법은 군집화의 문제를 가지고있다. 군집화란 충돌시 바로 다음 인덱스에 접근하기 때문에 충돌한 부분이 계속해서 길게 증가하는 것을 말하고, 해당 구간에서 선형탐색이 빈번하게 일어나게 된다.

- **Quadratic Probing(이차 탐사)**  
  선형탐사의 문제를 해결하기 위해 고안되었다. 1이 아닌 상수를 제곱한 값을 더하는 방식으로 군집화를 해결할 수 있다. 그러나 약한 군집화가 존재하고, bucket의 비어있는 공간이 있어도 찾지 못할 수 있다.

- **Double Hashing(이중 해싱)**  
  앞의 두 방법은 해시 충돌의 발생 시 일정한 규칙에 따라 인덱스를 증가시키기 때문에, 규칙에 따른 군집이 발생한다는 문제를 해결하지 못했다.

  이중 해싱은 충돌시 추가적인 해시 함수를 사용하여 해당 버킷에 저장하는 방식이다. 충돌시 h(key) + i\*J(key)의 형태로 탐색순서를 추가적으로 곱해주어 충돌 확률을 매우 낮출 수 있다.

  그러나 이는 추가적인 해시 함수를 사용하므로 함수의 성능이 해시 테이블 전체에 큰 영향을 주게된다.

<br/>

## Hash Table 시간복잡도

해시테이블은 key와 value가 1:1 쌍을 이루므로 삽입, 삭제, 검색 등의 과정에서 모두 평균적으로 **O(1)\* **의 시간복잡도를 갖는다.

엄밀하게는 아래의 worst case에서는 **O(n)** 의 시간복잡도를 갖을 수 있다.

- 너무 많은 요소들이 동일한 해시값으로 매핑될 경우, 동일한 인덱스에 대한 탐색을 하는데에 O(n)이 소요될 수 있다.
- 해시테이블이 로드밸런서를 이미 거쳤을 경우 rehash\*가 일어난다.

  _\* **rehash** 는 기존 HashTable 크기를 늘리고 새로이 데이터를 복사하는 과정._

그럼에도 평균적으로 **O(1)** 이라고 하는 이유는 아래와 같다.

- 좋은 해시 함수를 선택했고, 큰 로드밸런스를 필요로 하지 않는다면 많은 요소가 동일한 값으로 해싱되는 경우는 드물다.
- O(n)의 시간복잡도를 갖는 rehash 연산은, n/2회 이상의 O(1) 연산이 수행된 후에나 발생한다._(Java에서는 threshold가 기본 0.75, 즉 75% 이상 입력되었을 때 rehash가 실행된다.)_
  때문에 평균 시간복잡도를 구한다면 다음과 같은 형태가 된다.

  (k \* O(1) + n-k \* O(n)) / n = O(1)

<br/>

---

## Reference

📄https://you88.tistory.com/36  
📄https://en.wikipedia.org/  
📄https://go-coding.tistory.com/30  
📄https://galid1.tistory.com/170  
📄https://modeling-languages.com/robust-hashing-models/  
📄https://stackoverflow.com/questions/9214353/hash-table-runtime-complexity-insert-search-and-delete
