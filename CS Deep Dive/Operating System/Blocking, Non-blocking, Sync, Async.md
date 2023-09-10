# Blocking / Non-blocking. Synchronous / Asynchronous

Blocking과 Asynchronous를 같은 개념으로 잘못 이해하는 경우가 많다.  
Blocking/Non-blocking 과 Synchronous/Asynchronous는 다른 관점의 다른 개념이다.

<br/>

## Blocking / Non-blocking

한 작업이 다른 작업을 호출했을 때 제어권이 어디에 있는지에 따른 서로 다른 방식이다.

- **Blocking** <br>
  - 호출된 함수가 계속 제어권을 갖고, 기존 함수는 대기한다.  
  - 호출된 함수가 기존 함수를 **Block 한다**.
  - 호출된 함수는 그 결과를 작업이 **다 끝난 후** 반환한다.
- **Non-blocking** <br>
  - 호출된 함수가 제어권을 바로 반환하여 기존 함수가 다른 작업을 수행할 수 있다.  
  - 호출된 함수가 기존 함수를 **Block 하지 않는다**.
  - 호출된 함수는 결과의 처리 유무를 **바로** 반환한다.

> **제어권** <br>
  함수의 코드나 프로세스의 실행 흐름을 제어할 수 있는 권리를 말한다.

<br/>

## Synchronous / Asynchronous

동기(Synchronous)와 비동기(Asynchronous)는 프로세스 수행 순서 보장에 관한 서로 다른 매커니즘이다.

- **Synchronous** <br>
  - 동기는 수행 순서가 보장되는 것을 의미한다.  
  - 수행 순서를 보장하기 위해 기존 함수가 호출된 함수의 작업 완료 여부를 확인한다.

- **Asynchronous** <br>
  - 비동기는 수행 순서가 보장되지 않는 것을 의미한다.  
  - 기존 함수는 수행 순서를 확인하지 않는다. 호출된 함수에게 Callback을 전달해서 작업을 완료하면 실행하도록 하는 등의 방식이다.
  - I/O 작업과 같이 느린 작업이 발생할 때 기다리지 않고 다른 작업을 같이 처리하므로 동시에 처리하는 멀티 작업을 진행할 수 있다. 이는 전반적인 시스템 성능 향상에 도움을 줄 수 있다.

<br/>

## Blocking / Non-blocking X Synchronous / Asynchronous

`Blocking` / `Non-blocking`과 `Synchronous` / `Asynchronous` 를 조합하면 다음 그림처럼 4가지 방식이 생긴다.

<img src="https://user-images.githubusercontent.com/66757141/210782186-d6313700-834a-49ec-bf5d-f00cbe577817.png" alt="Blocking / Non-blocking / Synchronous / Asynchronous" width="700px" />


### 1. Sync Blocking
호출한 작업이 진행되는 동안 자신의 작업을 멈추고 호출한 작업이 끝난 후 그 결과를 받으며(Blocking), 호출한 작업의 완료 여부를 받은 후 순차적으로 자신의 작업을 처리(Sync)하는 방식이다.
* **코드 동작 예시** <br>
  ``` js
  const fs = require('fs'); // 파일 시스템 모듈 불러오기

  // 동기적으로 파일 읽기
  const data1 = fs.readFileSync('file1.txt', 'utf8'); // file1을 sync으로 read 함
  console.log(data1); // 파일 내용 출력하고 적절한 처리를 진행

  const data2 = fs.readFileSync('file2.txt', 'utf8'); 
  console.log(data2); 

  const data3 = fs.readFileSync('file3.txt', 'utf8'); 
  console.log(data3);
  ```

### 2. Sync Non-blocking
호출한 작업이 진행되는 동안에도 자신의 작업을 처리하고 호출한 작업의 결과 처리 유무를 바로 받으며(Non-Blocking), 호출한 작업의 완료 여부를 받은 후 순차적으로 자신의 작업을 처리(Sync)하는 방식이다.
* **코드 동작 예시** <br>
  동기 + 논블로킹 코드를 표현하는데 적합한 대중적인 언어로 자바를 들 수 있다. 스레드 객체를 만들어 요청 작업을 백그라운드에 돌게 하고, 메인 메서드에서 while문을 통해 스레드가 모두 처리되었는지 끊임없이 확인하고, 처리가 완료되면 다음 메인 작업을 수행한다.
  ``` java
  // Runnable 인터페이스를 구현하는 클래스 정의
  class MyTask implements Runnable {
      @Override
      public void run() {
          // 비동기로 실행할 작업
          System.out.println("Hello from a thread!");
      }
  }

  public class Main {
      public static void main(String[] args) {
          // Thread 객체 생성
          Thread thread = new Thread(new MyTask());

          // 스레드 실행
          thread.start();

          // Non-Blocking이므로 다른 작업 계속 가능
          System.out.println("Main thread is running...");

          // Sync를 위해 스레드의 작업 완료 여부 확인
          while (thread.isAlive()) {
              System.out.println("Waiting for the thread to finish...");
          }
          System.out.println("Thread finished!");

          System.out.println("Run the next tasks");
      }
  }
  ```


### 3. Async Blocking
호출한 작업이 진행되는 동안 자신의 작업을 멈추고 호출한 작업이 끝난 후 그 결과를 받으며(Blocking), 순차적으로 작업이 수행됨을 보장하지 않는(Async) 방식이다. <br>
실무에서 잘 마주하지 않아 다룰 일이 거의 없다. <br>
Sync-blocking과 개념적으로 차이가 있지만, 성능적으로 차이가 없다. 보통 Asnyc-blocking은 개발자가 Async-NonBlocking으로 처리하려다가 실수하는 경우에 발생한다. 그래서 이 방식을 안티 패턴이라고 치부하기도 한다.

### 4. Async Non-blocking
호출한 작업이 진행되는 동안에도 자신의 작업을 처리하고 호출한 작업의 결과 처리 유무를 바로 받으며(Non-Blocking), 순차적으로 작업이 수행됨을 보장하지 않는(Async) 방식이다. <br>
* **코드 동작 예시**
  Sync Blocking에서 구현한 코드를 Asnyc Non-Blocking 방식으로 구현한 것이다. 차이점은 호출 함수에 콜백 함수를 넣음으로써 작업의 결과를 후처리 할 수 있다.
  ``` js
  // 비동기적으로 파일 읽기
  const fs = require('fs'); // 파일 시스템 모듈 불러오기

  fs.readFile('file.txt', 'utf8', (err, data) => { // 파일 읽기 요청과 콜백 함수 전달
    if (err) throw err; // 에러 처리
    console.log(data); // 파일 내용 출력
  });

  fs.readFile('file2.txt', 'utf8', (err, data) => {
    if (err) throw err; 
    console.log(data);
  });

  fs.readFile('file3.txt', 'utf8', (err, data) => { 
    if (err) throw err; 
    console.log(data);
  });

  console.log('done'); // 작업 완료 메시지 출력
  ```

<br/>


## Blocking I/O, Non-blocking I/O

**Blocking / Non-blocking** 내용을 운영체제에서 `Blocking I/O`, `Non-blocking I/O`로, 네트워크에서 `Blocking API`, `Non-blocking API` 등으로 소개되기도 하는데 근본적인 내용은 같다. **Blocking / Non-blocking** 은 각 분야들에 적용되는 개념으로 입출력의 두 가지 방식을 구분하기도 하고, 네트워크에도 적용되는 것이다.

<br>

I/O는 데이터의 Input과 Output을 일컫는 말로 네트워크를 통한 데이터의 전송, 콘솔의 입출력 등 모든 데이터의 입출력을 포함하는 개념이다.
Kernel level에서의 입출력에 Blocking과 Non-blocking을 적용하여 생각한다면, Process, Thread가 기존 함수이고 커널의 I/O 호출하는 형태로 이해할 수 있다.

![img (1)](https://user-images.githubusercontent.com/66757141/210787511-bbffdbb2-2789-48c5-b912-3092d5242e96.png)

![img (2)](https://user-images.githubusercontent.com/66757141/210787522-9d7663b5-df27-44de-9813-06c382350b45.png)

<br/>

---

## Reference

📄https://interconnection.tistory.com/141  
📄https://jaehoney.tistory.com/242  
📄https://steady-coding.tistory.com/531  
📄https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/%5BNetwork%5D%20Blocking%20Non-Blocking%20IO.md  
📄https://etloveguitar.tistory.com/140  
📄https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC  
📄https://hamait.tistory.com/m/930