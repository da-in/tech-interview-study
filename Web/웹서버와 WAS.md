# 웹 서버(WS)와 웹 어플리케이션 서버(WAS)

웹서버(WS)와 WAS는 서버를 구성하는 기초적인 개념이지만 혼동하기 쉽다. 웹서버와 WAS의 차이점을 살펴본다.

<br/>

## Static Page & Dynamic Page

#### 정적 페이지(Static Page)

요청한 자원의 경로와 일치하는, 서버에 미리 저장된 파일이 그대로 전달되는 웹페이지를 말한다.  
항상 동일한 페이지를 반환한다.  
ex | image, html, css, javascript 파일과 같이 하드웨어에 저장되어 있는 파일들.

#### 동적 페이지(Dynamic Page)

클라이언트의 요청 인자에 따라 스크립트에 의해 동적으로 생성 후 반환되는 페이지를 의미한다.

![static-vs-dynamic](https://gmlwjd9405.github.io/images/web/static-vs-dynamic.png)

<br/>

## Web Server

웹 서버란 HTTP 프로토콜을 기반으로 클라이언트의 요청을 받아 **정적 컨텐츠**를 제공하는 서버이다. 정적 컨텐츠란 위에서 설명한 것과 같이 단순 HTML 문서, CSS, 이미지, 파일 등 즉시 응답 가능한 컨텐츠이다.

웹 서버가 정적 컨텐츠가 아닌 동적 컨텐츠를 요청받으면 WAS에 해당 요청을 넘겨주고, WAS에서 처리한 결과를 클라이언트에게 전달하는 역할도 한다.

이러한 웹 서버에는 Apache, NginX 등이 있다.

<br/>

## WAS

![WAS](https://gmlwjd9405.github.io/images/web/webserver-vs-was1.png)

WAS란 DB 조회 혹은 다양한 로직 처리를 요구하는 동적 컨텐츠를 제공하기 위해 만들어진 Application 서버이다.

WAS는 Web Server + Web Container 이다.
_\* Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다._

HTTP 프로토콜을 기반으로 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로서, 주로 데이터베이스 서버와 같이 수행된다.
WAS는 JSP, Servlet 구동환경을 제공해주기 때문에 **서블릿 컨테이너\*** 혹은 **웹 컨테이너\*** 로 불린다.

WAS는 웹 서버의 기능들을 구조적으로 분리하여 처리하고자 하는 목적으로 제시되었다. 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다. WAS는 프로그램 실행 환경과 DB 접속 기능을 제공하고, 여러 개의 트랜잭션을 관리 가능하다. 또한 비즈니스 로직을 수행할 수 있다.

WAS에는 Tomcat, JBoss, WebSphere 등이 있다.

<br/>

## WAS와 Web Server를 분리하는 이유.

WAS도 웹 서버의 역할을 할 수 있지만 분리하는 이유는 다음과 같다.

1. **서버 부하 방지**  
   WAS와 웹 서버는 분리하여 서버의 부하를 방지해야 한다. WAS는 DB 조회나 다양한 로직을 처리하고, 단순한 정적 컨텐츠는 웹 서버에서 처리해줘야 한다. 만약 정적 컨텐츠까지 WAS가 처리한다면 부하가 커지고 수행 속도가 느려질 것이다.

2. **보안 강화**  
   SSL에 대한 암호화, 복호화 처리에 웹 서버를 사용 가능

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

![web-service-architecture](https://gmlwjd9405.github.io/images/web/web-service-architecture.png)

<br/>

---

## Reference

👍 https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html  
📄 https://code-lab1.tistory.com/199  
📄 https://yozm.wishket.com/magazine/detail/1780/
