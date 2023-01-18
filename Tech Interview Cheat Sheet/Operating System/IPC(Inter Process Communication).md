# IPC(Inter Process Communication)

**프로세스 간 통신(Inter-Process Communication, IPC)** 이란 프로세스들 사이에 서로 데이터를 주고받는 행위 또는 그에 대한 방법이나 경로를 뜻한다.

**프로세스(Process)** 는 독립적으로 실행되는 객체이지만 정보 공유, 계산 속도 향상, 모듈성, 편의성 들을 위해 통신을 필요로 할 수 있으며, 독립적인 프로세스 간의 통신을 위해서는 데이터를 교환하는 `IPC 메커니즘`이 필요하다.

<br/>

## IPC Model

IPC의 두 가지 기본 모델에는 **메세지 패싱** 과 **공유 메모리** 가 있다.

### 1. 메세지 패싱 모델(Message-passing Model)

- 메세지 패싱 모델은 협력 프로세스 간에 교환되는 메세지를 통해 통신이 발생한다.
- 메세지 큐를 사용하여 프로세스 간 메세지를 주고 받게되며, 일반적으로 커널의 시스템콜을 사용하여 구현된다.
- 커널의 개입으로 동기화 문제로부터 안전하다는 장점이 있다.
- 커널이 개입하므로 비교적 많은 시간이 소요된다는 단점이 있다.

<img src="https://user-images.githubusercontent.com/66757141/213210443-4baf6513-8b9f-4f63-8419-a303d529d6a5.png" alt="message passing model" /><br/>
[_img reference_](https://sepang2.tistory.com/45)

메세지 패싱 모델의 IPC는 세 가지 요소가 다른 방식으로 구현될 수 있다.

1. **Direct Communication과 Indirect Communication**
   - `Direct Communication` : 프로세스가 커널에 메시지를 전달하면, 커널이 상대 프로세스에 메세지를 직접 전달한다.
   - `Indirect Communication` : 프로세스가 커널에 메세지를 넣어두고, 상대 프로세스가 커널에서 해당 메세지를 읽어온다.
2. **Synchronous**
   - `Blocking` : 두 프로세스는 메세지가 수신될 때 까지 기다린다.
   - `Non-Blocking` : 송신측은 메세지를 보내고 자신의 할 일을 한다. 수신측도 수신문을 실행하고도 계속 작업을 이어간다.
3. **Buffering**
   - `Zero Capacity` : 송신측은 무조건 수신자를 기다린다.
   - `Bounded Capacity` : 송신측은 link가 꽉차면 기다린다.
   - `Unbounded capacity` : 송신측은 기자리지 않는다.

### 2. 공유 메모리 모델(Shared-memory Model)

- **공유 메모리** 모델은 프로세스 간의 공유 메모리 영역을 설정한 다음 공유 영역에서 데이터를 읽고 쓰는 방식으로 정보를 교환한다.
- 시스템 콜이 공유 메모리 영역을 설정할 때에만 필요하므로 커널의 개입이 적어, 메세지 패싱 모델보다 빠르다는 장점이 있다.
- 동기화 문제를 해결해야한다는 단점이 있다.

<img src="https://user-images.githubusercontent.com/66757141/213210653-10cda272-e938-4783-bd33-e998d776ab2c.png" alt="shared memory model" /><br/>
[_img reference_](https://sepang2.tistory.com/45)

<br/>

## IPC 설비

- 메세지 패싱 모델 : `PIPE`, `FIFO`, `Message Queue`, `Socket`, `Semaphore`
- 공유 메모리 모델 : `Shared Memory`, `Memory Map`  
  <br/>
- Traditional Unix IPCs : `signal`, `pipe`, `socket`
- System V IPCs : `message queue`, `semaphore`, `shared memory`

<br/>

---

## Reference

✨https://sepang2.tistory.com/37?category=981709  
📄https://ko.wikipedia.org/wiki/프로세스_간_통신  
📄https://jwprogramming.tistory.com/54  
📄https://sepang2.tistory.com/45  
📄https://jhnyang.tistory.com/24  
📄https://code-lab1.tistory.com/42
