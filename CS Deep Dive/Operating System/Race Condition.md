# Race Condition

`Race Condition(경쟁 상태)`이란 여러 개의 [프로세스](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Operating%20System/프로세스%20&%20스레드.md)가 공통 자원을 동시 접근하여 읽거나, 쓰는 경우 **어떤 순서**로 접근했는지에 따라서 실행 결과가 달라지는 상황이다. 즉, 공통 자원을 놓고 **경쟁하는 상태**이다.  

> Race(경쟁)의 의미가 그대로 함축되어 있다.

## Critical Section Problem
여러 스레드들이 공유 자원을 동시에 접근할 때 생기는 문제이다.  
`Critical Section(임계구역)` 이란 각 프로세스에 존재하는 공유 자원에 접근하는 코드 영역이고, `Mutual Exclusion(상호 배제)`를 지키지 않을 경우 `Race Condition`이 발생할 수 있다.  
만약 하나의 스레드가 `Critical Section`에 있다면, 다른 스레드는 그 코드 영역에 들어갈 수 없어야 한다.  

`Critical Section Problem`을 해결하기 위해선 3가지 조건이 충족되어야 한다.  

- **`Mutual Exclusion(상호 배제)`** : 하나의 스레드가 `Critical Section` 코드를 수행중이면 다른 스레드들은 그 영역에 접근할 수 없다.
- **`Progress(진행)`** : 현재 `Critical Section`에 진입한 스레드가 없는 상태에서 스레드가 진입하려 한다면 `Critical Section`에 진입하게 해주어야 한다.
- **`Bounded Waiting(유한 대기)`** : 스레드가 `Critical Section`에 진입하려고 요청한 후부터 요청이 허용될 때까지 다른 스레드들이 `Critical Section`에 진입하는 횟수에 한계가 있어야 한다. 즉, 스레드의 무한정 대기를 막는 것이다.

<br>

## 해결 방법 
여러 스레드들이 문제없이 공유 자원을 활용하도록 돕는 `Synchronization Primitive(동기화 기법)`를 사용한다.

- **Lock 방식**
  - `Mutex(뮤텍스)`: 하나의 스레드가  `Critical Section` 코드를 수행 중이면 다른 스레드는 `Critical Section`에 접근할 수 없으며, 큐에 대기시킨다.
  - `Spinlock(스핀락)` : Mutex와 달리 큐가 없고 Lock 검사를 계속 수행하는  `Busy Wating`\*을 한다.
  - `Monitor(모니터)` : 공유 자원의 구조, 공유 자원의 연산을 제공하는 `Procedure`, 현재 호출된 Procedure간의 동기화를 캡슐화한 모듈이다. 공유 자원의 접근은 Procedure를 통해서만 가능하다.  
  
  ![monitor](https://user-images.githubusercontent.com/102718303/209980840-8b94a1ac-67f5-4212-93ec-4abd73304fcf.png) 

  _\*Busy Wating : Critical Section 진입을 기다리면서 계속 CPU와 메모리를 사용한다._ 

- **Wait-Signal 방식**
  - `Semaphore(세마포어)` : n개의 자원을 다수의 스레드가 공유하여 사용하도록 돕는 자원 관리 기법으로, counter 변수를 사용하여 여러 스레드가 `Critical Section`에 접근하는 것을 원할하게 관리한다.

<br>

\*[Semaphore & Mutex 자세히 보기](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Operating%20System/세마포어(Semaphore)%20&%20뮤텍스(Mutex).md)  

----
## Reference
- https://iredays.tistory.com/125
- https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B2%BD%EC%9F%81-%EC%83%81%ED%83%9C-Race-Condition
-https://systorage.tistory.com/entry/CS-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94
- https://rebro.kr/176
- 명품 운영체제, 황기태 저, 생능출판사, 2023 
