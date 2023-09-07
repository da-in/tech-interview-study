# REST

REST는 REpresentational State Transfer 의 약자이다.
2000년도에 웹이 설계의 우수성에 비해 제대로 사용되지 못하였고, 이를 안타까워한 로이 필딩(Roy Fielding)은 웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표했다.

REST의 핵심은 **자원**(Resource)의 **표현**(Representation)에 의한 상태(Status)전달이다. REST에 따르면 HTTP URI를 통해 자원을 표현하고, [HTTP 메서드](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Web/HTTP%20Request%20Method.md)를 통해 해당 자원에 대한 상태 및 동작을 수행한다.

## REST의 구성

REST 아키텍처를 이루는 구성은 다음과 같다.

- 자원(Resource)
  - 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
  - 자원을 구별하는 ID는 HTTP URI이다.
  - Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태에 대한 조작을 Server에 요청한다.
- 행위(Method)
  - [HTTP Requset Method](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Web/HTTP%20Request%20Method.md)를 사용한다.
- 표현(Representation)
  - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 대해 응답(표현)을 보낸다.
  - 자원은 `JSON`, `XML`, `TEXT`, `RSS` 등으로 표현되어 나타내질 수 있다. `JSON` 혹은 `XML`을 통해 전달하는 것이 일반적이다.

## REST의 6가지 원칙과 RESTful

아래의 원칙을 지켜 개발하면 RESTful한 API를 만들 수 있다. 꼭 모든 원칙을 지키지는 않아도 RESTful하다고 할 수 있으며, truely RESTful 하지 않을 뿐이다.

1.Client-Server(클라이언트-서버 구조)

- Client Application과 Server Application은 반드시 서로간의 의존성 없이 개발되어야한다.
  - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client인 구조를 갖는다.
  - REST 서버는 API를 제공하여 비즈니스 로직을 처리 및 저장하고, Client는 오직 URI만을 알고있어야한다.
  - 역할을 명확히 구분함으로서 서로의 의존성을 줄인다.

2. Stateless(무상태)

- 서버는 클라이언트가 요청한 HTTP request에 대해서 상태정보(세션, 쿠키 등)를 저장하지 않는다.
  - HTTP 프로토콜은 무상태성을 갖고, 이를 따르는 REST도 무상태성을 가짐.
  - 클라이언트의 Context를 서버에 저장하지 않아 구현이 단순해진다.

3. Caching(캐싱)

- 데이터나 응답을 가능하다면 캐싱한다.
  - 캐싱은 성능향상과 server에 대한 확장성을 증가시키고 대량의 요청을 효율적으로 처리할 수 있게 한다.
  - 캐싱은 server 또는 client에서 구현될수 있다.

4. Hierarchical System(계층 구조)

- REST는 계층 시스템 아키텍처(Layered System Architecture)를 허용한다.
  - 예를 들어 API는 A서버에서, Data 저장은 B서버에서, 요청 검증은 C서버에서 진행할 수 있다.
  - 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 구조를 변경할 수 있고, Proxy, Gateway와 같은 네트워크 기반의 중간매체 사용가능
  - 이 때 Client는 End-Server에 연결되었는지 매개체에 연결되었는지 알 수 없다.

5. Uniform Interface(인터페이스 일관성)

- URI로 지정한 자원에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미한다.
- 특정 언어나 기술에 종속되지 않고, HTTP 표준 프로토콜, REST를 따르는 모든 플랫폼에서 사용 가능하다.

6. Code on demand(optional)

- 대부분은 `XML`이나 `JSON`형태로 리소스들에 대한 정적인 표현으로 응답하게되지만, Application의 일부를 지원하기 위해 `executable code`를 보낼수도 있다.

# REST API란?(사실 여기부터 본론입니다 머쓱;)

## REST API의 정의

- REST의 특징을 기반으로 서비스 API를 구현한 것

## REST API의 특징

- REST API는 각 요청이 어떤 동작이나 정보를 위한 것인지를 요청의 모습 자체로 추론이 가능한 것이다.
  - ex) POST.../content -> "아하! 게시물을 작성하는 요청이구나!"(희망편)

## REST API 디자인 가이드

1. URI는 정보의 자원을 표현해야 한다.
2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.

## REST API 설계 규칙

1. URI는 명사를 사용한다.
   - 동사를 사용하지 말것! ex) /createUser ... 등등
2. 슬래시(/)로 계층관계를 표현한다.
3. URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
4. 밑줄(\_)을 사용하지 않고, 하이픈(-)을 사용한다.
5. URI는 소문자로만 구성한다.
6. HTTP응답 상태 코드 사용
   - <HTTP 상태코드 완성되면 여기 링크 넣기>
7. 파일확장자는 URI에 포함하지 않는다. ex) .../sample.png

# REST API와 RESTful API의 차이

RESTful은 REST의 설계 규칙을 잘 지켜서 설계된 API를 RESTful한 API라고 한다.  
REST의 원리를 잘 따르는 시스템 = RESTful하다!  
(여담이지만, 성능이 중요한 상황이라면 굳이 RESTful하지 않아도 된다고 합니다.)

---

## 출처

https://dev-coco.tistory.com/97#REST%EC%-D%--%--%EC%A-%--%EC%-D%--  
https://meetup.toast.com/posts/92
