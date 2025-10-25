# 트랜잭션 격리 수준(Transaction Isolation Level)

**트랜잭션 격리수준(isolation level)** 이란 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것이다.

- 간단하게 말해 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것이다.
- 격리수준은 `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE` 의 4가지가 있다.
- 뒤로 갈수록 고립 정도가 높아지고 성능은 낮아진다.

<br/>

## 격리 수준에 따라 발생할 수 있는 문제

**1. Dirty Read**

- 트랜잭션 A의 커밋하기 이전 변경사항을 트랜잭션 B가 참조한다.
- 트랜잭션 A가 문제가 생겨 ROLLBACK을 해도 B는 계속 로직을 수행한다.
- 데이터 부정합이 발생한다.

**2. Dirty Write**

**3. Read Skew1**

- 트랜잭션 A가 같은 쿼리를 반복해서 수행하는 도중, 트랜잭션 B가 A의 실행에 사용하는 값을 변경한다.
- 트랜잭션 A가 같은 쿼리를 수행하는데에도 B에 의해 다른 결과가 나온다.
- 같은 쿼리문에 대해 일관된 결과값이 나와야하는 `REPEATABLE READ` 정합성을 만족하지 못한다.

**4. Lost Update**

- 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했는데, 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상이다.

**5. Read Skew2**



<br/>

## 4가지 격리 수준

**1. READ UNCOMMITTED**

- 트랜잭션의 변경 내용을 `COMMIT`이나 `ROLLBACK`과 상관없이 다른 트랜잭션에서 볼 수 있다.
- `Dirty Read`, `NON-REPETABLE READ`, `Phantom Read` 문제가 발생할 수 있다.
- RDBMS에서는 표준으로 인정하지 않는다.

**2. READ COMMITTED**

- 어떤 트랜잭션의 변경 내용이 `COMMIT` 되어야만 다른 트랜잭션에서 조회할 수 있다.
- 오라클 DBMS에서 기본으로 사용하고 있고, 온라인 서비스에서 가장 많이 선택되는 격리수준이다.
- `NON-REPETABLE READ`, `Phantom Read` 문제가 발생할 수 있다.

**3. REPEATABLE READ**

- 트랜잭션이 시작되기 이전에 커밋된 내용에 대해서만 조회할 수 있는 격리수준이다.
- MySQL DBMS에서 기본으로 사용하고 있다.
- 트랜잭션 수행 시간에 따른 멀티 버전을 관리해야 하는 단점이 있다.
- `Phantom Read` 부정합이 발생할 수 있다.

**4. SERIALIZABLE**

- 가장 엄격한 격리 수준이다.
- 트랜잭션이 완료될 때까지 `SELECT` 문장이 사용하는 모든 데이터에 공유잠금`(Shared Lock)`이 걸린다.
- 다른 트랜잭션에서는 해당 데이터에 대한 수정 및 입력이 불가능하다.
- 동시 처리 능력이 다른 격리수준보다 떨어지고, 성능 저하가 발생한다.

---

## Reference

📄 https://joont92.github.io/db/트랜잭션-격리-수준-isolation-level/  
📄 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md
