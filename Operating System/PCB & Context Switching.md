# PCB (Process control Block)
구동중인 프로세스가 여러개이기 때문에 CPU 스케줄링을 통해 프로세스들을 관리한다. </br>
그럼 각각의 프로세스들을 어떻게 구분할까? </br>
PCB는 OS에 **프로세스의 메타데이터**들를 저장해놓은 곳이다. **하나의 PCB**에는 **하나의 프로세스 정보**가 담긴다. </br>

### 언제 생기고 언제 없어지나?
- 프로세스가 생겨나고, 프로세스 주소 공간에 코드, 데이터, 스택 공간이 생성된 후 PCB가 생성 & 저장된다. </br>
- 프로세스가 종료되면 PCB도 제거!

## 프로세스 정보
- `PID (Process ID)` : 프로세스 고유 식별 번호
- `Process State` : 현재 프로세스의 상태 기억
- `Process Priority` : 프로세스의 우선순위 저장
- `CPU Register` : 프로세스의 레지스터 상태를 저장하는 공간
- `Owner (계정 정보)` : CPU 사용시간의 정보 (Quantum), 스케줄러에 필요한 정보 기억
- `기억장치 관리 정보`
- `입출력 정보` : 프로세스 수행 시 필요한 주변 장치, 파일 정보 기억
- `프로그램 카운터 (PC)` : 다음 실행되는 명령어의 주소 기억
- `시그널 관련 정보` </br>

![PCB](https://user-images.githubusercontent.com/102718303/209789440-032105cc-1371-41b8-bb30-2940db268c36.png)


## PCB가 필요한 이유
여러개의 프로세스를 스케줄링 하기 위해서 현재 프로세스의 상태가 필요하고, CPU는 이를 토대로 스케줄링 한다. </br>
만약 어떤 프로세스로부터 인터럽트가 발생해서 현재 프로세스가 잠시 대시 상태가 되고, 인터럽트가 발생된 프로세스를 실행 상태로 바꿀 때, </br>
대기 중인 프로세스 정보를 잃어버리면 처음부터 다시 시작해야 한다.  </br>

따라서 여러 프로세스들이 이어서 잘 실행하기 위해 대기 중인 프로세스의 직전 정보, 상태를 저장해두는 공간인 PCB가 필요하다. </br>
> PCB에 저장된 정보를 기반으로 레지스터 값을 불러온다.


## PCB 관리
- **연결리스트 방식**으로 관리 -> **삽입, 삭제 용이!**
- PCB List Head에 PCB들이 생성될 때마다 이어붙게 된다. </br>

![pcb 연결](https://user-images.githubusercontent.com/102718303/209789493-5c33a99a-11b7-44f1-9c0e-2a47a2988b74.jpg)

>프로세스가 생성되면 `Ready Queue`에 들어가는데, 실제론 PCB가 연결리스트로 연결되어 있다. </br>
 
# Context Switching (문맥 교환)
- 여러 프로세스들이 CPU 스케줄링에 의해서 실행되는 데, 이 과정에서 프로세스를 바꾸는 행위(갈아끼우는)를 `Context Switching` 이라고 한다. 
- 원래 실행중이던 프로세스의 정보를 PCB에 저장하고, 바뀌는 프로세스의 정보를 토대로 레지스터에 값을 적재하는 과정이다. </br>
- 여러 개의 프로세스들을 동시에 수행하는 것처럼 보이게 하귀 위해 사용한다.

<img width="665" alt="컨택스 스위칭" src="https://user-images.githubusercontent.com/102718303/209789540-eb83853d-1615-40ce-bdb5-cacb13518303.png">


## 언제 발생하는가?
- 인터럽트 발생
- 프로세스의 선점시간 종료
- 입출력을 위해 대기하는 경우

> Context Switching 과정에서 CPU는 아무것도 하지 못하기 때문에 너무 빈번하게 일어나면 성능이 떨어질수 있다. </br>
> `Context Switching Overhead`를 주의 해야한다.


## Reference
- https://velog.io/@haero_kim/PCB-%EC%99%80-Context-Switching-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0
- 공룡 책
- https://velog.io/@heetaeheo/PCB-%EC%99%80-Context-Switching
