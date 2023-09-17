# 웹 서버(WS)와 웹 어플리케이션 서버(WAS)

웹 서버(WS)와 웹 어플리케이션 서버(WAS)는 서버를 구성하는 기초적인 개념이지만 혼동하기 쉽다. 웹서버와 WAS의 차이점을 살펴본다.

<br/>

## 정적 페이지와 동적 페이지

WS와 WAS의 차이점을 알기 위해서는 정적 페이지(Static Page)와 동적 페이지(Dynamic Page)에 대하여 알아야한다.

### 정적 페이지(Static Page)

요청한 자원의 경로와 일치하는, 서버에 미리 저장된 파일이 그대로 전달되는 웹페이지를 말한다.  
항상 동일한 페이지를 반환한다.  
ex | `image`, `html`, `css`, `javascript` 파일과 같이 하드웨어에 저장되어 있는 파일들.

### 동적 페이지(Dynamic Page)

클라이언트의 요청 인자에 따라 스크립트에 의해 동적으로 생성 후 반환되는 페이지를 의미한다.

![68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7374617469632d76732d64796e616d69632e706e67](https://user-images.githubusercontent.com/66757141/207196961-3209cb84-7a12-455f-b496-3dae343526e6.png)

<br/>

## Web Server

웹 서버(WS)란 HTTP 프로토콜을 기반으로 클라이언트의 요청을 받아 **정적 컨텐츠**를 제공하는 서버이다.  
정적 컨텐츠란 위에서 설명한 것과 같이 단순 HTML 문서, CSS, 이미지, 파일 등 즉시 응답 가능한 컨텐츠이다.

웹 서버가 정적 컨텐츠가 아닌 동적 컨텐츠를 요청받으면 WAS에 해당 요청을 넘겨주고, WAS에서 처리한 결과를 클라이언트에게 전달하는 역할도 한다.

웹 서버에는 Apache, Nginx, IIS, WebtoB 등이 있다.

<br/>

## WAS(Web Application Server)

![68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7765627365727665722d76732d776173312e706e67](https://user-images.githubusercontent.com/66757141/207196948-32b1f31c-1ccc-4a54-a375-6690f49657a9.png)

WAS(Web Application Server)란 DB 조회 혹은 다양한 로직 처리를 요구하는 동적 컨텐츠를 제공하기 위해 만들어진 Application 서버이다.  
HTTP 프로토콜을 기반으로 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로서, 주로 데이터베이스 서버와 같이 수행된다.

WAS는 `Web Server` + `Web Container*` 이다.  
WAS 별로 다양한 종류의 컨테이너를 내장하고 있으며, 이들 중 서블릿에 관련된 기능을 모아 놓은 것을 서블릿 컨테이너라 부른다.

_\* **Container**란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다._  
_\*\* **JSP**는 Java 언어를 기반으로 하는 Server Side 스크립트 언어이다. HTML에 JAVA 코드를 넣어 동적인 웹을 생성할 수 있도록 하는 웹 어플리케이션 도구이다._  
_\*\* **Servlet**은 WAS의 서블릿 컨테이너 내에서 관리되며 연산을 담당한다. JSP로 작성된 프로그램은 Servlet으로 변환된다._

_\* **Web Container**는 Java 서블렛과 상호작용하는 WAS의 구성요소이다. 서블릿의 생명 주기를 관리(초기화, 메소드 호출, 가비지 컬렉션)하고, 서블릿과 웹서버의 통신과 멀티스레딩을 지원하며 선언적 보안 관리가 가능하게 한다._  
_\* Java가 아닌 PHP, Perl, Python등의 언어는 Apache를 통해 CGI(Common Gateway Interface)를 적용시켜 컨테이너의 역할을 수행할 수 있다._

WAS는 웹 서버의 기능들을 구조적으로 분리하여 처리하고자 하는 목적으로 제시되었으며 주로 다음과 같은 기능을 수행한다.
- Servlet과 JSP 실행을 통한 동적 관리
- 웹 어플리케이션의 세션 생성, 저장, 무효화 등의 세션 관리
- HTTPS 지원, 인증, 데이터 암호화 등의 보안 기능
- 데이터베이스 연결 관리
- 클러스터링과 로드 밸런싱
- 에러와 예외 처리
- 로깅과 모니터링

WAS에는 Tomcat*, WebLogic, WebSphere, Jeus, JBoss 등이 있다.

_\*Apache Tomcat 은 WAS(Tomcat)가 웹 서버(Apache) 기능을 포함하고 있기 때문에 Apache Tomcat 이라고 부르기도 하고, 실제로 WAS 앞에 웹 서버를 두어서 Apache Tomcat 이라고 부르기도 한다._

<br/>

## Web Server와 WAS를 분리하는 이유.

대부분의 WAS는 정적인 컨텐츠를 제공할 수 있기 때문에 웹 서버를 포함하는 개념이고, 웹 서버 없이도 존재할 수 있다. 그럼에도 웹 서버와 WAS를 분리하여 사용하는 이유는 다음과 같다.

1. **서버 부하 방지**  
   WAS와 웹 서버를 분리하여 서버의 부하를 줄일 수 있다. WAS는 DB 조회나 다양한 로직을 처리하고, 웹 서버에서는 단순한 정적 컨텐츠를 처리하도록 분리하여 부하를 줄일 수 있다. 만약 정적 컨텐츠까지 WAS가 처리한다면 부하가 커지고 수행 속도가 느려질 것이다.

2. **보안 강화**  
   클라이언트와 연결하는 포트가 직접 WAS에 연결이 되어 있다면 중요한 설정 파일들이 노출될 수 있기 때문에 WAS 설정 파일을 외부에 노출시키지 않는다.
   웹 서버와 WAS에 접근하는 포트가 다르기 때문에 WAS에 들어오는 포트에는 방화벽을 쳐서 보안을 강화할 수도 있다.

3. **여러 대의 WAS 연결 가능**  
   `로드 밸런싱`을 위해 웹 서버를 사용할 수 있다. 여러 개의 서버를 사용하는 대용량 웹 어플리케이션의 경우 웹 서버와 WAS를 분리하여 `무중단 운영을 위한 장애 극복`에 쉽게 대응할 수 있다.

4. **여러 웹 어플리케이션 서비스 가능**  
   하나의 서버에서 PHP, JAVA 애플리케이션을 함께 사용할 수 있다.

<br/>

## Web Service Architecture

아래와 같이 다양한 구조를 가질 수 있다.  
(1) Client - 웹 서버 - DB  
(2) Client - WAS - DB  
(3) Client - 웹 서버 - WAS - DB

![68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7765622d736572766963652d6172636869746563747572652e706e67](https://user-images.githubusercontent.com/66757141/207196924-7ef2ded5-aa38-43a5-962a-fe0fbbdb288b.png)

<br/>

---

## Reference

👍 https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html  
📄 https://change-words.tistory.com/entry/Jetty-Tomcat-JBoss-WebLogic-WebSphere-JEUS
📄 https://code-lab1.tistory.com/199  
📄 https://yozm.wishket.com/magazine/detail/1780/  
📄 https://doozi316.github.io/web/2020/09/13/WEB26/
