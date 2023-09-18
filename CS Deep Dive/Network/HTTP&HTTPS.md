# **HTTP & HTTPS**

<img width="678" alt="스크린샷 2022-12-19 오후 8 25 35" src="https://user-images.githubusercontent.com/70997596/208444128-bd5296d4-54d5-4e5e-8938-08e0b87bf5dd.png">


## **HTTP**(Hypertext Transfer Protocol)  
HTTP는 인터넷에서 *하이퍼텍스트를 교환하기 위한 통신 규약으로, 80번 포트를 사용하고 있다. </br> 
사용자가 브라우저를 통해 어떤 서비스를 **요청**하면 서버에서 적절한 결과를 찾아 사용자에게 **응답**하는 방식으로 동작한다.


\**하이퍼 텍스트 : 인터넷 사용자가 필요한 정보의 자유로운 검색을 가능하도록 해주는 텍스트 전개 방식이다.* </br>

> HTML 문서만이 HTTP 통신을 위한 유일한 정보 문서는 아니다. </br>
> Plain text로 부터 JSON 데이터 및 XML과 같은 형태의 정보도 주고 받을 수 있으며, 보통은 클라이언트가 어떤 정보를 HTML 형태로 받고 싶은지, JSON 형태로 받고 싶은지 명시해주는 경우가 많다.

</br>


### **HTTP** 특징
- HTTP는 응용계층의 프로토콜로 TCP/IP 위에서 작동한다.  
- HTTP는 *서버/클라이언트 모델을 따라 상호간의 데이터를 주고 받는다.  
- HTTP는 상태를 가지고 있지 않는 Stateless(무상태) 프로토콜이다.
- HTTP 메세지는 Method, Path, Version, Headers, Body 등으로 구성된다.

\**서버/클라이언트 모델 : 클라이언트가 요청을 생성하기 위한 연결을 연 다음 서버로부터 응답을 받을 때까지 연결을 유지하는 구조이다.*

</br>

<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc7mI3U%2FbtqWX45M76d%2FgGoVLK6rcUJhekrxMcq6a1%2Fimg.png">


### **HTTP** 단점
- 암호화가 되지 않은 평문 데이터를 전송하는 프로토콜이기 때문에 제3자가 중간에서 정보를 조회할 수 있다.
- 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
- 정보의 변조가 가능하다.


## **HTTPS**(Hypertext Transfer Protocol Secure)
HTTPS 는 HTTP 통신의 취약점을 보완하여 세션 데이터를 SSL이나 TLS 프로토콜로 암호화하고, SSL 프로토콜 위에서 동작한다. </br>
HTTPS는 HTTP와 다르게 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 데이터 암호화를 지원한다.

</br>

#### ***SSL**
- SSL(Secure Sockets Layer)은 **암호화 기반 인터넷 보안 프로토콜**이다.  
- 인터넷 통신의 개인정보 보호, 인증, 데이터 무결성을 보장하기 위해 Netscape가 1995년 처음으로 개발했다.  
- SSL은 현재 사용 중인 TLS 암호화의 전신이다.


#### ***TLS**
- TLS(Transport Layer Security)는 전송 계층 보안 
- TLS는 가장 최신 기술로 더 강력한 버전의 SSL이다.  
- SSL이 더 일반적으로 사용되는 용어이기 때문에, 여전히 보안 인증서는 'SSL' 혹은 'SSL/TLS 암호화'로 표기한다.  
  [TLS 참고 링크](https://www.cloudflare.com/ko-kr/learning/ssl/transport-layer-security-tls/)

</br>

### **SSL 암호화 방식**
- SSL은 ***공개키 암호화 방식**을 이용해서 문서를 암호화한다. </br>
- 도청에 의해 개인키를 빼앗기진 않지만, 공개키의 진위여부를 증명할 수 없는 문제가 있다.
- 따라서 인증기관(CA)를 이용한다.

\**공개키 암호화 방식 : **공개키**(누구에게나 공개되어 "모두가 접근이 가능한 키")와 **개인키**(딱 한 사람만이 소유해 "본인을 제외한 누구도 접근이 불가능한 키")를 이용하여 암복호화한다.*

</br>

#### SSL 동작 흐름
1. 서버는 공개키와 개인키를 만든다.
2. 믿을만한 ***인증기관(CA)** 과 계약 후 두 키를 관리하도록 한다.
3. CA도 자신만의 공개키와 개인키를 가지고 자체 암호화를 하여 서버의 공개키를 포함한 SSL 인증서를 발급한다.
4. 클라이언트가 브라우저에 접속하면 서버는 CA에서 만든 SSL 인증서를 보내준다.
5. 클라이언트는 CA의 공개키를 이용해 SSL 인증서를 복호화한다.
6. 복호화가 성공한다면 인증서가 CA 기업으로부터 왔음을 확인하고, 검증된 공개키를 얻을 수 있다.

\**CA: Certificate Authority로, 공개키를 저장해주는 신뢰성이 검증된 민간기업*

</br>

### **HTTPS 동작 흐름**
1. 서버(A)를 만드는 기업은 HTTPS를 위해 공개키와 개인키를 만든다.
2. 신뢰할 수 있는 CA 기업에게 서버 공개키 관리를 부탁하며 계약을 한다.
3. 계약 완료된 CA 기업은 A기업의 이름, A서버 공개키, 공개키 암호화 방법을 담은 인증서를 만들고, 그 인증서를 CA 기업의 개인키로 암호화(디지털 서명)해서 A서버에게 제공한다.
4. A서버는 암호화된 인증서를 갖게 되고, A서버의 공개키로 암호화된 HTTPS 요청이 아닌 다른 요청이 오면,  
암호화된 인증서를 클라이언트에게 보낸다.
5. 클라이언트는 CA 기업의 공개키를 사용하여 인증서를 복호화하여 A서버의 공개키를 얻을 수 있다.
6. 클라이언트는 대칭키를 만든 후 A서버의 공개키를 이용해 암호화 한 후 A서버에 전달한다.
7. A서버는 개인 키로 복호화하여 대칭키를 얻을 수 있다.
8. 이후 A서버와 통신할 때, 대칭키로 암호화하여 요청을 날린다.

> 많은 브라우저가 주요 인증 기관(CA)의 공개키를 사전에 내장한 상태로 제품을 출시한다.

<img width="450" src="https://t1.daumcdn.net/cfile/tistory/993364345C457AED30">


### HTTPS 단점
- HTTPS는 SSL을 사용하기 때문에 처리 속도가 늦어진다. (HTTP에 비해 약 2~100배 정도 느리다)
- HTTPS를 지원한다고 해서 무조건 안전한 것은 아니다. 신뢰할 수 있는 CA 기업이 아니라 자체적으로 인증서를 발급할 수도 있고, 신뢰할 수 없는 CA 기업을 통해서 인증서를 발급받을 수도 있기 때문이다.

</br>

----

## 출처
- https://mangkyu.tistory.com/98  
- https://fomaios.tistory.com/entry/Network-HTTPS%EC%9D%98-%EB%B3%B4%EC%95%88-%EC%9B%90%EB%A6%ACfeat-SSL%EA%B3%B5%EA%B0%9C%ED%82%A4-%EC%95%94%ED%98%B8%ED%99%94-%EB%B0%A9%EC%8B%9D  
- https://www.cloudflare.com/ko-kr/learning/ssl/what-is-ssl/  
- https://github.com/Songwonseok/CS-Study/blob/main/Network/HTTP%26HTTPS.md
- https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
- https://mkil.tistory.com/488
- https://goodgid.github.io/TLS-SSL/

