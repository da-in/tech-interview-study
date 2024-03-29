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
 CREATE INDEX <인덱스명> ON <테이블명> ( 칼럼명1, 칼럼명2, ... );
 <br>과 같은 방식으로 인덱스를 생성할 수 있다.
B-Tree, Hash, Fractal, Merge-Tree 같은 여러 방식이 존재하지만, B-Tree 방식 인덱스만 주로 사용한다.



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

## B-Tree 인덱스
루트 노드, 브랜치 노드, 리프 노드로 이루어져 있다.
리프노드에는 실제 데이터에 접근할 수 있도록 주솟값을 가지고 있게 된다.
<img width="400" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/faf4b5ea-f6e6-49a0-9952-9e7df1baae30">



## 클러스터링 인덱스
클러스터링 인덱스는 프라이머리 키에만 적용되는 내용이다.
프라이머리 키 값이 비슷한 레코드들 끼리 묶어서 저장하는 것이 클러스터링 인덱스이다.
프라이머리 키 값에 의해 레코드의 물리적 저장 위치가 결졍되고, 프라이머리 키가 바뀌면 저장 위치도 바뀌게 된다.
클러스터링 테이블을 사용하는 데이터베이스 스토리지 엔진은 항상 클러스터링 인덱스로 테이블이 저장되기 때문에 프라이머리 키 기반 검색이 매우 빠르며, 대신 저장이 상대적으로 느리다.

## 논클러스터링 인덱스
클러스터링 인덱스의 반대되는 용어로, 대부분 사용자가 생성하는 인덱스를 뜻한다. 일반적으로 인덱스를 생성하면, 논클러스터링 인덱스로 생성된다.
주로 B-Tree 인덱스를 사용하게 되고 B-Tree 인덱스는 루트 노드, 브랜치 노드, 리프 노드로 이루어져 있다.
리프노드에는 실제 데이터에 접근할 수 있도록 주솟값을 가지고 있게 된다.
이 떄, 만약 데이터베이스 스토리지 엔진이 클러스터링 인덱스를 사용하는 엔진이면 논클러스터링 인덱스의 리프노드에 저장되는 값은 논리적인 주소값이다.
실제 데이터 레코드에 접근하기 위해서는 프라이머리 키가 저장된 인덱스를 한번 더 탐색해야 접근 가능하다.

클러스터링 인덱스를 사용하지 않는 스토리지 엔진이라면 실제 물리 주소를 가지고 있게 되므로 직접 접근하면 된다.

### 인덱스 레인지 스캔
검색해야 할 인덱스의 범위가 주어졌을 때 사용된다.
전체를 스캔하는 것이 아닌 범위만 스캔하게 된다.

스캔 후, 조건과 일치하는 레코드를 읽기 위해 랜덤 I/O가 일어난다. 랜덤 I/O는 비용이 많이 드는 작업이고, 만약 읽어야 하는 데이터 레코드가 20~25%를 넘어가면 인덱스보다 테이블 스캔이 효율적이다.

### 인덱스 풀 스캔
말 그대로 인덱스를 처음부터 끝까지 풀스캔 하는 방식이다.
인덱스의 크기가 테이블의 크기보다 작기 때문에 테이블을 풀스캔 하는것 보다는 효율적이지만, 인덱스 생성 의도와는 맞지 않는 방식.

## 다중 칼럼 인덱스
2개 이상의 칼럼을 포함하는 인덱스이다.
인덱스는 정렬되어 있기 때문에 다중 칼럼 인덱스도 정렬이 되어있다. 하지만 2개 이상의 칼럼을 갖고 있기 때문에, 첫번째 칼럼을 정렬하고, 두번째 칼럼은 첫번째 칼럼에 의존해서 정렬되어 있다. 

따라서 다중 칼럼 인덱스를 사용할 때에는 자주 사용하는 WHERE 절에 맞게 인덱스 조합 순서를 결정해야 한다.


## 커버링 인덱스

커버링 인덱스는 쿼리의 조건을 모두 충족하고 있는 인덱스를 뜻한다.

다음과 같은 인덱스를 갖고 있는 테이블에서
```
 CREATE INDEX test ON testdb ( age );
```

```
select * from test
where age = 30;
```

위의 쿼리를 다음과 같이 바꾸면

```
select age from user
where age = 30;
```
질의에 사용되는 모든 칼럼이 인덱스에 포함되어 있으므로, 데이터 테이블까지 접근하는 과정이 생략된다.

인덱스 레인지 스캔시 테이블 레코드에 최종적으로 접근하기 위해서는 데이터 수 만큼의 랜덤 I/O가 일어나는데, 커버링 인덱스를 이용하면 랜덤 I/O 과정이 생략되므로 성능이 향상되는 효과를 볼 수 있다.




## 출처
https://lalwr.blogspot.com/2016/02/db-index.html  
https://mangkyu.tistory.com/96  
