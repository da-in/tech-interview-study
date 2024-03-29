# TCP & UDP

## 개념
OSI 7계층 중 Layer 4 : 전송계층은 프로토콜 내에서 송신자와 수신자를 연결하는 통신 서버를 제공하는 계층이다. </br>
이 전송계층에서 사용되는 \*프로토콜이 **TCP 와 UDP**이다.

\**프로토콜 : 클라이언트와 서버가 정보를 교환할 수 있도록 하는 **메세지 형식에 대한 규칙***

</br>

## TCP란?
- TCP (Transmission Control Protocol)는 신뢰성 있는 데이터 전송을 지원하는 연결 지향형 프로토콜
- 일반적으로 IP 와 TCP가 같이 사용된다.
    - IP는 인터넷 망 속에서 IP 주소와 패킷과 같은 규칙을 통해 통신을 하는 것이다.
    - TCP는 IP의 여러 단점들을 커버해, 패킷 전송을 제어 및 관리하여 신뢰성을 보증하게 한다.
- TCP는 **3-way Handshake** 과정을 통해 연결 후 통신을 시작
- \*흐름제어와 \*혼잡제어를 지원하며 데이터의 순서를 보장한다. </br>

\**흐름 제어 : 보내는 쪽과 받는 쪽의 데이터 처리 속도 차이를 조절해주는 것* </br>
\**혼잡 제어 : 네트워크 내의 패킷 수가 넘치게 증가하지 않도록 방지하는 것*

</br>

## TCP 포장?
- TCP의 개념이 잘 안 와닿는다면 택배를 생각해보자
  - IP는 그냥 배달 주소지 정보라면, TCP는 주소지 뿐만 아니라 순서, 검증, 전송 제어 정보까지 들어있는 것이다.
  - 즉, TCP를 통해 목적지까지 안전 배달를 보증한다.
- 데이터를 TCP로 포장 -> 포장한 데이터를 IP로 포장 -> 포장한 데이터를 이더넷 포장 -> 목적지 도착
<img width="700" src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*xH3GtxFnlu3P5S6Xc9CyTA.png">


## 특징
- 연결형 서비스로 *가상 회선 방식을 제공
- 통신 시작(3-way Handshaking)과 통신 해제(4-way Handshaking)
- 전송 제어 기법 3가지를 통한 패킷 관리
  - 흐름 제어
  - 혼잡 제어
  - 오류 제어
- 데이터의 전송 순서 보장
  - 각 바이트마다 번호를 부여
- \*데이터의 경계를 구분하지 않는다.
- 신뢰성 있는 데이터 전송
- UDP보다 전송속도 느림
</br>

\**세그먼트 : 전송 계층에서의 데이터 단위이고, 각각에 TCP 헤더가 포함된 패킷의 깨진 조각이다.* </br>
\**가상 회선 방식 : TCP는 데이터를 전송하기 전에 각각의 기기마다 3-way Handshaking을 통해 논리적 연결을 수립하는데, 이를 가상 회선이라고 한다. (물리적인 연결은 아니다.)*

</br>

### *데이터의 경계

- 데이터 경계란 데이터를 보낼 때 여러번에 걸쳐 보낼 수 있는지의 여부이다.
</br>
<img width="440" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbC7MyJ%2FbtrrdcfQ1Ud%2FAcNHcEKS3kjMGtKZHLXjF0%2Fimg.png">

위의 사진의 첫번째 경우 처럼 송신 함수의 호출 횟수와 수신 함수의 호출 횟수가 일치 해야하는 경우는 **데이터의 경계가 있는 경우**이다. </br>
반대로 두번째 경우는 송신 함수의 호출 횟수와 수신 함수의 호출 횟수가 일치 하지 않아도 되는 **데이터의 경계가 없는 경우**이다. </br>

</br>

</br>

## UDP란?
> 인터넷 기술이 발전하면서 동영상이나 음악도 전송하게 되었고, 데이터의 크기가 점점 커짐과 동시에 빠른 통신이 필요하게 되었다.</br>
> HTTP 2.0에서는 한 번 연결된 TCP 회선을 길게 유지하고 데이터도 스트림이라는 특수한 형태로 보내는 식으로 극복 했지만, TCP가 가지는 근본적인 특징 때문에 결과적으론 속도 한계가 있었다.</br>
> 속도가 빠른 UDP를 사용하자!
- UDP(User Datagram Protocol)는 비연결형 프로토콜이다.
- 데이터그램 방식을 사용하는 프로토콜이기 때문에 각각의 패킷 간의 순서가 존재하지 않는 독립적인 패킷을 사용
- TCP 처럼 연결&해제 설정 없이 보내는 쪽에서 일방적으로 데이터를 전송하는 통신 프로토콜
- 혼잡제어를 지원하지 않기 때문에 속도는 빠르지만 패킷 손실이 발생할 수 있다.

</br>

## 특징
- 비연결형 서비스로 \*데이터그램 방식을 제공
- 비신뢰성
- 데이터의 경계를 구분
- 패킷 오버헤드가 적어 네트워크 부하 감소
- 혼잡 제어를 하지 않기 때문에 TCP보다 빠르다
- 연결 설정이 없다. </br>

\**데이터그램이란? - 네트워킹에서 전송되는 데이터 단위이고, UDP는 신뢰성보다 데이터 전송이 중요하므로 헤더와 출도착 주소, 데이터만 담고 있다.(독립적인 관계를 가지는 패킷이라는 의미로도 사용된다.)* </br>
\**비연결형이기 때문에 할당되는 논리적인 경로가 없다. 따라서 각 패킷이 다른 경로로 전송되고, 독립적인 관계를 가진다. 독립적인 관계란 데이터가 순서대로 오는지 알 수 없다는 의미와 같다.*

</br>

## TCP vs UDP

|| TCP | UDP |
|-----|-----|-----|
| 연결 방식 | 연결형 프로토콜 | 비열결형 프로토콜 |
| 전송 순서 | 보장함 | 보장하지 않음 |
| 데이터 경계 | 구분함 | 구분하지 않음 |
| 신뢰성 | 신뢰성있는 데이터 전송 | 비신뢰성 데이터 전송 |
| 패킷 | 세그먼트| 데이터그램 |
| 전송 속도 | 느림 | 빠름 |
| 통신 | 1:1 | 1:1, 1:N, N:N |

</br>

<img width="650" src="https://user-images.githubusercontent.com/102718303/214200303-9e9a9025-51e5-4693-a805-12f73b241234.png">

</br>

## HTTP3.0 과 UDP를 개조한 QUIC 프로토콜
- QUIC(Quick UDP Internet Connections)는 UDP를 기반으로 TCP + TLS + HTTP의 기능을 모두 구현하는 프로토콜이다.
- HTTP 3.0 부터는 TCP 대신 QUIC 프로토콜 채택하였다.
- QUIC은 TCP를 사용하지 않기 때문에 3 Way Handshake 과정을 거치지 않아도 된다.
- QUIC은 첫 연결 설정에 \*1 RTT만 소요된다. (TCP는 3 RTT 필요)
- 패킷 손실 감지에 걸리는 시간을 단축할 수 있다.

\**RTT(Round Trip Time) : 클라이언트가 보낸 요청을 서버가 처리한 후 다시 클라이언트로 응답해주는 사이클*

</br>

------ 
## Referance
- https://cocoon1787.tistory.com/757
- https://coding-factory.tistory.com/614
- https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4
- https://badayak.com/entry/tcpip%EC%99%80-udpip-%ED%86%B5%EC%8B%A0-%EC%B0%A8%EC%9D%B4%EC%A0%90
- https://yoon1fe.tistory.com/165
- https://inpa.tistory.com/entry/NW-%F0%9F%8C%90-%EC%95%84%EC%A7%81%EB%8F%84-%EB%AA%A8%ED%98%B8%ED%95%9C-TCP-UDP-%EA%B0%9C%EB%85%90-%E2%9D%93-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EC%9E%90
- https://www.baeldung.com/cs/networking-packet-fragment-frame-datagram-segment
- https://rural-mouse.tistory.com/35



