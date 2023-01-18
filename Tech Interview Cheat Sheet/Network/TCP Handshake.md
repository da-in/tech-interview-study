# TCP 3 way handshake & 4 way handshake

## Handshake

**핸드쉐이크(handshake)** 는 본 통신이 시작되기 전에, 두 개체(Client, Server 등)간의 통신 연결 프로토콜 확립을 위한 정보를 교환하는 자동화된 협상 과정이다.

- `Transport Layer`의 TCP(Transmission Control Protocol)는 높은 신뢰성을 보장하는 `연결 지향 프로토콜` 이며 `TCP`에서 통신을 연결할 때에는 `3 way handshake`를 연결 해제할 때에는 `4 way handshake`를 사용한다.
- 암호화 통신 프로토콜인 SSL(Secure Sockets Layer), TSL(Transport Layer Security)는 [TLS/SSL Handshake](https://github.com/da-in/tech-interview-study/blob/main/Network/TLS%20%26%20SSL%20Handshake.md)를 사용한다.

<br/>

## TCP Control Flag

<br/>

<img src="https://user-images.githubusercontent.com/66757141/212956486-1f3449fa-d63f-4fdd-acaf-60e9893a3a50.gif" alt="TCP Header" ><br/>
[_img reference_](https://www.juniper.net/documentation/us/en/software/junos/transport-ip/topics/topic-map/tcp-configure-features.html) TCP Header

<br/>

TCP 헤더는 6bit의 `Control Flag` 필드를 포함한다. 각 플래그의 사용을 `0`과 `1`로 나타낸다. 예 `SYN/ACK`는 `010010`.  
`Sequence Number`는 세그먼트\* 현재 응답 데이터의 순서 번호를 의미한다.  
`Acknowledge Number`는 상대방에게 받아야 할 패킷의 번호를 의미한다.  
`Sequence Number`와 `Acknowledge Number`를 통해 통신 순서를 확인한다.

\* 세그먼트는 4계층의 패킷을 의미한다. 계층별 패킷 구분을 위해 4계층은 `세그먼트`, 3계층은 `패킷`, 2계층은 `프레임` 이라고 칭한다.

<table >
  <tr>
    <th align='left'>SYN (Synchronize)</th>
    <td>연결 요청</td>
    <td>통신 시작을 위해 가장 먼저 보내는 패킷<br/>임의의 초기 `Sequence Number` 를 보낸다.</td>
  </tr>
  <tr>
    <th align='left'>ACK (Acknowledgment)</th>
    <td>응답 플래그</td>
    <td>송신측으로부터 패킷을 받았다는 것을 알려주기 위한 플래그<br/> 일반적으로 받은 `Sequence Number + 1` 하여 응답한다.</td>
  </tr>
  <tr>
    <th align='left'>Fin (Finish)</th>
    <td>연결 종료</td>
    <td>남은 전송 데이터가 없으므로 세션 연결을 종료시키는 플래그</td>
  </tr>
  <tr>
    <th align='left'>RST (Reset)</th>
    <td>재연결</td>
    <td>비정상적인 세션을 끊기 위해 연결을 재설정하는 플래그</td>
  </tr>
  <tr>
    <th align='left'>PSH (Push)</th>
    <td>밀어넣기</td>
    <td>빠른 응답을 위해 버퍼링 없이 OSI 7 Layer의 Application 계층으로<br/>바로 전달하도록 하는 플래그</td>
  </tr>
  <tr>
    <th align='left'>URG (Urgent)</th>
    <td>긴급 데이터</td>
    <td>긴급하게 전해야 할 내용이 있을 경우 사용하는 플래그</td>
  </tr>
</table>

<br/>
<br/>

아래와 같이 `3 way handshake`를 통해 연결을 설정하고 `4 way handshake`를 통해 해제한다.

<img src="https://user-images.githubusercontent.com/66757141/212936124-0627914e-d091-4e7a-9548-a7f2308ec4a7.gif" alt="Image2001"><br/>
[_img reference_](https://www.cablefree.net/support/radio/software/index.php/Manual:Connection_oriented_communication_%28TCP/IP%29)

<br/>

## 3 way handshake

TCP 3 way handshake는 전송의 신뢰성을 보장하기 위해서 통신 이전에 세션을 수립하는 것이다. 양쪽 모두 통신 준비가 되었다는 것을 확인하는 과정이며, 서로의 일련번호를 얻을 수 있다.

1. `Client`가 접속을 요청하는 `SYN` 패킷을 보낸다.
   - `Client`는 `SYN_SENT` 상태가 되어 `SYN/ACK` 응답을 기다린다.
2. `Server`가 요청을 승인하는 `SYN/ACK` 패킷을 보낸다.
   - `Server`는 `SYN_RECEIVED`상태가 되어 `ACK`를 기다린다.
3. `Client`는 `ACK`를 보내고 이 후로부터는 연결이 이루어진다.
   - `Client`와 `Server`는 `ESTABLISHED` 상태가 된다.

<br/>

## 4 way handshake

1. `Client`가 연결 종료를 의미하는 `FIN` 플래그를 보낸다.
   - `Client`는 `FIN_WAIT` 상태가 된다.
2. `Server`가 `FIN`을 받고 확인했다는 `ACK`를 보낸다.
   - `Server`는 `CLOSE_WAIT` 상태가 되어 자신에게 남은 통신이 끝나기를 기다린다.
3. `Server`가 연결 해지 준비가 되었다는 의미로 `FIN` 플래그를 보낸다.
   - `Server`는 `LAST_ACK` 상태가 된다.
4. `Client`가 `FIN`을 받고 확인했다는 `ACK`를 보낸다.
   - `Client`는 바로 세션을 종료시키지 않고 `TIME_WAIT` 상태가 된다. `Server`가 `FIN` 패킷보다 먼저 보냈지만 여러 문제로 상황으로 늦게 도착할 수 있는 잉여 패킷을 기다린다. (default 240초)
   - `Client`와 `Server`가 `CLOSE` 상태가 된다.

`FIN` 플래그로 종료를 요청하는 시점에, Client가 연결을 바로 종료하지 않고 남은 요청을 기다리는 것을 `Half-Close` 기법 이라고 한다.

<br/>

---

## Reference

📄https://velog.io/@averycode/네트워크-TCPUDP와-3-Way-Handshake4-Way-Handshake  
📄https://en.wikipedia.org/wiki/Handshake_(computing)  
📄https://velog.io/@osk3856/TLS-Handshake  
📄https://bangu4.tistory.com/74  
📄https://networkengineering.stackexchange.com/questions/23527/when-does-the-three-way-handshake-take-place-in-relation-to-data-flowing-down-th
