# 조인(JOIN)

- JOIN은 데이터베이스에서 **두 개 이상의 테이블**을 연결하여 **하나의 결과의 테이블**로 만드는 것을 의미하며 이를 통해 데이터를 효율적으로 검색하고 처리하도록 한다.
- JOIN을 사용하는 이유는 데이터베이스에서 테이블을 분리하여 ‘데이터 중복을 최소화’하고 ‘데이터의 일관성’을 유지하기 위함이다.
- 대표적으로 INNER JOIN, OUTER JOIN 등이 있다.

</br>

## JOIN의 종류

- INNER JOIN
- OUTER JOIN
  - LEFT OUTER JOIN
  - RIGHT OUTER JOIN
  - FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

<p align="center">
  <img src="https://user-images.githubusercontent.com/66757141/208731520-fc274729-7dfc-48a2-9ace-c4e568ba751e.jpg" alt="Visual_SQL_JOINS_orig" width="400px"/>
<p/>

<br/>

## INNER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208737969-3bc5524e-b23f-499f-8541-4621250fb91e.png" alt="INNER_JOIN" width="180px"/>

- 교집합의 개념이다.
- JOIN의 종류를 별도로 지정해주지 않았을 경우 `INNER JOIN` 방식이 기본적으로 사용된다.
- 기준 테이블과 join 테이블의 중복된 값을 보여준다.
- 명시적 조인 표현(explicit)과 암시적 조인 표현(implicit)이 있다.

_(지정한 열의 데이터가 두 테이블에 모두 존재할 때 JOIN)_

- 명시적 조인 표현
```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP;
```

- 암시적 조인 표현
```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, JOIN_TABLE B
WHERE A.NO_EMP = B.NO_EMP;
```
</br>

## LEFT OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738055-ca9ca9c0-4d64-4fb2-aacc-6fcac2183a02.png" alt="LEFT_JOIN" width="180px" />

- 왼쪽 테이블을 기준 테이블로 설정하여 JOIN이 이루어진다.
- 기준 테이블의 모든 값이 출력되고, 오른쪽인 조인 테이블에만 존재하는 값은 출력되지 않는다.  
- 기준 테이블에는 존재하는데 조인 테이블에는 존재하지 않는 데이터의 경우 조인 테이블의 속성 값이 NULL이 된다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

</br>

> **사례 1. 게시물 테이블(테이블 A)에서 해당 게시물의 사진 데이터(테이블 B)를 조회**  
> 게시물들은 사진이 존재하는 게시물들도 있지만 사진이 없는 게시물들 역시 존재하므로 B에서 불러오는 데이터의 값이 없을 수도 있다.
> 사진이 없는(B테이블에 데이터가 없는) 게시물도 같이 불러와야 하므로 left join을 사용한다.  
> 평소처럼 Inner Join을 사용하게 되면, 사진이 없는 게시물은 불러와지지 않게 된다.

> **사례 2. 게시물 테이블(테이블 A)에서 사진 데이터(테이블 B)가 없는 게시물만 조회**  
> 사용 예시1과 동일한 상황에서 사진이 없는 게시물들만 불러오는 경우는 아래 사진과 같으며, 다음과 같이 쿼리를 작성할 수 있다.

<img width="180" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/5639bceb-f1fc-4271-998b-5b3b24cc1ef9" >


```sql
SELECT *
FROM
	A left join B
    on A.postId = B.postId
WHERE B.postId IS NULL;
```

</br>

## RIGHT OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738091-c01277ef-59d5-4fe2-9dd2-5b392f282789.png" alt="RIGHT_JOIN" width="180px" />

- LEFT OUTER JOIN과 동일한 동작을 하며, 오른쪽 테이블을 기준 테이블로 설정하여 JOIN이 이루어진다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

</br>

## FULL OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738130-fc842d97-527a-4dc2-81dc-bc7dbcbde3c6.png" alt="FULL_OUTER_JOIN" width="180px" />

- 합집합의 개념으로 왼쪽과 오른쪽 테이블의 모든 데이터가 선택된다. 

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

> 모든 RDBMS에서 지원하진 않는다.
> 예를들어 MYSQL에서는 `FULL OUTER JOIN`를 지원하지 않아서 `RIGHT JOIN`과 `LEFT JOIN`을 합한 것으로 쿼리를 작성해야한다.

</br>

## CROSS JOIN

- 두 테이블의 모든 행을 조인시켜 생길 수 있는 모든 경우의 수를 표현해주는 방식이다.
- CROSS JOIN의 결과는 **두 테이블의 행의 개수의 곱** 만큼의 데이터를 갖는다.
- 카티션 곱(CARTESIAN PRODUCT)라고도 한다.

> Table A의 행이 3개, B가 4개이면 총 3\*4 = 12개의 데이터가 검색된다.

</br>

<img src="https://user-images.githubusercontent.com/66757141/208748788-ff23dd11-2461-4602-a8e8-e8d258811896.png" alt="CROSS_JOIN" width="200px" />

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

</br>

## SELF JOIN

- 1개의 테이블을 사용하여 자기자신과 조인하는 것이다.
- 자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.  
- 별도의 SELF JOIN 연산이 있는 것이 아니라, INNER JOIN, OUTER JOIN 등에서 대상이 되는 두 테이블을 자기 자신으로 조인하는 경우 SELF JOIN이 된다.

</br>

<img src="https://user-images.githubusercontent.com/66757141/208748797-7a0742c5-44c1-4933-919e-5638c8dc7b18.png" alt="SELF_JOIN" width="200px" />

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```

### 사용 예시
학생 테이블에 (학교, 학년, 나이) 칼럼이 존재하고, 같은 학교 같은 학년에 다니는 학생들의 나이를 비교하고 싶은 경우, 학교와 학년을 기준으로 SELF JOIN을 이용한다.

<br/>

----

## Reference

생활코딩 유튜브에서 데이터 예시를 기반으로 정말 잘 설명해줍니다!  
▶️ https://www.youtube.com/watch?v=pJqBR2TNe24

📄https://advenoh.tistory.com/23  
📄https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins  
📄https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md  
📄https://coding-factory.tistory.com/87  
📄https://parkmuhyeun.github.io/etc/database/2022-06-27-Join/
