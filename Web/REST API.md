# REST란?

Representational State Transfer의 약자로, 
2000년도에 로이 필딩 (Roy Fielding)에 의해 웹(HTTP) 설계의 우수성에 비해 제대로 사용되어지지 못하는 모습에 안타까워하며 웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표했다.  
자원을 이름(자원의 표현)으로 구분해 해당 자원의 상태(정보)를 주고 받는것을 의미하며, 자원(resource)의 표현(representation)에 의한 상태 전달을 뜻한다.

## REST의 구성
1. 자원(Resource) - URI  
    - 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재한다. 
    - 자원을 구별하는 ID는 '/exgroups/:exgroup_id'와 같은 HTTP URI이고, 
    - Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.

2. 행위(Method) - HTTP Method
    - HTTP Method들을 사용함
    - 자세한 내용은 <링크> 참고

3. 표현(Representation)
    - Client와 Server가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있다.
    - 제일 많이 사용되는 건 JSON, XML


## REST의 특징
1. Server-Client(서버-클라이언트 구조)
  - 자원이 있는 쪽이 서버, 자원을 요청하는 쪽이 클라이언트
    - REST 서버는 API를 제공하고 비즈니스 로직 처리 및 저장
    - 클라이언트는 사용자 인증, context(세션, 로그인 정보)를 직접 관리
    - 역할을 확실히 구분함으로써 서로 간의 의존성을 줄임
2. Stateless(무상태)
  - HTTP프로토콜은 Stateless 프로토콜이므로 REST도 무상태성을 가짐
    - 무상태성이란? 상태정보(세션 정보, 쿠키 정보)를 별도로 저장하고 관리하지 않음
  - 클라이언트의 context를 서버에 저장하지 않음 -> 구현이 단순해짐
  - 서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리함
    - 각 API 서버는 클라이언트의 요청만을 단순 처리하므로 서버의 처리 방식에 일관성이 생김 -> 서비스의 자유도가 높아짐
3. Cachable(캐시 처리 기능)
  - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있음
    - HTTP가 가진 특징 중에 캐싱기능을 적용하고 구현할 수 있음(대표적으로 Last-Modified Tag, E-Tag)
  - 대량의 요청을 효율적으로 처리할 수 있음
4. Layered-System(계층 구조)
  - REST 서버는 다중계층으로 구성될 수 있음
    - 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 주고를 변경할 수 있음
    - Proxy, Gateway와 같은 네트워크 기반의 중간매체 사용가능
5. Uniform Interface(인터페이스 일관성)
  - URI로 지정한 자원에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미함
  - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능.(특정 언어나 기술에 종속되지 않음)
6. Self-Descriptiveness(자체 표현)
  - 요청 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조임

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
4. 밑줄(_)을 사용하지 않고, 하이픈(-)을 사용한다.
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
