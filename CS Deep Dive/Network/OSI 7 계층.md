# OSI 7 계층
OSI 7 계층은 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것을 말하며, 국제표준화기구(ISO, International Organization for Standardization)에서 네트워크 간의 호환을 위해 OSI 7 계층이라는 표준 네트워크 모델을 만들었다. 개방형 시스템 상호 연결 모델(OSI)의 표준이다.

초기 여러 정보 통신 업체 장비들은 자신의 업체 장비들끼리만 연결이 되어 호환성이 없었다. 모든 시스템들의 상호 연결에 있어 문제없도록 **표준**을 정한것이 OSI 7계층이고, 실제 인터넷에서 사용되는 TCP/IP 4계층\*은 OSI 참조 모델을 기반으로 상업적이고 실무적으로 이용될 수 있도록 단순화 한 것이다.

_\* TCP/IP 4계층: L1 네트워크 액세스 계층(물리 계층 + 데이터링크 계층), L2 인터넷 계층(네트워크 계층), L3(전송 계층), L4 응용 계층(세션 계층 + 표현 계층 + 응용계층)_

* **특징**
  - 통신이 일어나는 과정을 단계별로 파악할 수 있다.
  - 통신 과정 중에 특정한 곳에 이상이 생긴 경우, 다른 단계의 장비 및 소프트웨어 등을 건드리지 않고 통신 장애를 일으킨 단계에서 해결할 수 있다.
  - 상위 계층의 프로토콜이 제대로 작동하기 위해서는 하위의 모든 계층에 문제가 없어야 한다.
  
<img width="500px" alt="OSI & TCP/IP" src="https://user-images.githubusercontent.com/70997596/208899170-46385a19-003d-4c50-a2bf-97b96bfcea1a.png">

<br>

## 작동 원리

- **데이터 전송 시**
  - 7계층에서 1계층으로 전달하면서 각각의 층마다 데이터를 인식할 수 있도록 헤더에 정보를 추가하며 이를 캡슐화라고 한다.
  - 출발지에서 데이터가 전송될 때 헤더에 정보가 추가되는데 2계층에서만 예외적으로 오류 제어를 위해 테일에 정보가 추가된다.
  - 하위 계층으로 내려갈수록 PDU\*에는 다양한 프로토콜에 의해 헤더와 테일이 더해진다. 물리 계층에서 PDU는 최종적인 모습으로 변하며, 데이터를 보내는 접점이 된다.
- **데이터 수신 시**
  - 1계층에서 7계층으로 헤더를 제거하며 이를 디캡슐화 라고 한다.
  - 응용 계층에 도달하면 원본 데이터만 남는다.

_\*PDU: 프로토콜 데이터 단위이며, OSI 모델의 정보 처리 단위이다._

<img weight="500px" alt="OSI" src="https://img1.daumcdn.net/thumb/R800x0/?scode%253Dmtistory2%2526fname%253Dhttps%253A%252F%252Ft1.daumcdn.net%252Fcfile%252Ftistory%252F25303F355755856B02">

## 7계층
### **L1 물리계층(Physical Layer)**

<img width="500px" alt="1layer" src="https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https://t1.daumcdn.net/cfile/tistory/25303F355755856B02">

- 7계층 중 최하위 계층이다.
- 상위 계층에서 전송된 데이터를 통신 매체(케이블, 허브, 탭, 리피터 등)를 통해 다른 시스템에 전기적 신호(0과 1의 비트열)를 전송한다.
- 데이터 전달 역할을 할 뿐 알고리즘, 오류제어 기능은 없다.

<br>

- **장비**
케이블, 허브, 탭, 리피터

<br>

### **L2 데이터링크 계층(Data-Link Layer)**

<img width="500px" alt="2layer" src="https://img1.daumcdn.net/thumb/R1600x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcedrlS%2FbtrD1tXvqHh%2FhOkxUgU1Qhr0RDNC6VlVx1%2Fimg.png">

- 통신 매체(이더넷, 케이블, 무선 랜 등)을 통한 인접한 두 장치 간의 신뢰성 있는 정보 전송을 담당한다.(Point-To-Point\* 전송)
- 데이터에 대한 오류를 감지할 수 있다. 만약 오류가 발생했다면 송신자에게 재전송하여 오류를 해결한다.
- PDU(데이터 단위)는 `프레임(Frame)`이다.
- 물리 주소인 MAC 주소\*를 헤더에 추가한다.
- 제어 정보를 테일에 추가한다.

_\* Point-To-Point: 컴퓨터 한 대가 다른 한 대의 컴퓨터에만 데이터를 보내는 방식_  
_\*MAC주소: xx : xx : xx : xx : xx : xx 의 형식으로 총 6바이트로 전 세계에서 유일한 주소이다._

<br>

- **장비**  
스위치, 브릿지

<br>

## **L3 네트워크 계층(Network Layer)**

<img width="500px" alt="3layer" src="https://img1.daumcdn.net/thumb/R1600x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNR9Ge%2FbtrD8MPHiQ0%2FkqBNBNRmKWf6Kwdil4mi71%2Fimg.png">

- 라우팅\* 알고리즘을 통해 최적 경로(목적지까지 가장 안전하고 빠른 경로)를 선택하여 데이터를 보낸다.
- 논리 주소인 IP 주소가 정의된다. (데이터 통신을 할 때 MAC 주소와 IP 주소가 사용된다.)
- PDU(데이터 단위)는 `패킷(Packet)`이다.
- 헤더에 IP 주소를 추가한다.

_\*라우팅: 네트워크에서 경로를 선택하는 프로세스이다._

<br>

- **프로토콜**  
IP, 라우팅 프로토콜  
- **장비**  
라우터, 스위치

<br>

## **L4 전송 계층(Transport Layer)**

<img width="500px" alt="4layer" src="https://img1.daumcdn.net/thumb/R1600x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoQpWd%2FbtrD5R5gZOF%2FUnuAxRirD1tiZcqEKuSUj1%2Fimg.png">

- 종단 간 신뢰성 있고 정확한 데이터 전송을 담당한다.
- 송신자와 수신자 간의 신뢰성있고 효율적인 데이터를 전송하기 위하여 오류 검출 및 복구, 흐름 제어와 중복 검사 등을 수행한다.
  - 데이터링크 계층과 유사하게 오류 제어, 흐름 제어 등을 제공하지만, 데이터링크 계층은 물리적으로 1:1 연결된 호스트 사이의 전송을 담당하고, 전송 계층은 논리적으로(네트워크 상에서) 1:1 연결된 호스트 사이의 전송을 제공한다.
- PDU(데이터 단위)는 `세그먼트(Segment)`이다.
- 헤더에 포트 번호(Port Number)를 추가한다.

<br>

- **프로토콜**  
TCP, UDP  
- **장비**  
로드 밸런서, 방화벽

<br>

## **L5 세션 계층(Session Layer)**

<img width="500px" alt="5layer" src="https://img1.daumcdn.net/thumb/R1600x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdz1Eix%2FbtrD9F3TOJl%2FSVMQIgJmLDK3J7yUpeSiFK%2Fimg.png">

- 통신 장치 간 상호 작용 및 동기화를 제공한다.
- 세션 관리를 한다. 연결된 세션에서 데이터 교환과 에러 발생 시의 복구와 재전송를 관리한다.
  - <동기 기능>  
    통신 양단 끼리 서로 동의하는 논리적인 공통 시점인 동기점을 만들어 메시지가 제대로 처리가 되고 있는지를 파악한다.  
    동기점은 오류 복구를 위하여 필수적으로 사용되는데 동기점 설정 이전까지는 서로 처리가 완료되었음을 합의하는 것을 의미한다. ( 동기점 이전 과정은 복구 X | 동기점 이후 처리과정에 대한 복구 O)
  - <대화 기능>  
    쉽게 데이터 전송 과정을 의미한다.  
    시간 경과에 따른 순차적으로 동기점을 부여하여 신뢰성 보장 기능을 단계적으로 구현할 수 있게되어 일시정지 후 나중에 이어서 작업을 진행할 수 있다.
- PDU(데이터 단위) `DATA` 이다.

<br>

- **프로토콜**  
RPC, RTCP, SSH

<br>

## **L6 표현 계층(Presentation Layer)**

<img width="500px" alt="6layer" src="https://img1.daumcdn.net/thumb/R1920x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn2Uho%2FbtrD2IH47et%2FQpbPHsQRxlhXdQTkKNdDRK%2Fimg.png">

- 데이터의 형식(png,jpg,...)을 정해준다.
- 받은 데이터를 압축, 암복호화 등의 과정을 통해 부호화\*한다.
  - MIME 인코딩이나 암호화 등의 동작이 표현계층에서 이루어짐. EBCDIC로 인코딩된 파일을 ASCII 로 인코딩된 파일로 바꿔주는 것이 한가지 예이다.

_\*부호화: 전송이 가능한 정보나 신호로 변환하는 것_

<br>

- **프로토콜**  
TLS, SSH

<br>

## **L7 응용 계층(Application Layer)**

<img width="500px" alt="7layer" src="https://img1.daumcdn.net/thumb/R1600x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeTEj5v%2FbtrD6xFx2fb%2FgJtnwbky9prdKQG2ZHOJDK%2Fimg.png">

- 사용자와 가장 밀접한 계층으로 인터페이스 역할을 한다. 즉, 사용자로부터 정보를 입력받아 하위 계층으로 전달하고 하위 계층에서 전송한 데이터를 사용자에게 전달한다.
- 응용 프로세스 간의 정보 교환을 담당한다.  
  ex) 전자메일, 인터넷, 동영상 플레이어 등

<br>

- **프로토콜**  
HTTP, SMTP, STUN, FTP, TELNET

<br>

## 대표 기능 정리
|계층|대표 기능|  
|-|-|
|물리 계층|전송 매체, 데이터 속도, 물리적 연결 형태 등을 다룬다.|  
|데이터 링크 계층|물리적 1대 1통신으로 프레임 단위로 물리 계층의 물리적 전송 오류 문제를 해결한다.|  
|네트워크 계층|데이터의 전송 경로를 결정(라우팅)한다. (IP)|  
|전송 계층|송수신 프로세스 사이의 1:1 통신 기능을 지원한다. (TCP, UDP)|  
|세션 계층|송수신자 사이 상위적 연결 개념인 세션을 지원한다.|  
|표현 계층|데이터의 의미와 표현 방법을 처리하며 암호화 압축 기능도 처리한다.|  
|응용 계층|HTTP, FTP, TeInet, email 등 다양한 인터넷 서비스 지원한다.|  

<br>

## 주요 프로토콜 및 장비
<img width="754px" src="https://velog.velcdn.com/images%2Fcgotjh%2Fpost%2F52907c8c-c149-4943-ad21-3996f44f912f%2F995EFF355B74179035.jpg" alt="Protocol">


---

## Reference

▶️ [우아한 Tech - 10분 테코톡 영상 추천] https://www.youtube.com/watch?v=1pfTxp25MA8&t=1912s
📄https://velog.io/@cgotjh/네트워크-OSI-7-계층-OSI-7-LAYER-기본-개념-각-계층-설명
📄https://onecoin-life.com/19  
📄https://velog.io/@hidaehyunlee/데이터가-전달되는-원리-OSI-7계층-모델과-TCPIP-모델
📄https://velog.io/@jsb100800/CS-스터디-네트워크-OSI-7계층
📄https://shlee0882.tistory.com/110  
📄https://backendcode.tistory.com/167