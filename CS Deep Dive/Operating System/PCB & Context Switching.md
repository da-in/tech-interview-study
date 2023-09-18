# PCB & Context Switching
## PCB (Process Control Block)
현대 운영체제는 여러 프로세스를 동시에 실행시키는 다중프로그래밍 운영체제이다. 구동중인 프로세스가 여러개이기 때문에, CPU 스케줄링을 통해 어떤 프로세스가 CPU에 할당될지 결정된다. 각각의 프로세스들은 어떻게 구분될까?

커널은 시스템 전체에 하나의 프로세스 테이블을 두고 실행 중인 모든 프로세스들을 관리한다. 또한 프로세스를 생성할 때마다 PCB를 생성하여 프로세스의 정보를 저장한다. 그리고 프로세스 테이블의 비어있는 항목에 PID(프로세스 번호)와 함께 PCB를 연결한다. 운영체제는 프로세스들을 PID로 구분한다. 

PCB는 **프로세스 관리의 메타 데이터**들을 저장해놓은 곳이다. **하나의 PCB**에는 **하나의 프로세스 정보**가 담긴다.

### PCB의 생성과 제거
* **생성**  
프로세스가 생겨나고, 프로세스 주소 공간에 코드, 데이터, 스택 공간이 생성된 후 PCB가 생성되고 프로세스 정보가 저장된다.
* **제거**  
프로세스가 종료되면 PCB도 제거된다.

### PCB에 저장되는 프로세스 정보
- `Pointer` : 프로세스의 현재 위치를 저장
- `Process State` : 현재 프로세스의 상태 정보(Create, Ready, Running, Waiting, Terminated)
- `PID (Process ID)` : 프로세스 고유 식별 번호
- `Program Counter` : 프로세스가 다음에 실행할 명령어의 주소
- `Registers` : 누산기, 베이스, 범용 레지스터 등
- `Memory Limits` : 메모리 관리 시스템 정보(페이지 테이블, 세그먼트 테이블 등)
- `Open File Lists` : 프로세스가 실행 중에 열어놓은 파일에 관한 정보

<img style="width: 500px" alt="PCB" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5tmZc%2FbtqUnLvQf0W%2FPVZ1TLoN3mEWk5YkjLUd90%2Fimg.png">


### PCB가 필요한 이유
여러 프로세스를 스케줄링 하기 위해 현재 프로세스의 상태가 필요하고, CPU는 이를 토대로 스케줄링 한다. </br>
만약 어떤 프로세스로부터 인터럽트가 발생해서 현재 프로세스가 잠시 `대기` 상태가 되고 인터럽트가 발생된 프로세스를 `실행` 상태로 바꿀 때, 대기 중인 프로세스 정보를 잃어버리면 처음부터 다시 시작해야 한다.  </br>

따라서 여러 프로세스를 이어서 잘 실행하기 위해 대기 중인 프로세스의 직전 정보와 상태를 저장하는 공간인 PCB가 필요하다.

커널은 현재 CPU가 실행 중인 프로세스를 중단시키고 다른 프로세스를 실행시킬 때, 현재 프로세스가 실행 중인 상황 정보, 즉 프로세스 컨텍스트를 PCB에 저장한다. 프로세스 컨텍스트는 현재 프로세스의 실행 상태를 나타내는 레지스터 값이다.


#### 프로세스 스케줄링
- **연결리스트 방식**으로 관리되기 때문에 **삽입, 삭제가 용이**하다.
- PCB List Head에 PCB들이 생성될 때마다 이어붙게 된다. </br>

<img style="width: 500px" alt="PCB 연결" src="https://user-images.githubusercontent.com/102718303/209789493-5c33a99a-11b7-44f1-9c0e-2a47a2988b74.jpg">

>프로세스가 생성되면 `Ready Queue`에 들어가는데, 실제론 PCB가 연결리스트로 연결되어 있다. </br>
 
## Context Switching (문맥 교환)
- 여러 프로세스들이 CPU 스케줄링에 의해서 실행되는 데, 이 과정에서 프로세스를 바꾸는 행위(갈아끼우는)를 `Context Switching` 이라고 한다. 
- 원래 실행중이던 프로세스의 정보를 PCB에 저장하고, 바뀌는 프로세스의 정보를 PCB에 저장된 내용을 토대로 레지스터에 적재하는 과정이다. </br>
- 여러 프로세스들을 동시에 수행하는 것처럼 보이게 하기 위해 사용한다.

<img width="width: 500px" alt="Context Switching" src="https://user-images.githubusercontent.com/102718303/209789540-eb83853d-1615-40ce-bdb5-cacb13518303.png">


### 발생하는 경우
- 인터럽트 발생
- 프로세스의 선점시간 종료
- 입출력을 위해 대기하는 경우

> Context Switching 과정에서 CPU는 아무것도 하지 못하기 때문에 너무 빈번하게 일어나면 성능이 떨어질수 있다. </br>
> `Context Switching Overhead`를 주의 해야한다.


## Reference
- https://velog.io/@haero_kim/PCB-%EC%99%80-Context-Switching-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0
- operating system concepts 10th edition
- https://velog.io/@heetaeheo/PCB-%EC%99%80-Context-Switching
- https://velog.io/@devdynam0507/CS-PCB
