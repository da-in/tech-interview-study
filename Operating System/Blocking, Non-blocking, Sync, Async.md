# Blocking / Non-blocking. Synchronous / Asynchronous

Blocking과 Asynchronous를 같은 개념으로 잘못 이해하는 경우가 많다.  
Blocking/Non-blocking 과 Synchronous/Asynchronous는 다른 관점의 다른 개념이다.

<br/>

## Blocking / Non-blocking

한 작업이 다른 작업을 호출했을 때 제어권이 어디에 있는지에 따른 서로 다른 방식이다.

- **Blocking**
  호출된 함수가 계속 제어권을 갖고, 기존 함수는 대기한다.  
  호출된 함수가 기존 함수를 **Block 한다**.
- **Non-blocking**
  호출된 함수가 제어권을 바로 반환하여 기존 함수가 다른 작업을 수행할 수 있다.  
  호출된 함수가 기존 함수를 **Block 하지 않는다**.

**Blocking / Non-blocking** 내용을 운영체제에서 `Blocking I/O`, `Non-blocking I/O`로, 네트워크에서 `Blocking API`, `Non-blocking API` 등으로 소개되기도 하는데 근본적인 내용은 같다. **Blocking / Non-blocking** 은 각 분야들에 적용되는 개념으로 입출력의 두 가지 방식을 구분하기도 하고, 네트워크에도 적용되는 것이다.

## Synchronous / Asynchronous

동기(Synchronous)와 비동기(Asynchronous)는 프로세스 수행 순서 보장에 관한 서로 다른 매커니즘이다.

- **Synchronous**
  동기는 수행 순서가 보장되는 것을 의미한다.  
  수행 순서를 보장하기 위해 기존 함수가 호출된 함수의 작업 완료 여부를 확인한다.

- **Asynchronous**
  동기는 수행 순서가 보장되지 않는 것을 의미한다.  
  기존 함수는 수행 순서를 확인하지 않는다. 호출된 함수에게 Callback을 전달해서 작업을 완료하면 실행하도록 하는 등의 방식이다.

---

## Reference

📄https://interconnection.tistory.com/141  
📄https://jaehoney.tistory.com/242  
📄https://steady-coding.tistory.com/531
