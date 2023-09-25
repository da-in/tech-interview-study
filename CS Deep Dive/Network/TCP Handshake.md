# TCP 3 way handshake & 4 way handshake

## Handshake

**핸드쉐이크(handshake)** 는 TCP 통신이 시작되기 전에, 클라이언트와 서버간의 통신 프로토콜 확립을 위해 정보를 교환하는 자동화된 협상 과정이다.

- 전송계층의 **TCP(Transmission Control Protocol)** 는 높은 신뢰성을 보장하는 연결 지향 프로토콜이다.
- TCP에서 통신을 연결할 때에는 `3 way handshake`를, 연결 해제할 때에는 `4 way handshake`를 사용한다.
- 암호화 통신 프로토콜인 SSL(Secure Sockets Layer), TSL(Transport Layer Security)는 [TLS/SSL Handshake](https://github.com/da-in/tech-interview-study/blob/main/Network/TLS%20%26%20SSL%20Handshake.md)를 사용한다.

<br/>

## Port 상태 정보
- CLOSED: 포트가 닫힌 상태
- LISTEN: 포트가 열린 상태로 연결 요청 대기 중
- SYN_RCV: SYNC 요청을 받고 상대방의 응답을 기다리는 중
- ESTABLISHED: 포트 연결 상태

</br>

## TCP Flag 정보

- TCP 헤더는 6bit의 `Control Bit(Flag Bit)` 필드를 포함한다.
- 비트는 각각 `URG-ACK-PSH-RST-SYN-FIN` 의 의미를 가지고, 각 플래그의 사용을 `0`과 `1`로 나타낸다.(ex.`SYN/ACK`는 `010010`).    

</br>

<table >
  <tr>
    <th align='left'>URG (Urgent)</th>
    <td>긴급 데이터</td>
    <td>긴급하게 전해야 할 내용이 있을 경우 사용하는 플래그</td>
  </tr>
  <tr>
    <th align='left'>ACK (Acknowledgment)</th>
    <td>응답 플래그</td>
    <td>송신측으로부터 패킷을 받았다는 것을 알려주기 위한 플래그<br/> 일반적으로 받은 'Sequence Number + 1' 하여 응답한다.</td>
  </tr>
  <tr>
    <th align='left'>PSH (Push)</th>
    <td>밀어넣기</td>
    <td>빠른 응답을 위해 버퍼링 없이 OSI 7 Layer의 Application 계층으로<br/>바로 전달하도록 하는 플래그</td>
  </tr>
  <tr>
    <th align='left'>RST (Reset)</th>
    <td>재연결</td>
    <td>비정상적인 세션을 끊기 위해 연결을 재설정하는 플래그</td>
  </tr>
  <tr>
    <th align='left'>SYN (Synchronize)</th>
    <td>연결 요청</td>
    <td>통신 시작을 위해 가장 먼저 보내는 패킷<br/>임의의 초기 'Sequence Number' 를 보낸다.</td>
  </tr>
  <tr>
    <th align='left'>FIN (Finish)</th>
    <td>연결 종료</td>
    <td>남은 전송 데이터가 없으므로 세션 연결을 종료시키는 플래그</td>
  </tr>
</table>

</br>

- `Sequence Number`는 *세그먼트 데이터의 순서 번호를 의미한다.  
- `Acknowledge Number`는 상대방에게 받아야 할 패킷의 번호를 의미한다.  
- `Sequence Number`와 `Acknowledge Number`를 통해 통신 순서를 확인한다.  

\**세그먼트는 4계층의 패킷을 의미한다. 계층별 패킷 구분을 위해 4계층은 `세그먼트`, 3계층은 `패킷`, 2계층은 `프레임` 이라고 칭한다.*

<br/>

## 3 way handshake

TCP 3 way handshake는 전송의 신뢰성을 보장하기 위해서 통신 이전에 세션을 수립하는 것이다. 양쪽 모두 통신 준비가 되었다는 것을 확인하는 과정이며, 서로의 일련번호를 얻을 수 있다.

</br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F225A964D52F1BB6917"><br/>
[_img reference_](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)

</br>

1. `Client`가 접속을 요청하는 `SYN` 패킷을 보낸다.
   - `Client`는 `CLOSED -> SYN_SENT` 상태가 되어 `SYN/ACK` 응답을 기다린다.
   - `Server`는 `LISTEN` 
2. `Server`가 요청을 승인하는 `SYN/ACK` 패킷을 보낸다.
   - `Client`는 패킷을 받고 `SYN_SENT -> ESTABLISHED` 상태가 된다.
   - `Server`는 `LISTEN -> SYN_RCV`상태가 되어 `ACK`를 기다린다.
4. `Client`는 `ACK`를 보내고 이 후로부터는 연결이 이루어진다.
   - `Server`는 패킷을 받고 `ESTABLISHED` 상태가 된다.

<br/>


## 4 way handshake

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2152353F52F1C02835"><br/>
[_img reference_](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)

</br>

1. `Client`가 `CLOSED`를 호출하고, 연결 종료를 의미하는 `FIN` 플래그를 보낸다.
   - `Client`는 `FIN_WAIT` 상태가 된다.
2. `Server`가 `FIN`을 받고 확인했다는 `ACK`를 보낸다.
   - `Server`는 `CLOSE_WAIT` 상태가 되어 자신에게 남은 통신이 끝나기를 기다린다.
   - `Client`는 `FIN_WAIT_2` 상태가 된다.
3. `Server`가 연결 해지 준비가 되었다는 의미로 `FIN` 플래그를 보낸다.
   - `Server`는 `LAST_ACK` 상태가 된다.
4. `Client`가 `FIN`을 받고 확인했다는 `ACK`를 보낸다.
   - `Client`는 바로 세션을 종료시키지 않고 `TIME_WAIT` 상태가 된다. `Server`가 `FIN` 패킷보다 먼저 보냈지만 여러 문제로 상황으로 늦게 도착할 수 있는 잉여 패킷을 기다린다. (default 240초)
   - `Client`와 `Server`가 `CLOSE` 상태가 된다.

\**`FIN` 플래그로 종료를 요청하는 시점에, Client가 연결을 바로 종료하지 않고 남은 요청을 기다리는 것을 `Half-Close` 기법 이라고 한다.*

<br/>

---

## Reference

📄https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake  
📄https://en.wikipedia.org/wiki/Handshake_(computing)  
📄https://velog.io/@osk3856/TLS-Handshake  
📄https://bangu4.tistory.com/74  
📄https://networkengineering.stackexchange.com/questions/23527/when-does-the-three-way-handshake-take-place-in-relation-to-data-flowing-down-th
