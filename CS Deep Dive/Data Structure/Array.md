# 배열 (Array)
배열은 연속된 메모리 공간에 순차적으로 저장된 데이터 모음이다.
- 배열을 구성하는 각각의 값을 요소(element)
- 배열에서의 위치를 가리키는 숫자는 인덱스(index) : 인덱스는 0부터 시작

## 특징
- 배열은 값의 중복을 허용하는 자료형
- 배열의 모든 원소들은 동일한 Type
- 연속된 메모리 공간에 데이터를 저장
  - 낭비되는 공간이 거의 없음
  - 데이터에 순서가 있으며, indexing 및 slicing이 가능함.

## 장단점
### 장점
- 인덱스를 사용해서 무작위 접근이 가능하여 검색 성능이 빠르다.<br/>
  인덱스를 활용해서 접근하기 때문에 접근성이 매우 높다.
- 순차 접근이 연결리스트보다 빠르다.<br/>
  배열은 주소가 순차적으로 나열되어 있기 때문에 접근성이 매우 높다 (바로 옆칸 뒤지면 되니까)
- 추가적인 메모리 할당이 필요 없다.<br/>
  할당된 메모리만 사용하므로 추가적인 메모리 사용이 없다.

### 단점
- 메모리를 처음에 할당하면 이후 크기를 바꿀 수 없다.<br/>
  사용하지 않는 공간이라도 해당 메모리 공간을 차지하고 있어 메모리가 낭비될 수 있다.
- 자료 삽입 삭제가 어렵다. <br/>
  삽입 삭제를 위해 당기거나 뒤로 미는 작업이 필요하기 때문에! 복잡도 O(n)
- 메모리를 재사용 할 수 없다. <br/>
  포인터로 구성되어있는 구조라면 해당 메모리를 해제하여 재활용할 수 있지만, 배열은 안됨.

## 배열의 시간 복잡도
| Operation | average case | worst case |
| :-------  |:--: |:--: |
| read      |O(1) |O(1)|
| insert    |O(n) |O(n)|
| delete    |O(n) |O(n)|
| search    |O(n) |O(n)|


## 배열(Array)의 기초 메소드
※자바스크립트 기준으로 작성합니다.
- arr.length : 배열의 길이를 출력 (※ 주의! 이건 속성임!)
- Array.isArray() : 인자 안에 들어간 변수, 데이터, 특정 값이 배열이면 true, 아니면 false
- arr.indexOf() : 배열에 해당 데이터가 있는 index 번호를 반환, 없으면 -1 반환
- arr.includes() : 배열에 해당 데이터가 있으면 true, 없으면 false
- arr.slice(start, end) : start 부터 end-1까지 슬라이싱 (start만 주면 끝까지)
- arr.unshift() : 배열의 맨 앞에 요소 추가
- arr.shift() : 배열의 맨 앞에 index 삭제 
- arr.push() : 배열의 맨 뒤에 element 추가
- arr.pop() : 배열의 맨 뒤에 index 삭제
- string.split() : 문자열을 split의 인자로 구분하여 배열로 변경
- arr.join() : 문자열 요소를 가지는 배열을 join의 인자로 구분하여 문자열로 변경 

## Reference
- https://hanamon.kr/javascript-%EB%B0%B0%EC%97%B4-%EA%B8%B0%EC%B4%88/
- https://yoongrammer.tistory.com/43
- https://cocodding0723.github.io/datastructure/02_array-post/
