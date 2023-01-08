# TLS/SSL Handshake

## SSL이란?
SSL은 웹사이트와 브라우저 사이에서 전송되는 데이터를 암호화하여 인터넷 연결을 보호하기 위한 표준 기술이다.</br>
이를 통해 개인 데이터나 금융데이터 등의 전송되는 정보를 보거나 훔치는 것을 방지한다. </br>



## TLS란?
TLS(전송 계층 보안)는 SSL의 발전된 버전이다. </br>
즉, 인터넷 커뮤니케이션을 위한 개인 정보와 데이터 무결성을 제공하는 보안 프로토콜이다. </br>


## TLS / SSL Handshake
브라우저(사용자)와 웹서버가 안전하게 데이터를 주고받기 위해 필요한 과정. 즉 ,송신자와 수신자가 암호화된 데이터를 교환하기 위한 일련의 협상과정이다. 이 협상과정에는 여러 항목들이 포함된다. </br>
- SSL 인증서 전달
- 대칭키 전달
- 암호화 알고리즘 결정
- TLS/SSL 프로토콜 결정

> SSL(보안 소켓 계층) 인증서는 브라우저와 서버 사이의 암호화된 연결을 수립하는데 사용된다.</br>


## 과정

<img src = "https://user-images.githubusercontent.com/102718303/211181665-6906c3f3-aa1f-426e-a314-780a5a975b67.png">

1. `Client Hello` : Client가 Server에 연결을 시도하며 전송하는 패킷이다.
   - 사용 가능한 **암호화 알고리즘**, 세션 ID, SSL 프로토콜 버전, Random Byte등 전달 
 
2. `Server Hello` : Client가 보내온 `Client Hello` 패킷을 받고, 암호화 알고리즘을 선택해서 Clinet에게 알린다.
   - 자신의 SSL 프로토콜도 같이 보낸다. 
  
3. `Certificate` : server가 `CA`의 개인키로 암호화된 자신의 SSL 인증서를 Client에게 전달한다.
   - 인증서 내부에 Server가 발행한 **공개키**가 들어있다. 
   - Client는 `CA`의 공개키로 복호화한다. -> 성공하면 이 SSL인증서는 `CA`가 서명한 것 확인
   
4. `Server Key Exchange / ServerHello Done` : Server의 공개키가 SSL 인증서에 없는 경우, Server가 직접 전달한다. (있으면 생략) 그리고 Server가 행동을 마쳤음을 전달한다.

5. `Client Key Exchange` : 대칭키를 Client가 생성해서 위에서 얻은 Server의 공개키로 암호화해서 전달한다. 
   - 여기서 전달한 **대칭키**가 `TLS/SSL Handshake`의 목적이다.
   - 이후 이 대칭키를 이용해서 데이터를 암호화하여 교환한다.
  
6. `ChangeCipherSpec / Finished` : 패킷으로 교환할 정보를 모두 교환한 뒤 통신할 준비가 완료되었다고 알린다. </br></br>


> CA(인증 기관)란? - 인증서가 진짜인지 가짜인지 보장해주는 공인된 인증 기관 </br>


----
## Referance
- https://aws-hyoh.tistory.com/entry/HTTPS-%ED%86%B5%EC%8B%A0%EA%B3%BC%EC%A0%95-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3SSL-Handshake
- https://steady-coding.tistory.com/512

