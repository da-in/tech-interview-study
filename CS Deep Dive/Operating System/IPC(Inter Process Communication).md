# IPC(Inter Process Communication)

**프로세스 간 통신(Inter-Process Communication, IPC)** 이란 프로세스들 사이에 서로 데이터를 주고받는 행위 또는 그에 대한 방법이나 경로를 뜻한다.  

**프로세스(Process)** 는 독립적으로 실행되는 객체이지만 정보 공유, 계산 속도 향상, 모듈성, 편의성 들을 위해 통신을 필요로 할 수 있다. 그렇지만 프로세스들은 주소 공간이 분리되어 있어 프로세스가 다른 프로세스의 공간을 액세스 할 수 없다. 따라서 운영체제는 독립적인 프로세스 간 통신을 위해 데이터를 교환할 수 있는 `IPC`를 제공한다.

<br/>

## IPC 라이브러리
응용프로그램에서 IPC를 활용하는 방법은 다음 2가지로 나뉜다.
* System V의 IPC 라이브러리
* POSIX 표준 IPC 라이브러리

<br>

* **차이점**  
두 라이브러리가 지원하는 IPC 함수의 이름은 조금씩 다르지만, 사용하는 방법에는 큰 차이가 없다.  

||System V|POSIX 표준|
|---|---|---|
|공유 메모리에 접근하기 위한 공유키|16비트 정수 사용|파일 경로명 사용|

<br>

## IPC Model

IPC의 두 가지 기본 모델에는 **공유 메모리** 과 **메세지 패싱**가 있다.

- 공유 메모리 모델 : `Shared Memory`, `Memory Map`  
- 메세지 패싱 모델 : `Signal`, `PIPE`, `FIFO`, `Message Queue`, `Socket`, `Semaphore`

## 1. 공유 메모리 모델(Shared-memory Model)

- 프로세스 간의 공유 메모리 영역을 설정한 다음 공유 영역에서 데이터를 읽고 쓰는 방식으로 정보를 교환한다.
- 시스템 콜이 공유 메모리 생성 및 제거할 때에만 필요하므로 커널의 개입이 적어, 메세지 패싱 모델보다 빠르다는 장점이 있다.
- 동기화 문제가 발생할 수도 있다는 단점이 있다.

<img src="https://user-images.githubusercontent.com/66757141/213210653-10cda272-e938-4783-bd33-e998d776ab2c.png" alt="shared memory model" /><br/>
[_img reference_](https://sepang2.tistory.com/45)

### Shared Memory
공유 메모리는 한 컴퓨터 시스템 내에 있는 프로세스들에 의해서만 공유된다. 프로세스 중 하나가 먼저 공유 메모리를 생성하면 다른 프로세스들이 이 공유 메모리를 읽거나 쓸 수 있다.

공유 메모리를 사용하는 응용프로그램은 다음 과정에 해당하는 코드를 작성한다.
1. 공유 메모리 생성
2. 공유 메모리 크기 설정
3. 가상 주소 공간에 매핑
4. 공유 메모리 읽거나 쓰기
5. 공유 메모리 사용이 끝났을 시 공유 메모리를 가상 주소 공간에서 분리
6. 공유 메모리 닫기
7. 커널에게 공유 메모리를 메모리에서 완전히 제거하도록 요청

<br>

## 2. 메세지 패싱 모델(Message-passing Model)

- 공유되는 주소 공간 없이, 협력 프로세스 간에 교환되는 메세지를 통해 정보를 교환한다.
- send, receive 연산을 통해 통신한다.
- 큐를 사용하여 프로세스 간 메세지를 주고 받게되며, 일반적으로 커널의 시스템 콜을 사용하여 구현된다.
- 커널의 개입으로 동기화 문제로부터 안전하다는 장점이 있다.
- 커널이 개입하므로 비교적 많은 시간이 소요된다는 단점이 있다.

<img src="https://user-images.githubusercontent.com/66757141/213210443-4baf6513-8b9f-4f63-8419-a303d529d6a5.png" alt="message passing model" /><br/>
[_img reference_](https://sepang2.tistory.com/45)

메세지 패싱 모델의 IPC는 세 가지 요소가 다른 방식으로 구현될 수 있다.

1. **Direct Communication과 Indirect Communication**
   - `Direct Communication` : 프로세스가 커널에 메시지를 전달하면, 커널이 상대 프로세스에 메세지를 직접 전달한다.
   - `Indirect Communication` : 프로세스가 커널을 통해 메일박스 또는 포트에 메세지를 넣어두고, 상대 프로세스가 커널을 통해 메일박스 또는 포트에서 해당 메세지를 읽어온다.
2. **Synchronous**
   - `Blocking` : 두 프로세스는 메세지가 수신될 때 까지 기다린다.
   - `Non-Blocking` : 송신측은 메세지를 보내고 자신의 할 일을 한다. 수신측도 수신문을 실행하고도 계속 작업을 이어간다.
3. **Buffering**
프로세스들에 의해 교환되는 메시지는 임시 큐에 들어가 있는다.
   - `Zero Capacity` : 큐의 길이가 0이다. 따라서 송신측은 무조건 수신자를 기다린다.
   - `Bounded Capacity` : 큐의 길이가 n이다. 따라서 송신측은 link가 꽉차면 기다린다.
   - `Unbounded capacity` : 큐의 길이가 무한하다. 따라서 송신측은 기다리지 않는다.

<br/>

### Signal
프로세스들끼리 혹은 커널이 프로세스에게 사건 발생을 비동기적으로 알리는 방법이다.

신호 핸들러를 등록하고, 신호를 보낼 때 시스템 호출 함수를 이용한다. 신호 핸들러는 사용자 공간에 작성되는 코드이며, 신호가 전달되는 과정은 커널에 의해 이루어진다. 신호 핸들러가 등록되어 있지 않은 경우 4가지 기본 행동 중 하나를 취한다.
1. 종료: 신호를 수신할 프로세스를 강제 종료
2. 코어 덤프: 신호를 수신할 프로세스를 강제 종료시키고 코어 파일 생성
3. 중지: 신호를 수신할 프로세스의 실행을 일시 중지. 중지된 프로세스는 이후 계속 실행 가능
4. 무시: 신호를 무시하고 아무 처리도 하지 않음

* 신호를 수신하게 되는 경우
   * 프로세스 자신이 보낸 신호 수신
   * 다른 프로세스로부터 신호 수신
   * 커널로부터 신호 수신 (ex. 0으로 나누기, 자식 프로세스 종료, 시스템 알람 등의 사건)

* 신호 처리 과정
   1. 신호 등록: 시스템 호출을 이용하여 신호를 수신했을 때 실행시킬 핸들러를 등록한다.
   2. 신호 발생: 송신 프로세스가 수신 프로세스로 신호를 보낸다.
   3. 신호 전파: 커널이 수신 프로세스가 신호 핸들러를 실행하도록 한다.


<br>

### PIPE

<img src="https://user-images.githubusercontent.com/66757141/213225176-084ea7be-6f0b-4300-9269-3d3770d81e28.jpg" alt="pipe_with_one" /><br/>
[_img reference_](https://www.tutorialspoint.com/inter_process_communication/inter_process_communication_pipes.htm)

파이프(PIPE)는 두 개의 프로세스를 연결하며, 하나의 프로세스는 쓰기만 가능하고 다른 프로세스는 읽기만 가능한 형태이다. 이러한 특성으로 `반이중(Half-Duplex)통신`이라고 부른다.

만일 두 프로세스가 모두 읽기와 쓰기가 가능하도록 하고싶다면 파이프를 두 개 만들어 사용해야한다. 하지만 이는 구현이 복잡하다. 따라서 전이중 통신이 필요한 상황에서는 부적합 할 수 있다.

<br/>

---

## Reference

✨https://sepang2.tistory.com/37?category=981709  
📄https://ko.wikipedia.org/wiki/프로세스_간_통신  
📄https://jwprogramming.tistory.com/54  
📄https://sepang2.tistory.com/45  
📄https://jhnyang.tistory.com/24  
📄https://code-lab1.tistory.com/42  
📄https://www.tutorialspoint.com/inter_process_communication/inter_process_communication_pipes.htm  
📄https://neos518.tistory.com/134
교재(명품 운영체제)