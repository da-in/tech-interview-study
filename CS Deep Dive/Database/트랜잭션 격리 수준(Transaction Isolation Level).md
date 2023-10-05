

## 트랜잭션 격리수준이 필요한 이유



<img width="600" alt="image"  src="https://github.com/da-in/tech-interview-study/assets/79582366/b2cbc4db-eee4-49ed-ade4-3e14dd861f2b">

Race Condition이 발생하므로 트랜잭션을 서로 격리해서 다른 트랜잭션이 영향을 주지 못하게 해야 한다.
<br/><br/><br/>
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/fab50897-8ee4-499a-998f-15e2cc96564f">


가장 쉬운 방법은 트랜잭션을 순서대로 실행하는 방법이다.
동시 접근 문제가 아예 없어지지만, 한 개의 트랜잭션만 처리하기 때문에 성능 저하가 일어난다.
따라서 상황에 따라서 격리수준을 선택해야 한다.
<br/><br/><br/>
**트랜잭션 격리수준(isolation level)** 이란 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것이다.

- 간단하게 말해 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것이다.
- 격리수준은 `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE` 의 4가지가 있다.
- 뒤로 갈수록 고립 정도가 높아지고 성능은 낮아진다.

<br/>

## 격리 수준에 따라 발생할 수 있는 문제

**1. Dirty Read**
- Dirty read를 막지 않은 경우

<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/f12e62e5-d0f2-4261-882c-fe7b9c32a4ef">

위와 같은 상황이 발생하면 읽지 않은 메세지는 존재하지만 읽지 않은 메세지의 수는 0이 되는 모순적인 상황이 발생한다.
<br/><br/>
- Dirty read를 막은 경우
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/f3d593e4-f8cb-4564-b82d-7449c9559106">

<br/>

**2. Dirty Write**

- Dirty Write를 막지 않은 경우
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/66371581-a277-459c-9ab1-01555437a275">
<br/><br/>

- Dirty Write를 막은 경우
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/53d711ba-ec80-4fb1-a8f8-d28fed4991f4">
<br/><br/>

Dirty Read/Write를 막지 않은 경우
- 트랜잭션 A의 커밋하기 이전 변경사항을 트랜잭션 B가 참조한다.
- 트랜잭션 A가 문제가 생겨 ROLLBACK을 해도 B는 계속 로직을 수행한다.
- 데이터 부정합이 발생한다.

<br/><br/><br/>

**3. Read Skew1**

- 트랜잭션 A가 같은 쿼리를 반복해서 수행하는 도중, 트랜잭션 B가 A의 실행에 사용하는 값을 변경한다.
- 트랜잭션 A가 같은 쿼리를 수행하는데에도 B에 의해 다른 결과가 나온다.
- 같은 쿼리문에 대해 일관된 결과값이 나와야하는 `REPEATABLE READ` 정합성을 만족하지 못한다.
- Dirty Read/Write를 막은것 만으로는 해결할 수 없다.
<br/><br/>
read skew 문제의 예시
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/0b18ae7c-916b-4864-bd02-ec41e20c3d92">
<br/><br/>

스냅숏 격리를 이용하여 해결한 경우

<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/d73a65ed-017e-4283-94f2-9656f6f7dac3">

<br/><br/>
<br/><br/>

**4. Lost Update**

- 같은 데이터를 쓸 때 발생한다.
  
<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/19fa7f5d-321d-4b6f-8937-c0d70797aa53">

<br/><br/>

명시적 잠금으로 해결한 경우

<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/3cc41c85-9295-4db8-9027-b07a7f9a7002">

<br/><br/>

CAS를 이용한 경우

<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/fc5727c6-8284-4ae9-a1a4-5e600083d56b">

<br/><br/><br/>

**5. Read Skew2**

- 같은 데이터를 쓰지 않지만 실제로는 경쟁 상태에 있다.
  
 <img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/5824c1ff-a6b6-4f6c-80eb-1fb59bfd618f">

ex) count쿼리의 값이 2이면 A,B 둘 중 하나를 수정하는 경우이다. 

<br/><br/>

인덱스 잠금을 이용해서 해결

<img width="600" alt="image" src="https://github.com/da-in/tech-interview-study/assets/79582366/6ab87c53-632b-49cc-af06-74246f0f7038">

<br/><br/><br/>


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
