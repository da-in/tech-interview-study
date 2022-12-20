# **HTTP & HTTPS**

<img width="678" alt="스크린샷 2022-12-19 오후 8 25 35" src="https://user-images.githubusercontent.com/70997596/208444128-bd5296d4-54d5-4e5e-8938-08e0b87bf5dd.png">


## **HTTP**(Hypertext Transfer Protocol)  
서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜이다.  
HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, 80번 포트를 사용하고 있다.  

### **HTTP** 구조
- HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다.  
- HTTP는 상태를 가지고 있지 않는 Stateless 프로토콜이며 Method, Path, Version, Headers, Body 등으로 구성된다.

### **HTTP** 단점
 HTTP는 암호화가 되지 않은 평문 데이터를 전송하는 프로토콜이였기 때문에  
 HTTP로 비밀번호나 주민등록번호 등을 주고 받으면 제3자가 정보를 조회할 수 있다.

## **HTTPS**(Hypertext Transfer Protocol Secure)
HTTP에 데이터 암호화가 추가된 프로토콜이다.(SSL)  
HTTPS는 HTTP와 다르게 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.

### **SSL**이 뭐에요?
>SSL(Secure Sockets Layer)은 암호화 기반 인터넷 보안 프로토콜이다.  
>인터넷 통신의 개인정보 보호, 인증, 데이터 무결성을 보장하기 위해 Netscape가 1995년 처음으로 개발했다.  
>SSL은 현재 사용 중인 TLS 암호화의 전신이다.

- TLS는 뭐에요..? -> TLS: 전송 계층 보안(Transport Layer Security, TLS)  
  TLS는 가장 최신 기술로 더 강력한 버전의 SSL이다.  
  그러나 SSL이 더 일반적으로 사용되는 용어라서, 여전히 보안 인증서는 SSL이라 불린다.  
  아니면 'SSL/TLS 암호화' 이렇게 표기한다.  
  [TLS 참고 링크](https://www.cloudflare.com/ko-kr/learning/ssl/transport-layer-security-tls/)

### **SSL** 작동 방식
SSL은 바로 **"공개키 암호화 방식"**을 이용해서 문서를 보안한다.  
이 방식의 핵심은 바로 공개키와 개인키가 있는 것인데,  
**공개키**는 누구에게나 공개되어 "모두가 접근이 가능한 키"고  
**개인키**는 딱 한 사람만이 소유해 "본인을 제외한 누구도 접근이 불가능한 키"다.

**SSL 흐름**
1. 서버는 공개키와 개인키를 만든다.
2. 믿을만한 저장소(CA)와 계약해 두 키를 관리하도록 한다.
    - *CA: Certificate Authority로, 공개키를 저장해주는 신뢰성이 검증된 민간기업*
3. CA도 자신만의 공개키와 개인키를 가지고 자체 암호화를 하여 SSL 인증서를 발급한다.
4. 클라이언트의 데이터 요청이 들어오면 서버는 CA에서 만든 SSL 인증서를 보내준다.
5. 클라이언트는 CA의 공개키를 이용해 SSL 인증서를 복호화(암호 해독)한다.
6. SSL 내부의 서버 공개키를 이용해서 암호화해서 인증서를 서버에게 보낸다.
7. 서버는 개인키로 암호화된 인증서를 복호화(암호 해독)하고 다시 암호화 하여 클라이언트에게 보낸다.

### HTTPS 흐름
1. 서버(A)를 만드는 기업은 HTTPS를 위해 공개키와 개인키를 만든다.

2. 신뢰할 수 있는 CA 기업에게 서버 공개키 관리를 부탁하며 계약을 한다.

3. 계약 완료된 CA 기업은 A기업의 이름, A서버 공개키, 공개키 암호화 방법을 담은 인증서를 만들고,  
그 인증서를 CA 기업의 개인키로 암호화해서 A서버에게 제공한다.

4. A서버는 암호화된 인증서를 갖게 되고, A서버의 공개키로 암호화된 HTTPS 요청이 아닌 요청이 오면,  
암호화된 인증서를 클라이언트에게 준다.

5. 클라이언트 입장에서, A서버로 example.exe 파일 조회를 요청한다.  
HTTPS 요청이 아니기 때문에 CA기업이 A서버의 정보를 CA 기업의 개인키로 암호화한 인증서를 받게된다.

6. CA 기업의 공개키는 브라우저가 이미 알고있다. (세계적으로 신뢰할 수 있는 기업으로 등록되어 있기 때문에, 브라우저가 인증서를 탐색하여 해독이 가능한 것)

7. 브라우저는 해독한 뒤 A서버의 공개키를 얻게 되었다.

8. 이제 A서버와 통신할 때는 A서버의 공개키로 암호화해서 요청을 날리게 된다.

### HTTPS 다른 장점

- 검색엔진 최적화(SEO)에 있어서도 큰 혜택을 볼 수 있다.

    - 구글에서는 HTTPS를 사용하는 웹사이트에 대해서 검색 순위 결과에 약간의 가산점을 주겠다고 발표

- 가속화된 모바일 페이지(AMP, Accelerated Mobile Pages)를 만들 수 있다.

    - AMP를 만들기 위해서는 HTTPS 프로토콜을 사용해만 한다.

## 출처
https://mangkyu.tistory.com/98  
https://fomaios.tistory.com/entry/Network-HTTPS%EC%9D%98-%EB%B3%B4%EC%95%88-%EC%9B%90%EB%A6%ACfeat-SSL%EA%B3%B5%EA%B0%9C%ED%82%A4-%EC%95%94%ED%98%B8%ED%99%94-%EB%B0%A9%EC%8B%9D  
https://www.cloudflare.com/ko-kr/learning/ssl/what-is-ssl/  
https://github.com/Songwonseok/CS-Study/blob/main/Network/HTTP%26HTTPS.md
