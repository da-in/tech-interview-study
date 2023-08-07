# Web

## RESTful API
<details>
  <summary> REST란 무엇인가요? </summary>  
  
  > REST란 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미합니다. 구체적으로 설명하자면 HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD 를 적용하는 것을 의미합니다.

</details>

<details>
  <summary> 자원이란 무엇인가요? </summary>  

  > 자원은 접근할 때 구분이 되는 고유한 아이디이자 해당 소프트웨어가 관리하는 모든 것입니다.
</details>

<details>
  <summary> REST와 RESTful의 차이는 무엇인가요? </summary>  

  > RESTful은  REST의 설계 규칙을 잘 지켜서 만들어진 것을 의미합니다. 
</details>

<details>
  <summary> REST의 구성요소에 대해 설명해주세요. </summary>  

  > REST의 구성 요소로는 자원, 행위, 표현이 있습니다. </br>
  >- 자원은 URI입니다. 모든 자원에는 고유한 아이디가 존재하고, 이 자원은 서버에 존재합니다. </br>
  >- 행위는 Method로 GET, POST, PATCH, DELETE 등의 HTTP Method를 사용합니다. </br>
  >- 표현은 클라이언트와 서버가 데이터를 주고받는 응답의 형태로 JSON, XML 등이 있습니다.

</details>

<details>
  <summary> REST의 장점은 무엇인가요? </summary>  

  >- 통신이 균일하기 때문에 형태에 상관없이 사용할 수 있습니다.
  >- HTTP 프로토콜의 인프라를 그대로 사용하기 때문에 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없습니다.
  >- HTTP 프로토콜의 표준을 활용하기 때문에 여러 추가적인 장점을 함께 가져갈 수 있습니다.
  >- HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용이 가능합니다.
  >- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있습니다.
  >- 서버와 클라이언트의 역할을 명확하게 분리할 수 있습니다.

</details>

<details>
  <summary> REST의 단점은 무엇인가요? </summary>  

  >- HTTP 통신할때만 사용이 가능합니다.
  >- 행위의 Method 가 제한적입니다.
  >- 표준이 존재하지 않습니다.
</details>

<details>
  <summary> 행위의 Method들의 대해서 설명해주세요. </summary>  

  >- GET : 정보를 요청(Read)
  >- POST : 정보를 입력(Create)
  >- PUT : 정보를 업데이트 (Update)
  >- PATCH : 정보의 일부만 업데이트(Update)
  >- DELETE : 정보 삭제(Delete)
</details>

<details>
  <summary> REST가 필요한 이유는 무엇인가요? </summary>  

  > 서버가 통신할 때 통신에만 집중이 가능하여 원할한 통신을 할 수 있습니다. 또한 애플리케이션의 분리 및 통합, 다양한 클라이언트의 등장과 최근의 서버 프로그램은 다양한 브라우저와 안드로이드폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 합니다. 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 설계하고 이용하는 방법을 모색한 결과, REST의 필요성이 커지게 되었습니다.
</details>

<details>
  <summary> REST의 특징중 하나인 무상태성에 대해서 설명해주세요. </summary>  

  > 무상태성이란 클라이언트의 context를 서버에 저장하지 않는 걸 의미합니다. 즉, 세션이나 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해집니다. 또한 무상태성을 갖게되면 서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리합니다. 
</details>

<details>
  <summary> URI는 무엇인가요? </summary>  

  > 통신을 할 때 사용하는 자원의 고유 아이디로서 URI를 통해 자원을 식별합니다.
</details>

<details>
  <summary> API란 무엇인지 구체적으로 설명해주세요. </summary>  

  > 데이터와 기능을 제공하여 컴퓨터 프로그램간 상호작용을 하며, 서로 정보 교환이 가능하게 해주는 매개체입니다. 즉, 통신을 할 때 정해놓은 규약이나 약속인데 이를 통해 원할하게 통신이 가능합니다. 
</details>

<details>
  <summary> REST 원칙 중, 클라이언트-서버 구조에 대해 설명해주세요. </summary>  

  > 클라이언트 응용 프로그램과 서버 응용 프로그램이 서로에 대한 종속성 없이 분리되어 개발되어야 함을 의미합니다. 클라이언트는 서버의 내부 동작에 대한 이해 없이, 리소스 URI만을 알고 동작해야합니다. 서버와 클라이언트는 인터페이스가 변경되지 않는 한 독립적으로 교체 및 개발될 수 있어야 함을 의미합니다.
</details>

<details>
  <summary> 클라이언트와 서버를 분리해서 개발하는 이유는 무엇인가요? </summary>  

  > 클라이언트와 서버를 구분해서 개발하면 각자의 역할이 명확해집니다. 이를 통해 서로 간의 의존성을 최소화하여 개발이 가능하다고 생각합니다.
</details>

<details>
  <summary> 표현 계층에서 보통 자원을 어떻게 표현하나요? </summary> 

  > Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 대해 응답(표현)을 보내는데, 자원은 `JSON`, `XML`, `TEXT`, `RSS` 등으로 표현되어 나타내질 수 있습니다. 그 중에서도 `JSON` 혹은 `XML`을 통해 전달하는 것이 일반입니다.

</details>
