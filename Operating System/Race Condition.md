# Race Condition

`Race Condition`이란 여러 개의 프로세스가 공통 자원을 동시 접근하여 읽거나, 쓰는 경우 **어떤 순서**로 접근했는지에 따라서 실행 결과가 달라지는 상황이다. 즉, 공통 자원을 놓고 **경쟁하는 상태**이다.

> Race(경쟁)의 의미가 그대로 함축되어 있다.

## Critical Section Problem
여러 프로세스들이 공유 자원을 동시에 접근할 때 생기는 문제이다. </br>
`Critical Section` 이란 각 프로세스에 존재하는 공유 자원에 접근하는 코드 영역이고, `Race Condition`이 발생할 수 있다. </br>
만약 하나의 프로세스가 `Critical Section`에 있다면, 다른 프로세스는 그 코드 영역에 들어갈 수 없어야 한다. </br>

`Critical Section Problem`을 해결하기 위해선 3가지 조건이 충족되어야 한다.

- **`Mutual Exclusion(상호 배제)`** : 한 프로세스가 `Critical Section`을 수행중이면 다른 프로세스들은 그 영역에 접근할 수 없다. </br>
- **`progress`** : 현재 `Critical Section`에 접근한 프로세스가 없는 상태에서 접근하려고 하는 프로세스가 있다면 `Critical Section`에 들어가게 해주어야 한다.</br>
- **`Bounded Waiting(유한 대기)`** : 프로세스가 `Critical Section`에 들어가려고 요청한 후부터 요청이 허용될 때까지 다른 프로세스들이 `Critical Section`에 들어가는 횟수에 한계가 있어야 한다. 즉, 프로세스의 무한정 대기를 막는 것이다. </br></br>



## 해결 방법 
해결 방법은 프로세스들끼리의 실행 순서를 정해주는 `Synchronization(동기화)`과정이 필요하다.

- `Semaphore(세마포어)` : 세마포어 변수를 사용하여 여러 프로세스가  `Critical Section`에 진입할 수 있다. </br>
  - **Busy Wating** 사용 X
- `Mutex(뮤텍스)` : 하나의 프로세스가  `Critical Section`에서 수행 중이면 다른 프로세스는  `Critical Section`에 접근할 수 없다. 
  - **lock이 하나만 존재**
  - **Busy Wating**의 단점
- `Monitor` : 공유 자원의 구조, 공유 자원의 연산을 제공하는 `Procedure`, 현재 호출된 프로시저간의 동기화를 캡슐화한 모듈이다. 공유 자원의 접근은 프로시저를 통해서만 가능하다. </br>

![monitor](https://user-images.githubusercontent.com/102718303/209980840-8b94a1ac-67f5-4212-93ec-4abd73304fcf.png)


> `Busy Waiting` : Critical Section 진입을 기다리면서 계속 CPU와 메모리를 사용

----
## Reference
- https://iredays.tistory.com/125
- https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B2%BD%EC%9F%81-%EC%83%81%ED%83%9C-Race-Condition
-https://systorage.tistory.com/entry/CS-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94
- https://rebro.kr/176
