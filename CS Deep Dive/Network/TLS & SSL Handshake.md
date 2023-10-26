# TLS/SSL Handshake

## SSL (Secure Socket Layer)
- SSL은 웹 서버와 클라이언트 사이에서 전송되는 데이터를 암호화하여 보호하기 위한 통신 암호화 프로토콜이다.
- SSL이 적용된 경우 사용자의 개인 정보나, 금융 데이터들이 암호화 되므로 안전한 통신이 가능하다.

</br>

## TLS (Transport Layer Security)
- TLS는 SSL의 발전된 버전이다.
- 즉, SSL과 동일하게 전송되는 데이터의 무결성을 제공하는 보안 프로토콜이다. </br>

> TLS가 더 보완된 버전이지만 SSL이 일반적으로 사용되는 용어이고, 보안 인증서는 여전히 SSL이라고 한다.  

</br>

*[자세한 SSL/TLS 참고](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Network/HTTP%26HTTPS.md)*

</br>

## TLS / SSL Handshake
TLS/SSL 연결을 하고 클라이언트와 웹서버가 안전하게 데이터를 주고받기 위해 필요한 과정이다. 즉, 송신자와 수신자가 암호화된 데이터를 교환하기 위한 일련의 협상과정이다. </br>
- SSL 인증서 전달
- 대칭키 전달
- 암호화 알고리즘 결정
- TLS/SSL 프로토콜 결정

> SSL(보안 소켓 계층) 인증서는 클라이언트와 서버 사이의 암호화된 연결을 수립하는데 사용된다.</br>


## 과정

<img width = "680" src = "https://user-images.githubusercontent.com/102718303/211181665-6906c3f3-aa1f-426e-a314-780a5a975b67.png">

1. `Client Hello` 요청
   - Client가 특정 주소에 접근하면, 해당 Server에 연결을 시도하며 전송하는 패킷이다.
   - 해당 패킷에는 아래의 정보들이 포함되어 있다.
      - 난수 데이터
      - SSL 프로토콜 버전
      - 데이터 암호화 알고리즘
      - 세션 ID
 
2. `Server Hello` 응답
   - Client가 보내온 `Client Hello` 패킷을 받고, 암호화 알고리즘을 선택해서 Clinet에게 응답 패킷을 보낸다.
   - 해당 패킷에는 아래의 정보들이 포함되어 있다.
      - 난수 데이터
      - 데이터 암호화 알고리즘
      - 인증서 (Certificate)
  
3. 인증서 검토
   - Server가 보낸 인증서 속 `CA`의 공개키로 암호화된 SSL 인증서를 복호화하여 서명을 확인한다.
   - Client는 인증서 내부에 Server가 발행한 **공개키**를 확인한다.


4. `Client Key Exchange` 
   - Client가 대칭키를 생성한 후 위에서 얻은 Server의 공개키로 암호화해서 전달한다. 
   - 여기서 전달한 **대칭키**가 `TLS/SSL Handshake`의 목적이다.
   - 이후 이 대칭키를 이용해서 데이터를 암호화하여 교환한다.
  
6. `ChangeCipherSpec / Finished`
   - 서로가 교환할 정보를 모두 교환한 뒤 통신할 준비가 완료 되었다고 알리는 패킷을 보낸다.
   - TLS HandShake가 종료된다.

</br>

> CA(인증 기관)란 인증서가 진짜인지 가짜인지 보장해주는 공인된 인증 기관이다. </br>

</br>

----
## Referance
- https://aws-hyoh.tistory.com/entry/HTTPS-%ED%86%B5%EC%8B%A0%EA%B3%BC%EC%A0%95-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3SSL-Handshake
- https://steady-coding.tistory.com/512
- https://velog.io/@osk3856/TLS-Handshake
- https://blog.itcode.dev/posts/2021/08/18/about-ssl

