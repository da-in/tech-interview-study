# Race condition

`Race Condition`이란 여러 개의 프로세스가 공통 자원을 동시 접근하여 읽거나, 쓰는 경우 **어떤 순서**로 접근했는지에 따라서 </br>
실행 결과가 달라지는 상황이다. 즉 공통 자원을 놓고 **경쟁하는 상태**이다.

> Race(경쟁)의 의미가 그대로 함축되어 있다.

## 제어 문제들
프로세스들이 경쟁하는 경우 세가지 제어 문제가 발생한다.

- `Mutual Exclusion(상호 배제)` : 여러 프로세스가 공용 자원에 동시 접근 하는 것을 막는다. 한 프로세스가 사용중이라면, 사용이 불가하거나 접근이 불가하게 만드는 것. 
- `Deadlock(교착 상태)` : 상호 배제가 충족되더라도 서로 자원의 해제를 무한정 기다리는 교착 상태가 발생할 수 있다. 
- `Starvation(기아 상태)` : 프로세스가 진행되지 않고 계속 블록되어 있는 상황이다. 즉 자신에게 소유권이 넘어오지 않고 무한정 기다리는 것.

> `Deadlock`과 `Starvation`의 차이점?

## 해결 방법 
해결 방법은 프로세스들끼리 `Synchronization(동기화)`이 필요하다.

- `Semaphore(세마포어)`
- `Mutex(뮤텍스)`
- `Monitor`


----
## Reference
- https://iredays.tistory.com/125
- https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B2%BD%EC%9F%81-%EC%83%81%ED%83%9C-Race-Condition
