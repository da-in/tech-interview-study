# TCP 3 way handshake & 4 way handshake

## Handshake

**핸드쉐이크(handshake)** 는 본 통신이 시작되기 전에, 두 개체(Client, Server 등)간의 통신 연결 프로토콜 확립을 위한 정보를 교환하는 자동화된 협상 과정이다.

- TCP(Transmission Control Protocol)에서 통신을 연결할 때 `3 way handshake`를 연결 해제할 때 `4 way handshake`를 사용한다.
- 암호화 통신 프로토콜인 SSL(Secure Sockets Layer), TSL(Transport Layer Security)는 [TLS/SSL Handshake](https://github.com/da-in/tech-interview-study/blob/main/Network/TLS%20%26%20SSL%20Handshake.md)를 사용한다.

<br/>

## TCP Control Flag

<img src="" alt="TCP Header" >
[_img reference_](https://www.juniper.net/documentation/us/en/software/junos/transport-ip/topics/topic-map/tcp-configure-features.html) TCP Header

TCP 헤더는 6bit의 `Control Flag` 필드를 포함한다. 각 플래그의 사용을 `0`과 `1`로 나타낸다. 예 `SYN/ACK`는 `010010`.

<table>
  <tr>
    <th>SYN (Synchronize)</th>
    <td>연결 요청</td>
    <td>통신 시작을 위해 가장 먼저 보내는 패킷<br/>임의의 초기 `Sequence Number`를 보낸다.</td>
  </tr>
  <tr>
    <th>ACK (Acknowledgment)</th>
    <td>응답 플래그</td>
    <td>송신측으로부터 패킷을 잘 받았다는 것을 알려주기 위한 플래그이다. 받은 `Sequence Number`에 +1 하여 응답한다.</td>
  </tr>
  <tr>
    <th>Fin (Finish)</th>
    <td>연결 종료</td>
    <td>더 이상 전송할 데이터가 없고 세션 연결을 종료시키겠다는 플래그이다.</td>
  </tr>
  <tr>
    <th>RST (Reset)</th>
    <td>연결 재설정</td>
    <td>비정상적인 세션을 끊기 위해 연결을 재설정하는 과정</td>
  </tr>
  <tr>
    <th>PSH (Push)</th>
    <td>넣기</td>
    <td>버퍼가 채워지기를 기다리지 않고 받는 즉시 전달한다. 버퍼링 없이 7 Layer Application Layer의 응용프로그램에게 바로 전달하는 플래그</td>
  </tr>
  <tr>
    <th>URG (Urgent)</th>
    <td>긴급 데이터</td>
    <td>긴급한 데이터의 우선순위를 다른 데이터의 우선 순위를 높여 긴급하게 전달하는 플래그</td>
  </tr>
</table>

<br/>

`Transport Layer`의 `TCP`는 높은 신뢰성을 보장하는 `연결 지향 프로토콜` 이며 아래와 같이 `3 way handshake`를 통해 연결을 설정하고 `4 way handshake`를 통해 해제한다.

<img src="https://user-images.githubusercontent.com/66757141/212936124-0627914e-d091-4e7a-9548-a7f2308ec4a7.gif" alt="Image2001"><br/>
[_img reference_](https://www.cablefree.net/support/radio/software/index.php/Manual:Connection_oriented_communication_%28TCP/IP%29)

## 3 way handshake

TCP 3 way handshake는 전송의 신뢰성을 보장하기 위해서 통신 이전에 세션을 수립하는 것이다. 양쪽 모두 통신 준비가 되었다는 것을 확인하는 과정이며, 서로의 일련번호를 얻을 수 있다.

1. `Client`가 접속을 요청하는 `SYN` 패킷을 보낸다.
   - `Client`는 `SYN_SENT` 상태가 되어 `SYN/ACK` 응답을 기다린다.
2. `Server`가 요청을 승인하는 `SYN/ACK` 패킷을 보낸다.
   - `Server`는 `SYN_RECEIVED`상태가 되어 `ACK`를 기다린다.
3. `Client`는 `ACK`를 보내고 이 후로부터는 연결이 이루어진다.
   - `Client`와 `Server`는 `ESTABLISHED` 상태가 된다.

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

서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)

TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

<br/>

---

## Reference

📄https://en.wikipedia.org/wiki/Handshake_(computing)  
📄https://velog.io/@osk3856/TLS-Handshake  
📄https://bangu4.tistory.com/74  
📄https://networkengineering.stackexchange.com/questions/23527/when-does-the-three-way-handshake-take-place-in-relation-to-data-flowing-down-th
