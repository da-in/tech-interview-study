# 인덱스(Index)
### Index란?  
DB에서 Index는 Table에 어떤 데이터가 어디에 위치하였는지 위치 정보를 가진 주소록의 개념을 가진다.  
Table의 컬럼을 색인화하여 풀스캔 하는 것이 아니라 색인화 되어있는 Index 파일을 검색하여 속도를 빠르게 하는 도구이다.  
Index는 Tree 구조로 색인화를 진행한다. (MySQL에서는 B+Tree 사용)


### Index 장점
- 키 값을 기초로 하여 테이블에서 검색과 정렬 속도를 향상시킨다.
- 전반적인 시스템의 부하를 줄일 수 있다.

### Index 단점
- 인덱스를 만들면 .mdb파일의 크기가 커진다.  
    > .mdb파일 - Microsoft Database를 나타내는 Microsoft Access Database 파일
- 여러 사용자 응용 프로그램에서의 여러 사용자가 한 페이지를 동시에 수정 할 수 있는 병행성이 줄어든다.
- 인덱스 된 필드에서 데이터를 업데이트하거나, 레코드를 추가 또는 삭제할 때 성능이 떨어진다.
- 인덱스가 데이터베이스 공간을 차지해 추가적인 공간이 필요해진다.(약 DB의 10%내외의 공간 필요)

*즉, Index를 사용할 지에 대한 결정은 미리 시험을 해보고 결정하는 것이 가장 좋다.*


### Index를 사용하면 좋은 경우
- 규모가 작지 않은 테이블

- INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼

- JOIN이나 WHERE 또는 ORDER BY에 자주 사용되는 컬럼

- 데이터의 중복도가 낮은 컬럼
### Index를 지양해야 하는 경우
- 데이터의 중복도가 높은 열은 인덱스로 만들어도 효용이 없다.  
(성별같이 타입이 별로 없는 경우 등)

- DML(INSERT, UPDATE, DELETE)이 자주 일어나는 경우  
(인덱스는 SELECT쿼리의 검색속도를 빠르게 하는데에 목적이 있으므로, 이외의 쿼리에서는 느려진다.)

>SELECT쿼리 경우에도 데이터 블록 수, 분포도 등에 따라 인덱스가 빠를수도 있고, 풀스캔보다 느려질 수도 있다.

### DML(Data Manipulation Language)에 취약하다.
**INSERT**  
기존 Block에 여유가 없을 때, 새로운 Data가 입력된다.

→ 새로운 Block을 할당 받은 후, Key를 옮기는 작업을 수행한다.

→ Index split 작업 동안, 해당 Block의 Key 값에 대해서 DML이 블로킹 된다. (대기 이벤트 발생)

성능면에서 매우 불리하다.

**DELETE**  

테이블에서 데이터가 DELETE 될 경우 - 지워지고 다른 데이터가 그 공간을 사용할 수 있음  

Index에서 데이터가 DELETE 될 경우 - 데이터가 지워지지 않고, 사용 안 됨 표시만 함 

즉, 테이블에서 데이터가 1만건이 있는 경우, 인덱스에는 2만건이 있을 수 있다는 뜻  

이런 경우 인덱스를 사용해도 수행속도를 기대하기 힘들다.

**UPDATE**

테이블에 UPDATE가 발생할 경우 인덱스에서는 DELETE가 먼저 발생한 후 새로운 작업의 INSERT 작업이 발생한다. 

DELETE와 INSERT 두 개의 작업이 인덱스에 동시에 발생 하여 다른 DML보다 더 큰 부하를 주어 성능을 저하시킨다.


### Index 생성 방법
- PK (Auto-Increasement)
- Unique제약을 정의할 경우 Unique Index


### 인덱스 종류

- 고유 인덱스(Unique Index)
    - 유일한 값을 갖는 컬럼에 대해서 생성하는 인덱스로, Unique 옵션을 지정해야 한다.
- 비고유 인덱스(NONUnique Index)
    - 고유 인덱스와 반대
- 단일 인덱스(Single Index)
    - 한 개의 컬럼으로 구성한 인덱스
- 결합 인덱스(Composite Index)
    - 두 개 이상의 컬럼으로 인덱스를 구성하는 것을 말한다. 예를들어 부서번호와 부서명을 결합하여 인덱스를 설정하는 것과 같다.
- 함수 기반 인덱스(Function Based Index)
    - 컬럼에 어떠한 산술식을 수행했을 때의 인덱스이다.

## 출처
https://lalwr.blogspot.com/2016/02/db-index.html  
https://mangkyu.tistory.com/96  