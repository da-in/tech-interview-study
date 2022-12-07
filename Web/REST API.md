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
  - HTTP Method들을 사용함.
  - 자세한 내용은 <링크> 참고

3. 표현(Representation)
  - Client와 Server가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있다.
  - 제일 많이 사용되는 건 JSON, XML


## REST의 특징
1. Server-Client(서버-클라이언트 구조)
2. Stateless(무상태)
3. Cachable(캐시 처리 기능)
4. Layered-System(계층 구조)
5. Uniform Interface(인터페이스 일관성)
6. Self-Descriptiveness(자체 표현)

# REST API란?


# REST API와 RESTful API의 차이
