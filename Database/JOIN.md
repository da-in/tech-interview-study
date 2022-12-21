# 조인(JOIN)

관계형 데이터베이스(RDBMS)에서는 중복 데이터를 피하기 위해서 데이터를 여러 테이블로 나누어 저장한다. 반대로 이러한 데이터베이스에서 원하는 결과를 도출하기 위해 테이블을 조합하게 된다.

관계형 데이터베이스에서는 조인(JOIN) 연산을 사용해 두 개의 이상의 테이블을 합쳐 SELECT 한다. 조인에는 여러 종류가 있다.

## SQL JOIN의 종류

- INNER JOIN
- OUTER JOIN
  - LEFT OUTER JOIN
  - RIGHT OUTER JOIN
  - FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

<p align="center">
  <img src="https://user-images.githubusercontent.com/66757141/208731520-fc274729-7dfc-48a2-9ace-c4e568ba751e.jpg" alt="Visual_SQL_JOINS_orig" width="500px"/>
<p/>

<br/>

## INNER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208737969-3bc5524e-b23f-499f-8541-4621250fb91e.png" alt="INNER_JOIN" width="180px"/>

교집합의 개념이다. JOIN의 종류를 별도로 지정해주지 않았을 경우 INNER JOIN이 Default로 사용된다. 기준 테이블과 join 테이블의 중복된 값을 보여준다.  
_(지정한 열의 데이터가 두 테이블에 모두 존재할 때 JOIN)_

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## LEFT OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738055-ca9ca9c0-4d64-4fb2-aacc-6fcac2183a02.png" alt="LEFT_JOIN" width="180px" />

왼쪽테이블 기준으로 JOIN이 된다. 기준테이블의 모든 값이 출력되고, 조인테이블에만 존재하는 값은 출력되지 않는다.  
기준테이블에는 존재하는데 조인테이블에는 존재하지 않는 데이터의 경우 조인테이블의 속성 값이 NULL이 된다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## RIGHT OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738091-c01277ef-59d5-4fe2-9dd2-5b392f282789.png" alt="RIGHT_JOIN" width="180px" />

LEFT OUTER JOIN과 동일한 동작을 하며, 오른쪽 테이블을 기준으로 JOIN 된다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## FULL OUTER JOIN

<img src="https://user-images.githubusercontent.com/66757141/208738130-fc842d97-527a-4dc2-81dc-bc7dbcbde3c6.png" alt="FULL_OUTER_JOIN" width="180px" />

합집합의 개념이다. 왼쪽과 오른쪽 테이블의 모든 데이터가 선택된다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## CROSS JOIN

두 테이블의 모든 행을 조인시켜 모든 경우의 수를 전부 표현해주는 방식이다. CROSS JOIN의 결과는 `두 테이블의 행의 개수의 곱` 만큼의 데이터를 갖는다.

카티션 곱(CARTESIAN PRODUCT)라고도 한다.

> Table A의 행이 3개, B가 4개이면 총 3\*4 = 12개의 데이터가 검색된다.

<img src="https://user-images.githubusercontent.com/66757141/208748788-ff23dd11-2461-4602-a8e8-e8d258811896.png" alt="CROSS_JOIN" width="200px" />

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

## SELF JOIN

1개의 테이블을 사용하여 자기자신과 조인하는 것이다.
자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.  
별도의 SELF JOIN 연산이 있는 것이 아니라, INNER JOIN, OUTER JOIN 등에서 두 대상을 자기 자신으로 조인하는 경우가 SELF JOIN이 된다.

<img src="https://user-images.githubusercontent.com/66757141/208748797-7a0742c5-44c1-4933-919e-5638c8dc7b18.png" alt="SELF_JOIN" width="200px" />

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```

<br/>

---

## Reference

생활코딩 유튜브에서 데이터 예시를 기반으로 정말 잘 설명해줍니다!  
▶️ https://www.youtube.com/watch?v=pJqBR2TNe24

📄https://advenoh.tistory.com/23  
📄https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins  
📄https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md  
📄https://coding-factory.tistory.com/87
