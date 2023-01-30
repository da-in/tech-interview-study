# 트랜잭션(Transaction)

> 데이터베이스 트랜잭션(Database Transaction)은 데이터베이스 관리 시스템 또는 유사한 시스템에서 상호작용의 단위이다. 어떤 시스템들에서는 트랜잭션들은 논리적 작업 단위(LUW, Logical Units of Work)로 불린다.

**트랜잭션(Transaction)**

- 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위
- 한꺼번에 모두 수행되어야 할 일련의 연산
- 장애가 발생했을 때 복구하는 작업의 단위

\* **데이터베이스의 상태를 변화** 시킨다는 것은 `SELECT`, `INSERT`, `DELETE`, `UPDATE` 등의 `SQL 질의어`를 사용하여 데이터베이스에 접근하는 것을 의미한다.

```sql
BEGIN TRANSACTION [ {transaction_name | @tran_name_variable }
BEGIN TRAN
UPDATE Person
SET    Lastname = 'Lucky',
        Firstname = 'Luke'
WHERE  PersonID = 1
SELECT @@TRANCOUNT AS OpenTransactions
COMMIT TRAN
```

<br/>

## 트랜잭션 사용 이유

- 트랜잭션은 **데이터 부정합** 을 방지하기 위해 사용한다.
- **데이터 부정합** 이란 다수의 클라이언트 접근 혹은 데이터 변경 과정에서의 중단 등으로 데이터 깂이 다른 경우를 말한다.
- 한 번에 하나의 프로세스만 처리하면 데이터부정합을 방지할 수 있지만 이는 효율이 좋지 않으며 트랜잭션이 필요한 것이다.

<br/>

## 트랜잭션의 특징(ACID)

이론적으로 데이터베이스 시스템은 각각의 트랜잭션에 대해 `원자성(Atomicity)`, `일관성(Consistency)`, `독립성(Isolation)`, `영구성(Durability)`을 보장한다. 첫 글자를 따 ACID라 부른다. 그러나, 실제로는 성능향상을 위해 이런 특성들이 종종 완화되곤 한다.

- **원자성(Atomicity)**
  - 트랜잭션의 명령을 부분적으로 실행되거나 중단되지 않는 것을 보장한다.
  - 트랜잭션 내의 모든 명령이 완벽히 수행되거나, 어느 하나라도 오류가 발생하면 트랜잭션 전부가 취소되어야한다.
- **일관성(Consistency)**
  - 트랜잭션이 성공적으로 완료되면 언제나 일관성 있는 데이터베이스 상태를 유지하는 것이다.
  - 트랜잭션 수행 전과 후의 데이터 타입 등 시스템 고정 요소의 상태가 같아야 한다.
- **독립성(Isolation)**
  - 둘 이상의 트랜잭션이 동시에 실행되는 경우 서로 간섭할 수 없고, 수행 결과를 참조할 수도 없다.
  - `트랜잭션 격리수준(Transaction Isolation Level)`에 따라 수행 결과 참조 가능 여부가 달라진다.
- **영구성(Durability)**
  - 성공적으로 완료된 트랜잭션의 결과는 영구적으로 반영된다.

<br/>

## TCL(Transaction Control Language) 트랜잭션 연산

<img src="https://user-images.githubusercontent.com/66757141/215517220-22b7971a-549a-4d0f-891e-e61d0515c84b.png" alt="rollbackin-sql" width="700px">

[_img reference_](https://www.scaler.com/topics/Rollback-in-sql/)

- **커밋(Commit)**
  - 모든 작업들을 정상적으로 처리했다고 확정하는 명령어이다.
  - 처리 과정을 데이터베이스에 영구적으로 저장한다.
  - 커밋 이후 트랜잭션이 종료된다.
- **롤백(Rollback)**
  - 작업 중 문제 발생으로 인해 트랜젝션의 처리 과정에서 발생한 변경사항을 취소한다.
  - 트랜잭션이 시작되기 이전의 마지막 커밋 시점으로 돌아간다.
  - 롤백 이후 해당 트랜잭션을 재시작하거나 폐기한다.
- **세이브포인트(Savepoint)**

  - 임시저장으로 트랜잭션을 작게 분할하도록 한다.
  - 여러 SQL문을 실행하는 트랜잭션의 중간 단계에 사용자가 지정 가능하다.

    ```sql
    -- Create Savepoint
    SAVE TRANSACTION savepoint_name ;
    -- Rollback To Savepoint
    ROLLBACK TRANSACTION savepoint_name ;
    ```

<br/>

## 트랜잭션 상태

<img src="https://user-images.githubusercontent.com/66757141/215512756-c09312c9-3180-4048-bd30-979c9fadf704.png" alt="database-transaction-2" width="900px">

- **활성화(Active)**
  - 트랜잭션의 실행중인 첫 상태이다.
  - 트랜잭션은 해당 명령(읽기 또는 쓰기 작업)이 수행되는 한 활성화되어있다.
- **부분 완료(Partially committed)**
  - 변경이 실행되었지만 데이터베이스가 아직 디스크에서 변경 내용을 적용하지 않은 상태이다.
  - 이 상태에서는 데이터가 메모리 버퍼에 저장되어있고 버퍼가 아직 디스크에 기록되지 않았다.
- **완료(Committed)**
  - 모든 트랜잭션의 업데이트가 데이터베이스에 영구적으로 저장된다.
  - 따라서 이 시점 이후에는 트랜잭션을 롤백할 수 없다.
- **실패(Failed)**
  - 트랜잭션이 실패하거나, 활성화 또는 부분 완료 상태에서 중단된 경우 트랜잭션은 실패 상태가 된다.
- **철회(Aborted)**
  - 트랜잭션이 비정상적으로 종료되어 롤백 연산을 수행한 상태이다.
- **종료(Terminated)**
  - 종료된 최종 트랜잭션 상태이다.
  - 데이터베이스 트랜잭션 생애 주기의 끝을 의미한다.

<br/>

## 트랜잭션 복구

`REDO`와 `UNDO`는 트랜잭션 복구와 관련된 서로 다른 두 가지 기술이다. _\* 본 문서에서는 REDO와 UNDO에 관해서는 자세하게 다루지 않는다._

- **UNDO** 는 되돌린다는 의미로 롤백을 통한 복구를 의미한다.
- **REDO** 다시 수행한다는 의미로 재수행을 통한 복구를 의미한다.

트랜잭션의 생명 주기와 커밋 그리고 실패 시점에 따라 REDO, UNDO 등의 수행 여부가 달라진다.

<img src="" alt="" width="">

<br/>

---

## Reference

📄 https://ko.wikipedia.org/wiki/데이터베이스_트랜잭션  
📄 https://fauna.com/blog/database-transaction  
📄 https://code-lab1.tistory.com/51  
📄 https://velog.io/@yu-jin-song/DB-트랜잭션Transaction
